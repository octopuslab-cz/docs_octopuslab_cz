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

### BLE
---

### pubsub

Toto je geniální nástroj pro předávání parametrů v rámci projektu a to i v samostatně běžících vláknech. Pracuje na principu **publish and subscribe**.

Zdrojový kód: [./lib/pubsub.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/lib/pubsub.py)

Základ práce - jedno vlákno (nebo část programu) publikuje získané hodnoty metodou `publish` kde parametrem je "topic" a hodnota.
`pubsub.publish('value', value)`. V jedoduché ukázce jednou za vteřinu generujeme náhodná čísla, která "publikujeme".

```
from time import sleep
from os import urandom
import pubsub


print("start: ps_random.py")

while True:
    value =  int(urandom(1)[0])
    print("rnd.: ", value)
    pubsub.publish('value', value)
    sleep(1)
```

Protistrana je odebírá / naslouchá.
A může je třeba zobrazovat na displeji:

```
import pubsub
from util.octopus import disp7_init

d7 = disp7_init()  # 8 x 7segment display init


@pubsub.subscriber("value")
def display_num(value):
    d7.show(value)
```

Ukázky jsou z vybraných ukázek pro pubsub: 
[examples/pubsub](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython/examples/pubsub)
---

