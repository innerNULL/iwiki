# Quantization Summary

## 1. Paper Summary

### 1.1. PACT- Parameterized Clipping Activation for Quantized Neural Networks
#### 1.1.1. When Using Lower Precision, When Using Higher
During some operations which include "averaging", such as the calculation of gradients 
during back propogation, since averaging has effect of "compensate". On the other hand, 
some operation, such as traditional activation function, which do not include "averaging" 
operation across batch samples, so we should use higher precision to execute this kind 
of operations.

#### 1.1.2. Clipping Activation Function
Clipping activation sometimes can has lower training error, but higher validation error.  
Refer to page 3.

#### 1.1.3. Disadvantage of Similiar Method
* Deep Learning with Low Precision by Half-wave Gaussian Quantization


### 1.2.Deep Learning with Limited Numerical Precision
#### 1.2.1. Ficed Pointed Format Notations
* Representation: \<IL, FL\>. Page 2.
* Representable Range: Page 3.
* Smallest Representable Positive Number: Page 3.

#### 1.2.2. Rounding Modes
Includes Round-to-Nearest, Stochastic-Rounding.


#### 1.2.4. Tips
* Saturate the result: Page 3.


### 1.3. Training deep neural networks with low precision multiplications
#### 1.3.1. Key(How To Dynamically Control Loss Scale Factor)
Use the idea of "dynamic fixed point", the "dynamic" means the precision of 
the data flow to different operations has unique shared fixed exponent. Refer 
to page 3.  
