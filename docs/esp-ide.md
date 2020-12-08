# ![logo](img/logo_small.png) ESP - IDE


## Tabulka nástrojů pro práci s ESP

- flash uPy - *"Flashování" Micropythonu*
- copy lib - *kopírování knihoven z externího zdroje*
- deploy /.py - *celé "setavení" konkrétního projektu*
- Terminal - *sériový terminál pro práci s ESP / REPL*
- IDE - *pokročilejší editor kódu*

(lib  | *.py - přesun celých knihoven nebo jen dílčí přesun souborů)


|             | - flash uPy - | - copy lib - | - deploy *.py - | - Terminal - | - IDE - |
| ----------- | :----: | :----: | :----: | :----: | :----: |
|<a href="/install_win/#2-instalace-micropythonu-do-esp">esptool</a>      |   ✅✅   |   ~   |   ❌   |    ❌    |   ❌  |
|<a href="#ampy">ampy</a>             |   ❌   |   ✅   |   ✅   |    ❌    |   ❌  |
|<a href="/install_win/#terminal-putty">putty</a>             |   ❌   |   ❌   |   ❌   |    ✅    |   ❌  |
|<a href="#rshell">rshell</a>         |   ❌   |   ✅   |   ✅   |    ✅✅    |   ~  |
|<a href="#pip">pip</a>              |   ❌   |   ✅   |   ✅✅   |    ❌    |   ❌  |
|<a href="#ftp">FTP</a>               |   ❌   |   ✅✅   |   ✅   |    ❌    |   ❌  |
|<a href="">web_server</a>            |   ❌   |   ~   |   ✅   |    ✅    |   ✅  |
|<a href="#thonny">Thonny</a>          |   ✅   |   ~   |   ✅   |    ✅    |   ✅  |
|<a href="#upycraft">uPyCraft</a>          |   ✅   |   ~   |   ✅   |    ✅    |   ✅  |
|<a href="#espy">EsPy</a>             |   ~   |   ~   |   ✅   |    ✅    |   ✅  |
|<a href="#mu">Mu</a>                 |   ~   |   ~   |   ✅   |    ✅    |   ✅  |
|<a href="/upyshell">shell / editor</a> |   ❌   |   ❌   |   ✅   |    ~    |   ~  |


*Legenda:*

✅✅  ideální | ✅  vhodné | **~**  použitelné | ❌  nevhodné

---

## ![hwsoc](img/mchtr.png){: style="width:28px" } Ampy

S programem **ampy** pracujeme v příkazové řádce svého počítače. Slouží pro "vzdálenou" práci s ESP po sériové lince, kdy nám umožňuje především přesouvat soubory **do** ESP `put`/ **z** ESP `get`, vytvářet adresáře `mkdir` a podobně.

