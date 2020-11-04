# ![logo](img/logo_small.png) FTP


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

---

## Použití z Total commanderu

V menu `Síť` se zvolí `Protokol FTP - připojit kserveru` (nebo přímo: `CTRL-F`), což vyvolá FTP okno, kde se zvolí `Nové připojení` a vyplní do `Hostilel [port]` IP adresa, kterou vám ESP oználilo. (Nejčastěji 192.168.*x.y*, kde *x y* jsou konkrétní čísla). Toto nastavení si uložíme v poli `Název relace` například pod názvem "ESP32".

Pro jednorázové připojení stačí v menu `Síť` zvolit `Protokol FTP - nové připojení` (nebo přímo: `CTRL-N`) a zadat IP adresu.

---

## Použití v terminálu Linuxu

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


## Použití v projektech

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

---

Další inspirace:
https://www.youtube.com/watch?v=a7DrFqqu-78&t=369s

---
