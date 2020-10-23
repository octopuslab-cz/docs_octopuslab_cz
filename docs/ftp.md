# ![logo](img/logo_small.png) FTP

File transfer protocol - pro ESP8266 i ESP32.
Základ funguje i v FTP pluginu **Total Comanderu** (testováno ve Win 10).
Jednoduchá verze - věží samostatně "pouzeů FTP:

```python
>>> from utils.octopus import w
>>> w() # wifi connect

>>> import ftp
>>> ftp
FTP Server started on  192.168.x.x # -> IP

```

---

Zdrojová knihovna:
https://github.com/robert-hh/FTP-Server-for-ESP8266-ESP32-and-PYBD

Možnost i threadu a pod.

```python
import uftpd
uftpd.start()
# uftpd.start([port = 21][, verbose = level])
```


Použití v terminálu Linuxu:

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


---

Hezká ukázka použití:
https://www.youtube.com/watch?v=a7DrFqqu-78&t=369s
