# ![logo](img/logo_small.png) Dokumentace

Toto je hlavní část dokumentace, popisující **co a jak**.
V dalších částech, především pak oddíle WORKSHOPY a TUTORIÁLY se pak dozvíte **jak na to**.

## Knihovny (util | lib)

Jednotlivé moduly - knihovny (podprogramy, třídy) jsme rozdělili do dvou základních adresářů:

- `./lib`, kde jsou převážně knihovny třetích stran, a malé fragmenty, které mají výhodu, že se při importu v adresáři lib hledají, **Micropython** je nalezne bez udání cesty k nim.
- `./util`, (utility) moduly octopusLAB, a třídy pro práci s periferiemi.

*Uživatele vlastně nemusí zajímat, kde to je uloženo, a tak na to důraz neklademe, jen je vhodné si to pohlídat při sestavování větších projektů.*

---
## Jednotlivé moduly a třídy

Letmý úvod do objektového programování si naznačíme na tradičním *hello world* projektu: **blikání ledky**. Svítivá dioda (LED) je malá součástka,kterou snad nemusíme představovat. Takže jak je to s těmi "objekty"?

Všechno v Pythonu je **objekt**. Základní vlastnost objektů (v programu) je to, že obsahují jak data (informace), tak předpis chování – instrukce nebo metody, které s těmito daty pracují. U svítivé diody budou *data* (vlastnosti / property) *1* nebo *0* - podle toho, jestli svítí nebo nesvítí. A metoda bude třeba `blikni` nebo v případě `sviť` je to přesněji: změň hodnotu na *1* `value(1)`.

**Předpis objektu je ve třídě** `class()`. Podle tohoto předpisu vytvoříme takzvanou instanci, do závorky se dávají vstupní parametry. Na PINU 2 máme připojenu LED a chceme s ní pracovat pomocí dostupných metod pro třídu Led? Mikrokontroléru to řekneme takto:

`led = Led(2)` Je vhodné dodržet nepsané pravilo, že **třída začíná vždy velkým písmenem**. Abychom odlišili `led` od `Led`.

`led.value(1)` Syntaxe je pak: instance objektu `led` "tečka" metoda `value` "( parametry )" `(1)`, ze pouze *1*, možno i *True*.

Chceme jinou Led? Na jiném pinu? Třeba druhou na PINu 33? Vytvoříme instanci stejného objektu:
`led2 = Led(33)` > a pak jí používáme "stejně": `led2.value(1)`


Na rozdíl od proměnné: `a = 123` *Medotoda nebo funkce data získá nebo na základě parametrů zpracuje, proměnná je obsahuje*.


**Třída** je jako formička na vánoční cukroví. `Kolečko, Hvězdička, Prasátko` - to je určení tvaru. A **instance** jsou jednotlivé kousky cukroví touto formičkou vyrobená. Můžeme si vytvořit tucet hvězdiček, podobně tak si můžeme připojit více LEDek (každou na jiném PINu)

- `led1 = Led(20)`
- `led2 = Led(2)`
- `led3 = Led(33)`

rozsvícení druhé ledky je: `led2.value(1)` no a zhasnutí třetí je `led3.value(0)`

---

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Led
Třída `Led` je vlastně jen jednoduchým rozšířením třídy `Pin`.
Parametr při vytváření instance je číslo pinu. `led = Led(2)`
Přidali k základní metodě `value()` dalších pár: `toggle()`, `blink()` 


Zdrojový kód knihovny:
[./util/led](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/led/__init__.py)

Nejkratší varianta použití:
```
from util.octopus import led
led = Led(2)

while True:
    led.blink()
```

Číslo PINu v ukázce je 2, to je svítivá dioda vestavěná v **DoIt** modulech i v našem ESP32boardu. Ale pro práci s obecným modulem, kde máme možnost si nastavit, kde se Led dioda nachází, použijeme pak variantu základní ukázky z examples, kde `BUILT_IN_LED` je konstanta, ve které je číslo PINu uloženo:
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

