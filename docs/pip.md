# ![logo](img/logo_small.png) PIP | upip | pipi

Postupně pracujeme na vlastních "balíčcích" (packages), které budeme distribuovat pomocí `pip` (package installer for Python), přesněji `upip` (pro Micropython).
V prvním kroku chceme k čisté "vanila" binárce Micropthonu doplnit [octopus_initial.setup()](../install/#octopus_initialsetup) v nějaké "lite" verzi z githubu nebo z vlastního cloudu:

► [github/octopuslab-installer](https://github.com/octopusengine/octopuslab-installer)

```python
import upip
upip.install('shutil')  # TODO include in `setup.py`
upip.install('micropython-octopuslab-installer')
from lib import octopuslab_installer
octopuslab_installer.deploy()
```

---

## uPip

►► [micropython/packages](https://docs.micropython.org/en/latest/reference/packages.html)


```python
>>> import upip
>>> upip.help()
upip - Simple PyPI package manager for MicroPython
Usage: micropython -m upip install [-p <path>] <package>... | -r <requirements.txt>
import upip; upip.install(package_or_list, [<path>])

If <path> is not given, packages will be installed into sys.path[1]
(can be set from MICROPYPATH environment variable, if current system
supports that).
Current value of sys.path[1]: /lib

Note: only MicroPython packages (usually, named micropython-*) are supported
for installation, upip does not support arbitrary code in setup.py.
```


V dalších krocích chceme používat `pipi` (the Python Package Index), který zkoušíme na vlastní doméně.

►► [pypi.org/](https://pypi.org/)

---