Pozor na kolize portu - **ampy** nesmí být blokováno sériovým terminálem (screen nebo [putty](../install_win/#terminal-putty)).


### Instalace

Pro používání **ampy** musíte mít nainstalován Python3.

**Windows:**
Instalace Pythonu – hezky popsáno na https://naucse.python.cz/course/pyladies/beginners/install/

**Linux:**
Python bývá už součástí základní instalace

Instalace `ampy` přes `pip`:

```bash
pip install adafruit-ampy 
pip install adafruit-ampy --upgrade  
```

### Příkazy

```bash
ampy --help
ampy --version
¨
```

Klasickému shellu podobné:

- get
- ls
- mkdir
- put
- reset
- rm
- rmdir
- run

---

### Hlavní příkaz put

!!! attention "**Pozor**"
    Následující ukázky jsou pro Win, kde jsme detekovali port `COM6`. Stejně tak by to mohl být jiný port nebo na jiných operačních systémech to bude obdobně. Třeba pro Linux to bývá `/dev/ttyUSB0`.

```bash
ampy -p /COM6 ls
ampy -p /COM6 put main.py

ampy -p /COM6 mkdir config
ampy -p /COM6 mkdir utils
ampy -p /COM6 put ./shell/__init__.py shell/__init__.py

ampy -p /COM6 mkdir lib
ampy -p /COM6 put ./lib/max7219_8digit.py lib/max7219_8digit.py
ampy -p /COM6 put ./lib/ssd1306.py lib/ssd1306.py

...
```

---

## ![hwsoc](img/mchtr.png){: style="width:28px" } rshell 

Alternativa k [ampy](/ampy) nebo [Thony](/thony) se sériovým terminálem [screen](/install_linux/#terminal) pro Linux (běží i na Raspberry Pi).

Ke stažení 🡒 [github.com/dhylands/rshell](https://github.com/dhylands/rshell).

---

### Instalace

```
sudo pip3 install rshell
```

### Připojení a spuštění

```
rshell --buffer-size=30 -p /dev/ttyUSB0
```

Výchozí cesta k připojené desce je `/pyboard`.
Možnost nastavení editoru dalším parametrem: `- e nano`, **nano** je i výchozí (Linux).


### Základní příkazy

Podbné Linuxu: `ls` (list) a `cp` (copy file).

```
> ls /pyboard
> cp myfile.py /pyboard
> cd 
...
> edit /pyboard/main.py
...
> rsync . /pyboard
...
> exit
```

### Terminál + REPL

Plnohodnotný a stabilnější sériový terminál pro [REPL](/repl) se pustí snadno příkazem `repl`:

```
> repl
```

Pro ukončení práce s terminálem (exit: `CTRL+X`) - zpět do rshellu.


---

## ![hwsoc](img/mchtr.png){: style="width:28px" } PIP 

Hesla: PIP| upip | pypi

Pracujeme na vlastních "instalačních balíčcích" (packages) pro [Rozšíření MicroPythonu](/extension). Tyto balíčky se nejčastěji instalují pomocí `pip` (**package installer for Python**), přesněji `upip` (pro Micropython). Chceme používat `pypi` (**the Python Package Index**) na stránkách 🡒 [pypi.org/](https://pypi.org/).

### micropython-octopus-installer

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

### uPip

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

Možnosti instalace dalších "balíčků" uvádíme v samostatné kapitole [Rozšíření MicroPythonu](/extension).

---

## ![hwsoc](img/mchtr.png){: style="width:28px" } FTP


**FTP** (File transfer protocol) - protokol pro přenos souborů mezi počítači pomocí počítačové sítě.

Původní knihovna pro ESP8266 i ESP32 v základu funguje. 
Používáme například FTP plugin **Total Commanderu** (testováno ve Win 10).

Jednoduchá verze - na ESP běží samostatně "pouze" FTP. Po připojení k lokální síti se spustí FTP a vypíše IP adresu.


```python
>>> from utils.octopus_lib import w
>>> w() # wifi connect

>>> import ftp
>>> ftp
FTP Server started on  192.168.x.y # -> IP

```

Spustit se dá i ze [setup()](/setup/#setup) - příkazy `cw` -> `ftp`.

---

### Použití z Total commanderu

V menu `Síť` se zvolí `Protokol FTP - připojit kserveru` (nebo přímo: `CTRL-F`), což vyvolá FTP okno, kde se zvolí `Nové připojení` a vyplní do `Hostilel [port]` IP adresa, kterou vám ESP oználilo. (Nejčastěji 192.168.*x.y*, kde *x y* jsou konkrétní čísla). Toto nastavení si uložíme v poli `Název relace` například pod názvem "ESP32".

Pro jednorázové připojení stačí v menu `Síť` zvolit `Protokol FTP - nové připojení` (nebo přímo: `CTRL-N`) a zadat IP adresu.

---

### Použití v terminálu Linuxu

```bash
$ sudo apt-get install ftp

$ ftp 192.168.x.y
ftp> ls
...
ftp> mput *.py
...
ftp> prompt
```

---

Zdrojová knihovna 🡒 [github.com/robert-hh/FTP-Server...](https://github.com/robert-hh/FTP-Server-for-ESP8266-ESP32-and-PYBD)

Možnost běhu i v threadu a pod., zatím netestováno.

```python
import uftpd
uftpd.start()
# uftpd.start([port = 21][, verbose = level])
```

---


### Použití v projektech

Po *boot* se stiskem tlačítka `BOOT`/`EN` spustí **ftp server**, pokud tlačítko stiknuto není, bude pokračovat standardní program.

```python
from time import sleep
from machine import Pin
from utils.octopus_lib import w

btnum = 0
button = Pin(0, Pin.IN)
print("press button / CTRL+C or continue")
sleep(1)

for i in range(12):
    print("-",end="")
    btnum += button.value()
    sleep(0.2)

w()
print()

if (btnum > 0):
    print("button1 -> start FTP")
    import ftp 
    
else:
    print("button0 -> continue")
    # ...

# your code: ...
    
```

Využili jsme například v ukázce [WiFi RGB lampičky](https://github.com/octopusengine/octopuslab/blob/master/projects/webserver1/main-www-rgb.py), kde se dodatečně mohou modifikovat parametry.


Další inspirace:
https://www.youtube.com/watch?v=a7DrFqqu-78&t=369s

---

## ![hwsoc](img/mchtr.png){: style="width:28px" } Thonny

Alternativou k IDE + [Ampy](https://docs.octopuslab.cz/ampy/) (i [esptool](https://github.com/espressif/esptool)) je tento jednoduchý nástroj (program běžící na PC). V prvním vydání byl takřka nepoužitelný (až na pár tutoriálových výjimek), ale novější verze, po odstranění řady zásadních nedostatků, už běží mnohem lépe. **Pro velmi jednoduché a paměťově nenáročné pokusy** funguje podle očekávání, ale když chcete připojení k WiFi a zároveň BlueTooth, tak nejspíš narazíte. Občas i běžící program znemožní korektní start `Thonny`, a jelikož se tluče komunikace na sériovém portu, **musíte si osvojit specifické rutiny, jak to provozovat. Pomáhají opakované restarty jak ESP tak Aplikace Thony, což není úplně komfortní**, ale za zkoušku to stojí.


Nastavení v `Tools/Options/Interpreter`, by mělo být zvoleno v **Interpreter** `MicroPython (ESP32)`
a v **Port** Vaše USB připojení k ESP - například `Silicon Labs CP210x USB to UART Bridge (COM6)`.

---

![thony1](https://www.octopuslab.cz/wp-content/uploads/2020/10/thony1-1200x765.png)

Pak v levém sloupci vidíte i soubory dostupné v ESP, které můžete v hlavním okně (horní) editovat, v okně dolním pak bývá přednastaven terminál (shell).

---

Tato speciální aplikace *Thonny - Python IDE for beginners*, je ke stažení zde: 🡒 https://thonny.org/

---

Pár (anglických) odkazů (ale nebojte se použít [google](https://www.google.com/search?sxsrf=ALeKk024xpsufvjOrJskDFK_Od76pAVBvg%3A1602843167094&ei=H3KJX8OiBaSzgwe_7qaoAw&q=thony+esp32&oq=thony+esp32&gs_lcp=CgZwc3ktYWIQAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwA1AAWABgokhoAXAAeACAAQCIAQCSAQCYAQCqAQdnd3Mtd2l6yAEIwAEB&sclient=psy-ab&ved=0ahUKEwiDruuM8LjsAhWk2eAKHT-3CTUQ4dUDCA0&uact=5)):

- [randomnerdtutorials.com/getting-started-thonny-micropython](https://randomnerdtutorials.com/getting-started-thonny-micropython-python-ide-esp32-esp8266/)

- [youtube.com/Saravanan...](https://www.youtube.com/watch?v=lvmNLuHj25o)


---

## ![hwsoc](img/mchtr.png){: style="width:28px" } uPyCraft


https://randomnerdtutorials.com/uPyCraftWindows


---

## ![hwsoc](img/mchtr.png){: style="width:28px" } Mu

Další alternativní IDE:

https://codewith.mu/en/download

---
## ![hwsoc](img/mchtr.png){: style="width:28px" } EsPy


https://github.com/jungervin/EsPy


---


Připravujeme: [deployer](/deployer)

---

---
