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
>>> code='--<-<<+[+[<+>--->->->-<<<]>]<<--.<++++++.<<-..<<.<+.>>.>>.<<<.+++.>>.>>-.<<<+.'
>>> func=brainfuck_to_function(code) # This will take several seconds, because the C++ compiler is compiling your code.
>>> func
<built-in method run of PyCapsule object at 0x0000022568364150>
>>> func() # About 3x faster than using a brainfuck interpreter implemented in C++.
Hello World!
```

You can also convert brainf**k to Python modules by writing setup.py like this:

```python
from fastbf import dist_brainfuck
code='--<-<<+[+[<+>--->->->-<<<]>]<<--.<++++++.<<-..<<.<+.>>.>>.<<<.+++.>>.>>-.<<<+.'
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

