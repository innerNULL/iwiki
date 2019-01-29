# Mixed Precision Training

* reference:  
    https://arxiv.org/abs/1710.03740  
    https://github.com/NVIDIA/apex  
    https://nvidia.github.io/OpenSeq2Seq/html/mixed-precision.html#  
    https://devblogs.nvidia.com/apex-pytorch-easy-mixed-precision-training/ 

## 1. Introduction  
The paper "Mixed Precision Training" is easy to read after understanding 
some underlying computer system knowledge such as data type, so here just 
introduce some tips and extension of the paper by summary some industrial 
implementation.  


## 2. Extension

### 2.1. Loss Scaling
As the paper mentioned, loss scaling is really useful when putting the "compressed" 
parameters into the range in which lower data precision can represent them. This tech 
could be used in two approach, one is using static loss scaling factor, other is using 
dynamic loss scaling factor. The first one is easy to understand, now focus on the 
dynamic one.  

The paper mentioned "automating loss-scaling factor" at last, the author means, for 
instance, if some gradients or parameters happened overflow, which means these number 
is to large to represented by float16, so we should decrease loss-scaling factor, on 
the other hand, if underflow happens, in this case we should increase loss-scaling 
factor.  

OpenSeq2Seq did more on "automating loss-scaling factor". OpenSeq2Seq implements 
an extension to the mixed precision recipe that we call **automatic loss scaling**. 
The optimizer inspects the parameter gradients at each iteration and uses their 
values to select the loss scale for the next iteration.  Concretely, OpenSeq2Seq 
has support for two automatic loss scaling algorithms, Backoff and LogNormal scaling.  

#### 2.1.1. Backoff Scaling
Backoff scaling begins with a large loss scale and checks for overflow in the 
parameter gradients at the end of each iteration. Whenever there is an overflow, 
the loss scale decreases by a constant factor (default is 2) and the optimizer will 
skip the update. Furthermore, if there has been no overflow for a period of time, 
the loss scale increases by a constant factor (defaults are 2000 iterations and 2, 
respectively). These two rules together ensure both that the loss scale is as large 
as possible and also that it can adjust to shifting dynamic range during training.  

This scaling method is similiar with "dynamic fixed point" method mentioned in 
"Training deep neural networks with low precision multiplications".

#### 2.1.2. LogNormal Scaling
LogNormal scaling uses gradient statistics, rather than the presence of overflow, 
to set the loss scale. It keeps a running estimate of the mean and variance of 
the inter-iteration maximum absolute value of the parameter gradients. It models 
the inter-iteration maximum as log-normally distributed (hence the name), and then 
chooses the loss scale for the next iteration s.t. the probability of the maximum 
overflowing float16 is less than some constant (default is 0.001). In the rare 
event of an overflow, the optimizer skips the update.



