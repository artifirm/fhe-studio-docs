# FHE Development Guide

# FHE Circuits
Fully homomorphic encryption (FHE) is often represented and understood in terms of circuits because it enables secure computation using a method similar to how digital circuits work. <br/>
FHE circuits are a way to describe how encrypted data flows through a sequence of mathematical operations, just like how electronic signals flow through a digital circuit. The term "circuit" is used to describe this process, as it follows a similar concept of combining simple operations to achieve complex computation while preserving the security of the underlying data.

# FHE Circuits Limitations
First it is slow. This is why it is very important to give a circuit correct narrowed input examples known as `inputset`. Lower values are better because it takes less bit in encrypted evaluations.<br/>
FHE has two operations: addition (including subtraction) and multiplication over integer numbers, but not division.<br/>
However you still can implement lots of functions like `cos` and `sin`, but you have to sample them in an array and use `LookupTable`. Fair number of such functions are already implemented this way by the engine itself. [The list of available function is here](https://docs.zama.ai/concrete/getting-started/compatibility).
<br>
Please note, the `comparison` is implemented also using lookup tables, so it not as simple operation in FHE.


# FHE Circuit Source 

Here is an example of basic circuit that adds two numbers:
```python
from concrete import fhe

def add(x, y):
    return x + y

compiler = fhe.Compiler(add, {"x": "encrypted", "y": "clear"})

inputset = [(2, 3), (0, 0), (1, 6), (7, 7), (7, 1)]
circuit = compiler.compile(inputset)

x = 4
y = 4

clear_evaluation = add(x, y)
homomorphic_evaluation = circuit.encrypt_run_decrypt(x, y)

print(x, "+", y, "=", clear_evaluation, "=", homomorphic_evaluation)
```
<br/>

The circuit operates with binary data behind the scenes and it needs to know how many bits of internal variable should be sufficient to evaluate incoming encrypted data. <br>
For this reason we have to give few examples of input data, e.g. 
```python
inputset = [1, 2, 4, 10]
```
or 
```python
inputset = range(10)
```
And below, there are few input arguments. Then `inputset`holds arrays of tuples 

```python
@fhe.compiler({"x": "encrypted", "y": "encrypted"})
def circuit(x,y):
    return x + y + 42

inputset = [(1,1), (5,5), (10,10)]
```
[For more examples you can refer to the underline FHE engine](https://docs.zama.ai/concrete/getting-started/quick_start)

# Lookup Tables
You can create a lookup table using FHE

```python
table = fhe.LookupTable([2, -1, 3, 0])

@fhe.compiler({"x": "encrypted"})
def circuit(x):
    return table[x]

inputset = range(4)
```

### Matrix Multiplication
```python
import numpy as np
a = [[1,2]]

@fhe.compiler({"x": "encrypted", "b": "encrypted"})
def circuit(x, b):
    m = np.matmul(a,x)
    return np.sum(m) + b

inputset = [([1,2],3)]
```

### Linear Regression
```python
import numpy as np

# TFHE support only integers, so we need to quantify floats to ints
#
# Quantization could be a bit more complex to reach the better results, 
# more is here https://huggingface.co/docs/optimum/concept_guides/quantization
def qvalues(values):
    return np.rint(np.array(values) * 127. + 0 ).astype(np.int8)

#linear model intercept
intercept = qvalues([-.53]).item()

#linear model coefs
theta = [ qvalues([0.3, .1, .2]) ] 

@fhe.compiler({"x": "encrypted"})
def circuit(x):
    m = np.matmul(theta,x)
    # keep in mind, the decrypted value needs to be devided by 127*127
    #to dequantifized because of matmul at the previous step
    return np.sum(m) + intercept

inputset = [ qvalues([-.9, -.9, -.9]), qvalues([.9, .9, .9]) ]
```