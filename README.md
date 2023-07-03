
# A big bugfix is applied to this package due to the technique Python uses to import modules.

In previous versions, when brainfuck_to_function is called, it creates a module named _foo, which is imported. But Python also stores it into a cache, that means when you call brainfuck_to_function again, the new module would not be imported, which causes a function the same as the previous function is returned.

However, in this version and higher, a module with a random name is created instead, which fixed the bug.

### Fast Brainf**k

The real name of this package is not fast-bf, it's [fast-brainf**k](https://pypi.org/project/fast-brainfuck/).

To install it, use the command

```commandline
pip install fast-brainfuck
```

You also need a C++ compiler.

To use the package, run like this:

```python
>>> from fastbf import brainfuck_to_function
>>> code='++++++++[>++++++++<-]>++++++++.>++++++++++++[>++++++++<-]>+++++.+++++++..+++.>++++[>++++++++<-]>.<<<<+++++++++++++++.>>.+++.------.--------.>>+.'
>>> func=brainfuck_to_function(code) # This will take several seconds, because the C++ compiler is compiling your code.
>>> func
<built-in method run of PyCapsule object at 0x0000022568364150>
>>> func() # About 3x faster than using a brainfuck interpreter implemented in C++.
Hello World!
```

You can also convert brainf**k to Python modules by writing setup.py like this:

```python
from fastbf import dist_brainfuck
code='++++++++[>++++++++<-]>++++++++.>++++++++++++[>++++++++<-]>+++++.+++++++..+++.>++++[>++++++++<-]>.<<<<+++++++++++++++.>>.+++.------.--------.>>+.'
dist_brainfuck(
    code,modulename='hello'
)
```

Then run **python setup.py build_ext --inplace** (Do not run other commands, will not work).
That will created a Python extension module and hello.py, you now can import it in other scripts:

```python
import hello
hello.run() # Hello World!
```

Note that moving the pointer to the left of the origin causes **UNDEFINED BEHAVIOR** in this version, that's why I change the Hello World code.
The version 2.0.6 and 2.0.7 are omitted here, because they are already yanked.
