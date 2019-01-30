# Quantization Summary

## 1. Paper Summary

### 1.1. PACT- Parameterized Clipping Activation for Quantized Neural Networks
#### 1.1.1. When Using Lower Precision, When Using Higher
During some operations which include "averaging", such as the calculation of gradients 
during back propogation, since averaging has effect of "compensate". On the other hand, 
some operation, such as traditional activation function, which do not include "averaging" 
operation across batch samples, so we should use higher precision to execute this kind 
of operations.


### 1.2. Training deep neural networks with low precision multiplications
#### 1.2.1. Key(How To Dynamically Control Loss Scale Factor)
Use the idea of "dynamic fixed point", the "dynamic" means the precision of 
the data flow to different operations has unique shared fixed exponent. Refer 
to page 3.  
