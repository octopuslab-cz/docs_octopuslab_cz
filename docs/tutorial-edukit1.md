# ![logo](img/logo_small.png) Tutorial - EDU_KIT1

Předpokládáme, že již máte na svém [ESP32 Do-It](/esp32/#modul-esp32-doit-2x15) nainstalovaný [Micropython](/install). V úvodních [tutorial 1 (Python)](/tutorial1-python) a [tutorial 2 (Micropython | ESP)](/tutorial2-micropython-esp) jsme se seznámili s úplnými základy. V tomto dalším pokračování už budeme potřebovat **ESP32**. 

## • Led

Led dioda osazená na [ESP32 Do-It](/esp32/#modul-esp32-doit-2x15) modulu je na Pinu 2.

Pár ukázek - "blikáme LEDkou" hned několika způsoby:

```python
from time import sleep
from components.led import Led
led = Led(2)

# 1
>>> while True:
...   led.value(1) 
...   sleep(1)
...   led.value(0)
...   sleep(1) 

# 2
>>> while True:
...   led.value(not led.value())
...   sleep(0.5)

# 3
for _ in range(10):
…    blink(led,1000,1000)
…
```
> ctrl+C (pro přerušení běhu programu)


🡒 [referenční příručka / led](/basicdoc/#led)

---

## • RGB Led

RGB barevná dioda je na WS konektoru. Tento typ se dá připojit i na další konektor a diod WS se může řadit víc z sebou. (Až 127, na to je ale potřeba posílit napájení napětí 5V) Používáme častěji **pásek** 8-mi diod, **kroužek** 12 nebo 18, také **matice** 4x4 a spojované do většího bloku.

```python
>>> from components.rgb import Rgb 
>>> ws = Rgb(32)
>>> ws.test()                # problikne R G B cca - default 500ms
>>> ws.test(100)             # s parametrem 100ms

>>> import colors_rgb as rgb # definice barev v /lib > RED, GREEN, BLUE, ORANGE, BLACK (nesvítí)
>>> ws.color(rgb.BLUE)       # zobrazení barvy, rgb.RED/rgb.GREEN ...
>>> ws.color((128,0,0))      # parametr color je (128,0,0) 
>>> ws.rainbow_cycle()       # "projedou barvy" duhy 

# ws2 = Rgb(pin,num)    #  > číslo pinu a počet LEDek
>>> ws2 = Rgb(32,8)

>>> ws.color(5,rgb.RED)      > při LED pásku  > nastavení páté na RED 
```

🡒 [referenční příručka / rgb](/basicdoc/#rgb)

---

## • Display7

Oblíbený modul s obvodem MAX na sběrnici SPI přímo připojitelný na OCTOBUS-display sběrnici.

🡒 [referenční příručka / display7](/basicdoc/#led)

## • Servo

🡒 [referenční příručka / servo](/basicdoc/#servo)

## • Senzory

## • Možnosti rozšíření

### Mechatronika

Modul ROBOT board se dá v jedné verzi zapojení osadit "H-můstkem" L293, kterým se dají ovládat dva DC motory. Používáme "levné čínské" žluté, na 5-9V (doporučeno 7)

#### DC motory

### Expandér I2C
PCF 8 bit + výkonový budič ULN. 

---

Pro pokračování - materiály k některým Workshopům:

Práce s daty a databáze 🡒 [Workshop Python DATA](/ws-python-data)

Tvoření jednoduché hry 🡒 [Workshop EDUshield1)](/ws-edushield1)

---
# Jednoduché ukázky

## Náhodně blikajíci ledka

```python
from utils.octopus_lib import randint
from components.led import Led

led = Led(2)

# random blink
def randblink(n):
    for _ in range(n):
       delay = randint(100,500)
       print(delay)
       led.blink(delay)


>>> randblink(10)
```

