# ![logo](img/logo_small.png) PIP | upip | pypi

Pracujeme na vlastních "instalačních balíčcích" (packages) pro [Rozšíření MicroPythonu](/extension). Tyto balíčky se nejčastěji instalují pomocí `pip` (**package installer for Python**), přesněji `upip` (pro Micropython). Chceme používat `pypi` (**the Python Package Index**) na stránkách 🡒 [pypi.org/](https://pypi.org/).

## micropython-octopus-installer

Základním instalačním balíčkem je `micropython-octopus-installer`, nahrazující [octopus_initial.setup()](../install/#octopus_initialsetup) v "lite" verzi.

🡒 [pipi.org/octopuslab-installer](https://pypi.org/project/micropython-octopuslab-installer/#data)

🡒 [github.com/octopuslab-installer](https://github.com/octopusengine/octopuslab-installer)

🡒[Micropython](http://micropython.org/download/esp32/) pro ESP32. (Používáme zatím lépe otestovanou verzi `ESP-IDF v3.x`)
V této základní (vanilla) verzi Micropythonu stačí provést dva následující kroky:


**Připojení k WiFi**

Můžete použít copy&paste celého bloku popmocí `CTRL+E`
(nezapomeňte si vyplnit svoje ssid a heslo).

```python
import network
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect('ssid', 'password')
```

**Instalace metody deploy() z octopuslab_installer**
```python
import upip
upip.install('micropython-octopuslab-installer')

# wait for install

from lib import octopuslab_installer
octopuslab_installer.deploy()
```

---

## uPip

🡒 [micropython/packages](https://docs.micropython.org/en/latest/reference/packages.html)


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


---

Připravujeme: [deployer](/deployer)

---

Možnosti instalace dalších "balíčků" uvádíme v samostatné kapitole [Rozšíření MicroPythonu](/extension).

---