# Dokumentace

Toto je hlavní část dokumentace, popisující **co a jak**.

## Knihovny (util | lib)

na esp je to takto...

---
## Jednotlivé moduly a třídy

### Led
Třída `Led` je vlastně jen jednoduchým rozšířením třídy `Pin`.
Parametr při vytváření instance je číslo pinu. `led = Led(2)`
Přidali k základní metodě `value()` dalších pár: `toggle()`, `blink()` 


Zdrojový kód je zde:
[./util/led](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/led/__init__.py)

Základní ukázka z examples:
```
from util.led import Led
from util.pinout import set_pinout

pinout = set_pinout()           # set board pinout
led = Led(pinout.BUILT_IN_LED)  # BUILT_IN_LED = 2

print("---examples/blink.py---")
# start main loop

while True:
    led.blink()
```

Nejkratší varianta:
```
from util.octopus import led
led = Led(2)

while True:
    led.blink()
```


---

### RGB

### Oled

### Disp7

### Servo

### DCnotors

### Echo

### IoT