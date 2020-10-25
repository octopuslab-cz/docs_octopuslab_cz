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
FTP Server started on  192.168.x.x # -> IP

```

---

V Total Commanderu (přes `CTRL+F` stačí zadat IP a zbytek "proklikat").

## Použití v terminálu Linuxu:

```bash
$ sudo apt-get install ftp

$ ftp 192.168.x.x
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


# Použití v projektech
Po *boot* se stiskem tlačítka `BOOT` (EN) vyvolá `fpt()`, pokud tlačítko stiknuto není, poběží standardní program.

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



---

Další inspirace:
https://www.youtube.com/watch?v=a7DrFqqu-78&t=369s

---
