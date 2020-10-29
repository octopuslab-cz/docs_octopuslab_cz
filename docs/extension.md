# ![logo](img/logo_small.png){: style="width:39px" } Rozšíření Micropythonu

Možnost rozšíření Micropythonu o vlastní moduly jsme si již zmínili u [octopus_initial.setup()](/install/#octopus_initialsetup).
Máme více možností, zmíníme tři základní varianty.

1. Rozšíření je implementováno do samotného Mictopythonu (což využíváme ve forku micropython-octopus).

2. Máme možnost si přihrát vlastní modul (například do adresáře `/lib`), což je například celý **Octopus FrameWork**.

3. Varianta, na kterou se zaměříme je využití `pip` (package installer for Python) v případě Micropythonu [upip](/pip).

---

## octopuslab_installer

Pro instalci  **Octopus FrameWork** využíváme metody `deploy()` z "balíčku" `octopuslab_installer`.

```python
... WiFi conncect

import upip
upip.install('micropython-octopuslab-installer')

# wait for install
from lib import octopuslab_installer
octopuslab_installer.deploy()
```

---

## itertools

V "dospělém" Pythonu existuje "modul" itertools, který umožní pokročilejší práci s "iterátory".
Například podle následující ukázky využíváme metodu `cycle()` s možností `next()`:

```python
import itertools as it

players = ["John", "Alice", "Bob"]
player_choice = it.cycle(players)

print(next(Plyyer_choice)) # John
print(next(Plyyer_choice)) # Alice
print(next(Plyyer_choice)) # Bob
print(next(Plyyer_choice)) # John
print(next(Plyyer_choice)) # Alice
...
```

V Micropythonu itertools nenajdeme, ale naštěstí existuje možnost snadné instalace `upip.install("micropython-???")`:

```python
... WiFi conncect

>>> import upip
>>> upip.install('micropython-itertools')

Installing to: /lib/
Warning: micropython.org SSL certificate is not validated
Installing micropython-itertools 0.2.3 from https://micropython.org/pi/itertools/itertools-0.2.3.tar.gz

```

---

## Některé další moduly

- https://libraries.io/pypi/micropython-sqlite3

- https://pypi.org/project/micropython-itertools/

- https://libraries.io/pypi/micropython-vec vectors

- https://pypi.org/project/micropython-wifimanager/

- https://pypi.org/project/micropython-wifi-setup/

- https://pypi.org/project/micropython-mailbox/

- https://pypi.org/project/micropython-email.utils/

- https://pypi.org/project/micropython-mqtt/

- https://pypi.org/project/micropython-umqtt.simple/

- https://pypi.org/project/micropython-mqtt-async/

- https://pypi.org/project/micropython-umqtt.robust/

- https://pypi.org/project/micropython-uaiohttpclient/

- https://pypi.org/project/micropython-bme280/

- https://pypi.org/project/micropython-dht12/ sensor

- https://pypi.org/project/micropython-pcf8591/ i2c (4x A/D, 1x D/A)

- https://pypi.org/project/micropython-mpu6886/ gyroskop

- https://pypi.org/project/micropython-ssd1306/ oled

- https://pypi.org/project/micropython-pcd8544/ nokia displ.

- https://libraries.io/pypi/micropython-rfsocket

---
