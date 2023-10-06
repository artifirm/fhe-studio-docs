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

Here is an example of basic circuit that adds 42 to an encrypted number:
```python
@fhe.compiler({"x": "encrypted"})
def circuit(x):
    return x + 42

inputset = range(10)
```
The entrypoint should have the name `circuit`. The parameters needs to be annotated with either `encrypted` or `clear`. <br/>

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