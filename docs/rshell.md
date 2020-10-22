# ![logo](img/logo_small.png){: style="width:39px" } Rshell

Alternativa k [ampy](/ampy) nebo [Thony](/thony) se sériovým terminálem - běžící i na Raspberry Pi.

Ke stažení 🡒 [github.com/dhylands/rshell](https://github.com/dhylands/rshell).

## Instalace

```
sudo pip3 install rshell
```

## Připojení a spuštění


```
rshell --buffer -size=30 -p /dev/ttyUSB0
```

Výchozí je `pyboard`.


## Terminál + REPL

```
> repl
```

(exit: `CTRL+X`)

## Základní příkazy

Podbné Linuxu: ls (list) a cp (copy file).

```
> ls /pyboard
> cp myfile.py /pyboard
...
```

---