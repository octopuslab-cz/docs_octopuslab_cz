# ![logo](img/logo_small.png){: style="width:39px" } Ampy

S programem **ampy** pracujeme v příkazové řádce svého počítače.
Pozor na kolize portu - **ampy** nesmí být blokováno sériovým terminálem (screen nebo putty).


## Instalace

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

## Příkazy

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

## Hlavní příkaz put

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