► [pinout](#pinout)

---

### ![hwsoc](img/hwsoc.png){: style="width:28px" } RGB Led
Modul RGB je vytvořen především pro práci s ***RGB svítivými dioadmi*** typu *WS*.
Zdrojový kód knihovny: [util/rgb](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/rgb/__init__.py)


```
from util.rgb import Rgb

from util.pinout import set_pinout
pinout = set_pinout()   # set board pinout
from util.io_config import get_from_file
io_conf = get_from_file()

ws = Rgb(pinout.WS_LED_PIN,io_conf.get('ws'))

print("---examples/rgb_blink.py---")
ws.simpleTest()
```
Zdrojový kód ukázky: [examples/rgb_blink.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/rgb_blink.py)

► [pinout](#pinout)

---

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Analog
Tento modul je pro práci s analogovým vstupem pomocí DAC převodníku. Opět se jedná o rozšíření základní třídy `ADC`, kde vytvořením instance s parametrem vstupního PINu zjednodušujeme celou inicializaci na `an = Analog(33)`. Základní metodu `read()` jsme rozšířili o `get_adc_aver(num)`, kde počítáme průměr z *num* neměřených hodnot.


Zdrojový kód knihovny: [util/analog](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/analog/__init__.py)

```
from time import sleep
from util.analog import Analog
an2 = Analog(33)

while True:
    data =  an2.get_adc_aver(8)
    print(data)
    sleep(5)
```

---

### ![hwsoc](img/bits.png){: style="width:28px" } Bits
Pro práci s jednotlivými **bity**. `B1 = 0b11111001`. Bitové operace jsme si museli do Pythonu trochu doladit, aby se s nimi pracovalo lépe a intuitivně. **Používané metody:**

- `neg(B1)` pro negaci - vrací *0b00000110*
- `reverse()` obrácení poředí bitů - vrací *0b1001111*
- `get_bit(B1,1)` pro získání stavu jednoho bitu > 0
- `set_bit(B1,1)` pro nastavení stavu jednoho bitu
- `int2bin()` pomocná funkce pro převod čísla na bibární

Zdrojový kód knihovny: [util/bits](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/bits/__init__.py)



### ![hwsoc](img/hwsoc.png){: style="width:28px" } Button
Pro základní práci s tlačítky. Původně jsme používali samostatný blok s přerušením, ale knihovna pak byla přepsána tak, že využívá dekorátor `@led_button.on_press`, kterým uvedeme (odekorujeme) vlastní funkci `on_press_top_button()`, která se vyvolá vždy, když se zmáčkne tlačítko. Celá funkce pak běží na pozadí, je nablokující, a snadno i spolehlivě se dá použít i pro více tlačítek.

Zdrojový kód knihovny: [util/button](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/button/__init__.py)

```
from time import sleep
from machine import Pin
from util.button import Button

led_button = Button(0, release_value=1)
built_in_led = Pin(2, Pin.OUT)

built_in_led.on()
sleep(1)
built_in_led.off()

@led_button.on_press
def on_press_top_button():
    print("on_press_top_button")
    built_in_led.on()
    sleep(3)
    built_in_led.off()
```

► [Led](#led) | [@Dekorátor](#dekorator)

---


### ![hwsoc](img/hwsoc.png){: style="width:28px" } Disp7
Osm sedmisegmentovek s obvodem MAX na sběrnici SPI je do začátku ideální displej pro základy práce s mikrokontrolérem, sedm segmentů pro zobrazení čísel - proto `disp7`. Obdobný modul se stejným ovládáním je matice 8x8 svítivých diod, ten jsme pojmenovali `disp8`.

```
from time import sleep
from util.octopus import disp7_init

print("this is simple Micropython example | ESP32 & octopusLAB")
print()

d7 = disp7_init()	# 8 x 7segment display init

for i in range(999):
    d7.show(1000-i)
    sleep(1)
```

---
### ![hwsoc](img/hwsoc.png){: style="width:28px" } Oled
Oblíbili jsme si také malý 128x64px monochromatický OLED displej. Jeho přímé použítí vyžaduje už i inicializaci I2C a další drobnosti, proto jsme většinou využívali knihovny octopus.
Ale ukázalo se, že pro vlastní projekty je lepší umět spouštět displej i "samostatně", což je v ukázce:
[examples/oled_test.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/oled_test.py)

Zjednodušené ovládání je pak tradičně:
```
from util.octopus import oled_init
oled = oled_init()
...
```

---
### ![hwsoc](img/mchtr.png){: style="width:28px" } Servo
Modul pro práci se servem, opět vytvořením instance na daném PINu (musí být PWM).
Hlavní metodou je pak pootočení na dadaný úhel:  `set_degree()`.

Zdrojový kód knihovny: [util/servo](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/util/servo/__init__.py)

```
from time import sleep
from util.pinout import set_pinout

from util.servo import Servo
pinout = set_pinout()

# s1 = Servo(pinout.PWM1_PIN)
# s2 = Servo(pinout.PWM2_PIN)
s3 = Servo(pinout.PWM3_PIN)

angles = [0, 20, 50, 70, 90]

while True:
    for a in angles:
        s3.set_degree(a)
        sleep(1)
```

► [pinout](#pinout)

---

### ![hwsoc](img/mchtr.png){: style="width:28px" } DC Motors

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Echo

### ![hwsoc](img/wsetup.png){: style="width:28px" } IoT

### ![hwsoc](img/database.png){: style="width:28px" } Database
ESP díky paměti umožňuje bez nadsázky i základní práci s databází.
Zaměříme se na dvě základní:

- lokální `btree`
- a vzdálené `MySQL`, `Influx`

```
from util.database.btreedb import BTreeDB
db = BTreeDB("test")
db.addOne("one","1")
db.listAll()
```
---

### ![hwsoc](img/database.png){: style="width:28px" } MQTT

- MQTT - jako pub-sub
- MQTT broker - na RPi
- orchestrátor NodeJS
- využití v IoT
---

### ![hwsoc](img/bt.png){: style="width:28px" } BLE
Jelikož obecná problematika BLE (Bluetooth low energy) je poměrně obsáhlá, tak i modul BLE je dost robustní. Zahrnuje několik částí: `blesync`, `blesync_client`, `blesync_server` a samostatný modul `blesync_uart`. Každopádně funguje velmi dobře a snahou bylo, aby práce s ním byla srozumitelná a přitom umožnila využít všechny možné výhody, které BLE obecně přináší.

Následující příklad umožní z mobilní aplikace nalézt ESP zařízení jako `octopus-led-UID`, kdee UID je čás unikátního ID, které má každé ESP.
Pomocí mobilní aplikace šipkami nahoru (Up) a dolů (DOWN) pak ovládáme vestavěnou Led diodu.


```
import blesync_server
import blesync_uart.server
import util.ble.bluefruit as bf

from util.shell.terminal import getUid
uID5 = getUid(short=5)

from time import sleep
from util.led import Led
led = Led(2)


@blesync_uart.server.UARTService.on_message
def on_message(service, conn_handle, message):
    if message == bf.UP:
        led.value(1)
    if message == bf.DOWN:
        led.value(0)
    if message == bf.RIGHT:
        led.toggle()

    service.send(conn_handle, message)


_connections = []


devName = 'octopus-led-'+uID5
print("BLE ESP32 device name: " + devName)

server = blesync_server.Server(devName, blesync_uart.server.UARTService)
server.start()

```


#### ![hwsoc](img/mobplg.png){: style="width:28px" } Mobilní aplikace pro BLE
Používáme **Bluefruit connect** od společnosti Adafruit. Jeden z odkazů na [play.google.com/store/apps](https://play.google.com/store/apps/details?id=com.adafruit.bluefruit.le.connect&hl=cs)

Vytvořili jsme si pomocnou knihovnu pro "překládání" jimi definovaných kódů, která je zatím zde `./util/ble/blefruit.py`:

```
UP =   b'!B516'
DOWN = b'!B615'
LEFT = b'!B714'
RIGHT = b'!B813'
...
```

S touto knihovnou pak pracujeme takto:
```
import util.ble.bluefruit as bf
...
    if message == bf.UP:
        led.value(1)
    if message == bf.DOWN:
        led.value(0)
```


---
### ![hwsoc](img/database.png){: style="width:28px" } Config

Micropython má elegantně propacovanou práci se soubory (nahrávání a čtení) a i s `json` formátem, proto jsem toho využili pro externí konfigurační soubory. V adresáři `/config` jsou nahrány jednotlivé "jsony", které v sobě obsahují nějaké konstanty, nastavení a podobně. Proto můžeme daný projekt dynamicky konfigurovat. Využíváme to i vnastavneí PINů jednotivých zařízení `device.json` nebo pro uložení přístupů k WiFi `wifi.json`.

Zdrojový kód knihovny: [./config/__init__.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/config/__init__.py) 

Mějme ukázkový projekt **termostat**, který na základě změřené teploty pustí buď topení, nebo chlazení (ventilátor). Volitelně si můžeme v programu definovat `keys`, kde máme uloženy názvy podstatných konstant. Instanci pak vytvážíme `conf = Config("your_file", keys)`, kde "your_file" je název - nejčastěji shodný s názvem projektu. Například "termostat". Se souborem se pak dá pracovat několika metodami, například: `setup()` (interaktivní mód - používáme nejčastěji), `create_from_query()`, `set()`, `save()` ... 

```
from config import Config

keys = ["tempMax","tempMin"]
conf = Config("your_file", keys) > config/your_file.json
conf.setup()

conf.create_from_query("a=1&b=2")
conf.set("c",3)

conf.save()

```

---

### ![hwsoc](img/database.png){: style="width:28px" } pinout

Práci s PINy nám ulehčuje přednastanený pinout v configu. Podle toho, jakou máme HW platformu máme přesně svázány konstanty (názvy PINů) s jejich číselnou reprezentací:


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

► [Led](#led)

---


### ![hwsoc](img/database.png){: style="width:28px" } pubsub

Toto je geniální nástroj pro předávání parametrů v rámci projektu a to i v samostatně běžících vláknech. Pracuje na principu **publish and subscribe**.

Zdrojový kód knihovny: [./lib/pubsub.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/lib/pubsub.py)

Základ práce - jedno vlákno (nebo část programu) publikuje získané hodnoty metodou `publish` kde parametrem je "topic" a hodnota.
`pubsub.publish('value', value)`. V jednoduché ukázce jednou za vteřinu generujeme náhodná čísla, která "publikujeme".

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

