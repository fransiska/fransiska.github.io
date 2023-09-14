---
layout: post
title: Creating .so files from python
tags: [python, cython]
---

Refs: [The manual setup in this zip file](https://groups.google.com/g/cython-users/c/6trL0V1bLx4/m/7bxhj0xCK50J)

I want to be able to execute normal python files (not with `.pyx` or need compiling) during development and yet to be able to distribute it in binary.

The structure of the files:

```
setup.py
src/
  __init__.py
  example.py
  hellow/
    __init__.py
    hellow.py
```

The content of `example.py`

```python
import hellow.hellow as hellow

if __name__ == '__main__':
    hellow.hellow()
```

The content of `hellow.py`

```python
def hellow():
    print("hellow from cython")
```

We can go to the root folder of the project and `python src/example.py` to run. We can then build the `hellow` module as `.so` files.

The content of `setup.py`

```python
from distutils.core import setup
from distutils.extension import Extension
from Cython.Distutils import build_ext

ext_modules = [
    Extension("src.hellow.hellow", ["src/hellow/hellow.py"], include_dirs=['.'])
]

setup(
  name='workingCythonMultiPackageProject',
  cmdclass={'build_ext': build_ext},
  ext_modules=ext_modules,
  script_args=['build_ext'],
  options={'build_ext':{'inplace':True, 'force':True}}
)
```

Run with `python setup.py`. It will produce a `.c` file and compile it to be `.so` file. The files will be put in the same folder as the `.py`file, ie.:

```
setup.py
src/
  __init__.py
  example.py
  hellow/
    __init__.py
    hellow.py
    hellow.c
    hellow.cpython-39-darwin.so
```

Now, if we want to distribute this `.so` files, we can just copy it into the python's lib folder. I'm using pyenv here, so I'm copying it into the `~/.pyenv/versions/3.9.14/lib/python3.9` folder

```
hellow/
  hellow.cpython-39-darwin.so
```

We can then copy the `example.py` elsewhere and run it without having the `hellow` folder in the same directory! Oh this is much simpler than I thought.

For the cherry on top, we can also binarize the `example.py`

```bash
cd src
cython example.py --embed # Creates example.c
PYTHONLIBVER=python$(python3 -c 'import sys; print(".".join(map(str, sys.version_info[:2])))')$(python3-config --abiflags)
gcc -Os $(python3-config --includes) example.c -o example $(python3-config --ldflags) -l$PYTHONLIBVER # creates example binary
```

The resulting `example` binary file can also be run from any folder.
