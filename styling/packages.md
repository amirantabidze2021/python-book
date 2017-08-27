# Packages

> Package is directory with modules

Why do we need them?
* For structuring modules for easier usage

How to create a package?
1. Create directory
2. Place there special (maybe empty) file `__init__.py`
3. That's it.

```python
helpers/               Top-level package
    __init__.py        Init the helpers package
    file_processors/       Subpackage
        __init__.py        Init the subpackage
        parser.py              Module from package
        saver.py               Module from package 
main.py                Main module (entry point)
```

In `main.py` we can import presented packages/modules in the following ways:

```python
import helpers.file_processors.parser
from helpers.file_processors import parser
from helpers.file_processors import parser, saver
from helpers.file_processors import parser as ps
from helpers.file_processors.parser import *
```

If we need to import something in package's modules - it's better to use absolute import and specify path to needed module.
It will be possible because entry point is `main.py` and `PYTHONPATH` will be set accordingly.