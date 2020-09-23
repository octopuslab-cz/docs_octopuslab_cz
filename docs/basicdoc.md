# ![logo](img/logo_small.png){: style="width:39px" } Dokumentace

Toto je hlavní část dokumentace, popisující **co a jak**.
V dalších částech, především pak v oddíle **Workshopy / tutoriály** se pak dozvíte **jak na to**.

---
## Moduly, třídy, funkce

!!! attention "Základ pro další pochopení (Micro)Pythonu"
    Téměř vše v Pythonu je objekt. **Objekt** je kolekce dat (proměnných) a **metod** (funkcí), které s danými daty pracují. Prototypem objektů jsou **třídy**, z nichž jsou všechny **objekty** (čísla, řetězce, funkce, moduly, metody, atp) odvozeny coby **instance**.
    Pokud vám to není jasné, trochu podrobněji se o tom rozepisujeme na samostatné stránce: [class()](/class).
    Pro správné pochopení a především v kontextu práce s hardware začátečníkům doporučujeme zmíněný odkaz alespoň letmo navštívit.

!!! note
      Toto není výuka programování – ale jen ukázky a experimenty s přihlédnutím na sadu knihoven a modulů **octopusLab** pro práci s vybraným HW.

      Pro podrobnější proniknutí do tajů programování v Pythonu doporučujeme: 

      - [naucse.python.cz](https://naucse.python.cz/)
      - [naucse.python.cz/course/mi-pyt/intro/micropython](https://naucse.python.cz/course/mi-pyt/intro/micropython/)
      - [howto.py.cz](http://howto.py.cz/index.htm)

---

### Knihovny (components | utils | lib)

Jednotlivé moduly - knihovny (podprogramy, třídy) jsme rozdělili do několika základních adresářů:

- [/components](#octopus-components), kam postupně přidáváme jednotlivé "osamostatnělé" komponenty.

- [/lib](#octopus-lib), kde jsou převážně knihovny třetích stran, a malé fragmenty, které mají výhodu, že se při importu v adresáři lib hledají, **Micropython** je nalezne bez udání cesty k nim.

- [/utils](#octopus-utils), (utility) moduly octopusLAB, a třídy pro práci s periferiemi.

*Uživatele vlastně nemusí zajímat, kde to je uloženo, a tak na to důraz neklademe, jen je vhodné si to pohlídat při sestavování větších projektů.*

!!! hint "**Zdroje programového kódu**"
    `Github` => `stable.tar` => `docs`
    
    Naší snahou je udržet v souladu zdroj z githubu: [github.com/octopusengine/octopuslab](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython), který se po *kompilaci a komprimaci* stane [stable.tar](/install/#system-download-deploy) a k němu udržovat aktuální **dokumentaci**.

---

### Adresářová strukrura na ESP32
<pre>
|-- [boot.py](#soubory-bootpy-a-mainpy)       # inicializace po startu
|      |-- [reset](#reset)
|-- [main.py](#soubory-bootpy-a-mainpy)       # hlavní soubor programu
|-- /assets       # obrázky, zvuky, tabulky
|-- [/config](#config)       # kofigurační soubory (.json)
|-- [/lib]
|      |-- [pubsub](#pubsub)
|      |-- [/blesync_uart](#BLE)
|      |-- ...
|      |-- /bmp280
|      |-- /bh1750 # i2c light sensor
|      |-- [st7735.py](#st7735) # TFT128*166 color display
|      |-- colors_rgb.py
|      |-- [hcsr04.py](#hcsr04) # ultrasonic
|      |-- [lcd](#lcd)
|      |-- ...
|
|-- [/components](#octopus-components)
|      |-- [led](#led)
|      |-- [rgb](#rgb)
|      |-- [analog](#analog)
|      |-- [button](#button)
|      |-- [display7](#display7)
|      |-- [oled](#oled)
|      |-- [buzzer](#buzzer)
|      |-- [servo](#servo)
|      |-- [dcmotors](#dcmotors)
|      |-- [plc]
|      |-- [iot](#iot)
|            | Relay | PWM | Thermometer
|
|-- [/utils](#octopus-utils)
|      |-- [octopus_lib](#octopus_lib)
|            | [I2C](#i2c) | [SPI](#spi) | [LCD](#lcd) | [RTC](#rtc)
|      |-- [WiFiConnect](#wificonnect)
|      |-- [pinout](#pinout)
|      |-- [bits](#bits)
|      |-- [transform](#transform)
|      |-- [database](#database)
|      |-- [mqtt](#mqtt)
|      |-- octopus
|      |-- ...
|      |-- BLE
|
|-- [/pinouts](/pinouts)      # nastavení pinů
|-- [/examples](/examples)      # ukázky
|      |-- /asyncio
|      |-- /ble
|      |-- /param
|      |-- /pubsub
|      |-- blink.py
|      |-- ...
|
|-- /tests
|
|-- /shell
|      |-- [shell](/upyshell)
|      |-- [editor](/upyshell/#editor)
|-- ...
</pre>

!!! warning "**Pozor**"
    **Pokud jste používali náš systém už v roce 2019**, přeinstalujte si na novou verzi. Velká část systému by vám už nefungovala. Od té doby došlo totiž k řadě změn. Především byly tři zásadní verze Micropythonu, kde se měnil i formát "kompilovaných" souborů `.mpy`, které jsou základem naší distribuce. Také se doplnilo `BLE` pro práci s **BlueTooth low energy**.
    A další změnou byla velká `refaktorizace` systému **octopus**, kde podardesář `util` byl rozdělen na `utils` (pro SW utility a hlavní framework) a `components` (kde jsou převážně knihovny pro hw komponenty a periferie.) Také `shell` byl přesunut z `util/shell` do rootu.


### Soubory boot.py a main.py

#### • boot.py 
je soubor, který se spouští jako první po bezprostřením startu nebo po resetu ESP. Zpravidla ho neměníme. Měl by obsahovat základní obecnou inicializaci. My tam máme především definice cest k modulům:

```python
# boot.py
def setup():
    import utils.setup
    utils.setup.setup()

def octopus():
    import utils.octopus
    utils.octopus.octopus()
    return utils.octopus

def reset():
    from machine import reset
    reset()

def shell():
    import shell
    shell.shell()
```

##### Reset

Pro zjednodušené použití resetu pomocí příkazu `reset()` je v `boot.py` přednastaveno:
```python
def reset():
    from machine import reset
    reset()
```

---

#### • main.py 
je hlavní soubor uživatelského programu, který budeme využívat pro své projekty. Spustí se (pokud existuje) hned po `boot.py`.
Často používáme jednoduché kopírování existujícího programu nebo ukázky (z examples) v prostředí [uPyshell](/upyshell):

```batch
$ cp examples/blink.py main.py

```

---

## OCTOPUS Components

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Led
Třída `Led` je vlastně jen jednoduchým rozšířením třídy `Pin`.
Parametr při vytváření instance je číslo pinu. `led = Led(2)`
Přidali jsme k základní metodě `value()` dalších několik metod: `toggle()`, `blink()` 


Zdrojový kód knihovny:
[./components/led](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/components/led/__init__.py)

Nejkratší varianta použití:
```python
from components.led import Led
led = Led(2)

while True:
    led.blink()
```

```python
dir(led)
['class', 'init', 'module', 'qualname', 'value', 'dict', 'pin', 'blink', 'toggle', 'state']

>>> led.pin
> Pin(2)
>>> led.state
> False
>>> led.value(1) # svítí
>>> led.state    # info o stavu
1
```

**. TAB nabídka metod:** 
Micropython má obrovskou výhodu v tom, že běží jako interpret: když uživatel napíše název proměnné nebo instance objektu, skoro všechno se o nich můžeme dozvědět. Napište `led` pak `.` (tečka) a stiskněte `TAB`:
```
led.
class       init        module      qualname
value       dict        pin         blink
toggle      state
```

Číslo PINu v ukázce je 2, to je svítivá dioda vestavěná v **DoIt** modulech i v našem ESP32boardu. Ale pro práci s obecným modulem, kde máme možnost si nastavit, kde se Led dioda nachází, použijeme pak variantu základní ukázky z examples, kde `BUILT_IN_LED` je konstanta, ve které je číslo PINu uloženo:
```python
from components.led import Led
from utils.pinout import set_pinout

pinout = set_pinout()           # set board pinout
led = Led(pinout.BUILT_IN_LED)  # BUILT_IN_LED = 2

print("---examples/blink.py---")
# start main loop

while True:
    led.blink()
```

🡒 [pinout](#pinout)

---

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Rgb
Modul pro **adresovatelnou RGB led** je vytvořen především pro práci s **RGB svítivými diodami typu WS2812b** - *proto zkratka WS*. Knihovna je pak rozšířením vestavěné `NeoPixel`. *Pro řízení klasické RGB je potřeba na každou barevnou složku samostatný PIN, což využíváme jen ojediněle.*

Zdrojový kód knihovny: [components/rgb](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/components/rgb/__init__.py)

Rozšířeno o metody:

- `color(color)` # pro jednu LED diodu, color ve formátu (R,G,B), 0-255
- `color(color, index)` # pro více, indexováno
- `simpleTest()` # proběhne R, G, B
- `wheel()` # z čísla vygenerje barvu
- `random_color()` # náhodná barva
- `rainbow_cycle()` # duha


```python
from components.rgb import Rgb
ws = Rgb(15) # BUILT_IN_RGB (WS) ROBOTboard
ws.color((255,0,0)) # R G B => RED

ws.simpleTest()
```

Obecnější s využitím set_pinout() a io_config:

```python
from components.rgb import Rgb

from utils.pinout import set_pinout
pinout = set_pinout()   # set board pinout

from utils.io_config import get_from_file
io_conf = get_from_file()

ws = Rgb(pinout.WS_LED_PIN,io_conf.get('ws'))

print("---examples/rgb_blink.py---")
ws.simpleTest()
```
Zdrojový kód ukázky: [examples/rgb_blink.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/rgb_blink.py)

🡒 [pinout](#pinout)

---

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Analog
Tento modul je pro práci s analogovým vstupem pomocí DAC převodníku. Opět se jedná o rozšíření základní třídy `ADC`, kde vytvořením instance s parametrem vstupního PINu zjednodušujeme celou inicializaci na `an = Analog(33)`. Základní metodu `read()` jsme rozšířili o `get_adc_aver(num)`, kde počítáme průměr z *num* neměřených hodnot.


Zdrojový kód knihovny: [components/analog](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/components/analog/__init__.py)

```python
from time import sleep
from components.analog import Analog

an2 = Analog(33)

while True:
    data =  an2.get_adc_aver(8)
    print(data)
    sleep(5)
```

---


### ![hwsoc](img/hwsoc.png){: style="width:28px" } Button
Pro základní práci s tlačítky. Původně jsme používali samostatný blok s přerušením, ale knihovna pak byla přepsána tak, že využívá dekorátor `@led_button.on_press`, kterým uvedeme (odekorujeme) vlastní funkci `on_press_top_button()`, která se vyvolá vždy, když se zmáčkne tlačítko. Celá funkce pak běží na pozadí, je neblokující, a snadno i spolehlivě se dá použít i pro více tlačítek.


Zdrojový kód knihovny: [components/button](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/components/button/__init__.py)


```python
from machine import Pin
from button import Button

boot_pin = Pin(0, Pin.IN)
boot_button = Button(boot_pin, release_value=1)


@boot_button.on_press
def boot_button_on_press():
    print('boot_button_on_press')


@boot_button.on_long_press
def boot_button_on_long_press():
    print('boot_button_on_long_press')


@boot_button.on_release
def boot_button_on_release():
    print('boot_button_on_release')

```

Stará verze 1.0 měla v konstruktoru číslo PINu.
Nová verze 2.0 má přímo instanci PINu.

```python
from time import sleep
from machine import Pin
from components.button import Button

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

🡒 [Led](#led) | [@Dekorátor](#dekorator)

Práce se čtyřmi tlačítky (na ESP32board) - v ukázce je zakomentována spolupráce s displejem `tft` 🡒 [st7735](#st7735)

```python
from utils.pinout import set_pinout
pinout = set_pinout()

from components.button import Button
from utils.transform import Point2D

print("buttons init>")
button_dwn = Button(34, release_value=1)
button_top = Button(36, release_value=1)
button_lef = Button(35, release_value=1)
button_rig = Button(39, release_value=1)

# size = 3
cursor = Point2D(63,81) # center TFT128*166 dispaly (mod 3)

def position(dx,dy):
    global mx # cursor, fb, tft
    cursor.x = cursor.x + dx*3
    cursor.y = cursor.y + dy*3

    print(cursor.x,cursor.y)
    # fb.fill(color565(*BLACK))
    # tft.blit_buffer(fb, 0, 0, tft.width, tft.height)
    # tft.fill_rectangle(cursor.x,cursor.y, 6, 6, color565(*RED))


@button_dwn.on_press
def on_press_dwn():
    print("down")
    position(0,1)

@button_top.on_press
def on_press_top():
    print("top")
    position(0,-1)

@button_lef.on_press
def on_press_lef():
    print("left")
    position(-1,0)

@button_rig.on_press
def on_press_rig():
    print("right")
    position(1,0)

```

---

### ![hwsoc](img/hwsoc.png){: style="width:28px" } Display7
Osm sedmisegmentovek s obvodem MAX na sběrnici `SPI` je do začátku ideální displej pro základy práce s mikrokontrolérem. Má "retro" sedm segmentů pro zobrazení čísel - proto `disp7`. Obdobný modul se shodným ovladačem je matice 8x8 svítivých diod, ten jsme pojmenovali `disp8`.

Zdrojový kód [components/display7](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython/components/display7)

Před inicializací se musí nejdříve připojit `SPI`. V následující ukázce je "dvojitě" zakomentovaná `##` obecnější metoda a použitá je `spi_init()` z knihovny `octopus_lib`.


```python
from machine import Pin, SPI
from components.display7 import Display7
## from utils.pinout import set_pinout
from utils.octopus_lib import spi_init

print("this is simple Micropython example | octopusLAB & ESP32")

print("--- spi-init ---")
## pinout = set_pinout()
## spi = SPI(1, baudrate=10000000, polarity=1, phase=0, sck=Pin(pinout.SPI_CLK_PIN), mosi=Pin(pinout.SPI_MOSI_PIN))
spi = spi_init()

ss = Pin(pinout.SPI_CS0_PIN, Pin.OUT)
#spi.deinit() #print("spi > close")

print("--- display7-init ---")
d7 = Display7(spi, ss) # 8 x 7segment display init
d7.write_to_buffer('octopus')
d7.display()

```


Nejkratší je "octopus framework" verze, kde je ale nutno mít přes `setup()` a `ds` nastavenu desku (nějčastěji ROBOTboard nebo ESP32board) a dále pomocí `ios` nastaveno `disp7` (4 | 1)

```python
from time import sleep
from utils.octopus import disp7_init

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
[examples/test_oled.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/test_oled.py)

Zjednodušené ovládání je pak tradičně:
```python
from utils.octopus import oled_init
oled = oled_init()
...
```

Základ ale vychází z knihovny `ssd1306`, která je už součástí Micropythonu:
```python
def oled_init():

    from utils.pinout import set_pinout
    from machine import Pin, I2C
    import ssd1306

    # pinout = set_pinout()
    # i2c = I2C(0, scl=Pin(pinout.I2C_SCL_PIN), sda=Pin(pinout.I2C_SDA_PIN), freq=100000)
    from utils.octopus_lib import i2c_init
    i2c = i2c_init()

    oled = ssd1306.SSD1306_I2C(128, 64, i2c, 0x3c)
    return oled

oled = oled_init()
oled.text("octopusLAB", 0, 0)
oled.show()

oled.draw_image() # default /assets/octopus_image.pbm
oled.invert(0)
...
```

```python
>>> from assets.icons9x9 import ICON_clr, ICON_heart
>>> oled.draw_icon(ICON_heart,115,15) 

>>> def heartBeat()               
...    oled.draw_icon(ICON_heart,115,15)
...    sleep(1)
...    oled.draw_icon(ICON_clr,115,15)
...    sleep(1)
...
```

---


### ![hwsoc](img/hwsoc.png){: style="width:28px" } Buzzer

Pasivní piezo "pípák" slouží pro akustická upozornění, ale umí přehrát i velmi jednoduché "retro" melodie.

Zdrojový kód knihovny: [components/buzzer](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython/components/buzzer)

Základ práce:
```python
from components.buzzer import Buzzer
piezzo = Buzzer(33)
piezzo.beep()
```

Doplňující třída `melody` jako přidání další části kódu:
```python
from components.buzzer.melody import jingle1
piezzo.play_melody(jingle1)
```


---


### ![hwsoc](img/mchtr.png){: style="width:28px" } Servo
Modul pro práci se servem, opět vytvořením instance na daném PINu (musí být PWM).
Hlavní metodou je pak pootočení na daný úhel:  `set_degree()`.

Zdrojový kód knihovny: [components/servo](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/components/servo/__init__.py)

```python
from time import sleep
from utils.pinout import set_pinout

from components.servo import Servo
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

🡒 [pinout](#pinout)

---

### ![hwsoc](img/mchtr.png){: style="width:28px" } DCmotors

Zdrojový kód knihovny: [components/dcmotors](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/components/dcmotors/__init__.py)

```python
from utils.pinout import set_pinout
pinout = set_pinout()

from components.dcmotors import Motor, Steering

motor_r = Motor(pinout.MOTOR_1A, pinout.MOTOR_2A, pinout.MOTOR_12EN)
motor_l = Motor(pinout.MOTOR_3A, pinout.MOTOR_4A, pinout.MOTOR_34EN)
steering = Steering(motor_l, motor_r)
speed = 800

steering.center(0)
steering.center(-speed)
steering.right(speed)
steering.left(speed)
```

---


### ![hwsoc](img/wsetup.png){: style="width:28px" } IoT

Třída, která původně sloužila jako modul pro IoTboard, ale samostatná zahrnuje relé a PWM MOS-FET řízení.

Zdrojový kód knihovny: [components/iot](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython/components/iot)

Ukázka: 
```python
from components.iot import Relay
re1 = Relay() # default IoTboard pin 
re1.value(1)
re2 = Relay(26)



from components.iot import Pwm
pwm_led = Pwm(33)
pwm_led.duty(300)



from components.iot import Thermometer
tt = Thermometer(32) # DEV1 (ROBOTboard)
tx = tt.ds.scan()
tt.get_temp() # default index 0 > first sensor
tt.get_temp(tx[0])
```

---

## OCTOPUS Utils

### ![hwsoc](img/bits.png){: style="width:28px" } WiFiConnect

Hlavní výhodou našeho rozšíření pro připojení k WiFi je používání uloženého nastavení (v `config/wifi.json`).
Nastavení WiFi se provádí pomocí [setup()](../install/#setup-nastaveni-systemu)

```python
from utils.wifi_connect import WiFiConnect

net = WiFiConnect()
net.connect()
```

```python
if not net.isconnected()
    # hard reconect
    net.sta_if.disconnect()
    net.connect()
```

V případě "závažnějšího problému" s připojením někdy pomůže až "tvrdý" [reset](#reset).
```python
# hard reset
reset()
```

---


### ![hwsoc](img/bits.png){: style="width:28px" } Bits
Pro práci s jednotlivými **bity**. `B1 = 0b11111001`. Bitové operace jsme si museli do Pythonu trochu doladit, aby se s nimi pracovalo lépe a intuitivně. **Používané metody:**

- `neg(B1)` pro negaci - vrací *0b00000110*
- `reverse()` obrácení pořadí bitů - vrací *0b1001111*
- `get_bit(B1,1)` pro získání stavu jednoho bitu > 0
- `set_bit(B1,1)` pro nastavení stavu jednoho bitu
- `int2bin()` pomocná funkce pro převod čísla na binární

Zdrojový kód knihovny: [utils/bits](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/utils/bits/__init__.py)

```python
from components.bits import neg
B1 = 0b11111001
neg(B1) # > 0b00000110

```

---

### ![hwsoc](img/mchtr.png){: style="width:28px" } Transform

Pomocné funkce pro mechatroniku, zaměřené na transformace souřadnicových systémů a základy inversní kinematiky.

- `Point2D()` class p2 = (x,y) | p2.x, p2.y
- `distance2D(p1, p2, rr = 3)` vzdálenost dvou bodů v rovině
-  *využívá se round - zaokrouhlení na určitý počet míst:* `rr` = 3 
- `polar2cart(r, alfa, rr = 3)`
- `cart2polar(point)`
- `def cosangle(opp, adj1, adj2)`
- `move_2d_line(p_start, p_stop, steps = 300, max_dist = 100)`
- `invkin2_1(point2d, rr = 6)` inversní kinematika 1
- `invkin2(point2d, angleMode=DEGREES)`
- `Point3D()` class p3 = [x,y,z]
- `invkin3(point3d, angleMode=DEGREES)`
- `distance3()` vzdálenost dvou bodů v prostoru
- ...

```python
from utils.transform import Point2D, polar2cart, cosangle
p1 = Point2D(1,3)
print(p1)   # (1,3)
print(p1.x) # 1
print(p1.y) # 3
p1.x, p1.y = polar2cart(10, 0)
print(p1)
...
```


```python
from utils.transform import move_servo2, cosangle

...
def move_servo2(p1, p2, delay = delay):
    steps = move_2d_line(p1, p2)
    for step in steps:
        alfa = cosangle(step[0], dist, dist)[0]
        beta = cosangle(step[1], dist, dist)[0]
        print(step, alfa, beta)

        s1.set_degree(alfa)
        s2.set_degree(beta)
        sleep_ms(delay)

p1 = 0, 0 # strart point
p2 = 50, 50 # stop point
move_servo2(p1, p2)

```
Více plánujeme v samostatné sekci [inversní kinematika](/inv_kinematics)

---


### ![hwsoc](img/database.png){: style="width:28px" } Database
ESP díky paměti umožňuje bez nadsázky i základní práci s databází.
Zaměříme se na dvě základní: lokální `btree` a vzdálené `MySQL`, `InfluxDB`.

```python
from utils.database.btreedb import BTreeDB
db = BTreeDB("test")
db.addOne("one","1")
db.listAll()
```

Zvídavějším doporučujeme odkaz na práci s daty a databáze 🡒 [Workshop Python DATA](/ws-python-data)

---

### ![hwsoc](img/database.png){: style="width:28px" } MQTT

- MQTT - jako pub-sub
- MQTT broker - na RPi
- orchestrátor NodeJS
- využití v IoT
---

### ![hwsoc](img/database.png){: style="width:28px" } InfluxDB

Pro zobrazování dat v **Grafaně** průběžně posíláme údaje na vzdálený server, který je ukládá do databáze **InfluxDB**.
Jednoduchý příklad jednorázového odeslání jedné hodnoty (**timestamp** - datum a čas se přidají při ukládání automaticky):

```python
from utils.database.influxdb import InfluxDB

influx = InfluxDB("https://your.server.com/grafana/influx/user...", "user_db", "i_usr", "i_psw", "i_measurement")

value = 25.6  # zde je treba cist hodnotu z nejakeho senzoru, napr. teplomeru
influx.write(temperature=value)
...
```

Metoda `write` musí dostat pojmenované parametry (key word arguments - tzv. kwargs), které se v Influxu použijí, jako jednotlivé fieldy. V příkladu nahoře je to `temperature`, kam ukládáme hodnotu ze sensoru.

Funkční ukázka např: [examples/influxdb_disp7_therm.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/influxdb_disp7_therm.py)

---

Abychom mohli použít identický program s minimem změn,
využijeme konfigurační soubor, načteme pomocí `fromconfig()`. A také nechceme mít **přístupové údaje ve zdrojovém kódu**! 

```python
from utils.database.influxdb import InfluxDB

influx = InfluxDB.fromconfig()

temp = ...
influx.write(temperature=temp)
```

`fromconfig()` bere volitelně jako první parametr, název konfiguračního souboru, default je `"influxdb"`, tedy soubor `config/influxdb.json`.

Příklad obsahu je:

```json
{"influxdb_url": "https://parallelgarden.surikata.info:8086", "influxdb_pass": "heslo", "influxdb_name": "nazev_db", "influxdb_user": "uzivatel", "influxdb_measurement": "meteo", "influxdb_tags": {"location": "balkon"}}
```

Více o vytváření a editaci konfiguračních souborů 🡒 [Config](#config)

---


## OCTOPUS Lib

### LCD

Knihovna třetí strany pro ovládání dvou nebo čtyř-řádkového LCD displeje připojeného k `i2c` expandéru, byla původně určena pro starší ESP8266, ale funguje nám bez úprav i pro ESP32 (protože komunikační protokol na i2c se nemění).

Základem v nastavení je: počet řádků `rows` - 1/2/4, a počet "sloupců" `col` odpovídá počtu znaků na řádku.
Ukauka pro displej `2x16`: 

```python
# from machine import I2C , Pin
# i = I2C(scl=Pin(22), sda=Pin(21), freq=100000)
from utils.octopus_lib import i2c_init
i2c = i2c_init()
# i2c.scan() # > [39]
from lib.esp8266_i2c_lcd import I2cLcd
lcd = I2cLcd(i2c, 39, 2, 16) # addr, rows, col
lcd.putstr("octopusLab") # write text
...
```

V našem podadresáři `/assets` máme v souboru `lcd_chars.py` tabulky některých znaků pro LCD:

```python
import assets.lcd_chars as ch

from utils.octopus import lcd2_init
lcd = lcd2_init()

lcd.custom_char(0, ch.happy)
lcd.putchar(chr(0))

lcd.custom_char(1, ch.clock)
lcd.putchar(chr(1))

...
```
---


### St7735

Barevný displej TFT 128x160, který ale vyžaduje při práci s Micropythonem větší paměť.

Doporučené připojení k `ESP32board`:
```
Display | ESP32board
------------------------
1-RST   | PWM2     (16)
2-CS    | SCE0     (5)
3-D/C   | PWM1     (17)
4-DIN   | SPI_MOSI
5-CLK   | SPI_CLK
6-UCC   | 5V
7-BL    | 3V3
8-GND   | GND
```


```python
from machine import Pin, SPI, SDCard
from time import sleep, sleep_ms

from utils.pinout import set_pinout
pinout = set_pinout()

import framebuf
from lib import st7735
from lib.rgb import color565

print("spi.TFT 128x160 init >")
spi = SPI(1, baudrate=10000000, polarity=1, phase=0, sck=Pin(pinout.SPI_CLK_PIN), mosi=Pin(pinout.SPI_MOSI_PIN))
ss = Pin(pinout.SPI_CS0_PIN, Pin.OUT)

rst = Pin(16, Pin.OUT) #PWM2 (16) / DEv3(27)
cs = Pin(5, Pin.OUT)   #SCE0 (5)
dc = Pin(26, Pin.OUT)  #PWM1 (17) /  IO26

tft = st7735.ST7735R(spi, cs = cs, dc = dc, rst = rst)

print("spi.TFT framebufer >")
fb = framebuf.FrameBuffer(bytearray(tft.width*tft.height*2), tft.width, tft.height, framebuf.RGB565)
fbp = fb.pixel

fb.line(128,0,0,166,color565(0,255,0))
tft.blit_buffer(fb, 0, 0, tft.width, tft.height)
...
```

🡒 [pinout](#pinout)

[examples/test_tft128x160.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/test_tft128x160.py)

---


### hcsr04

Ultrazvukový měřič vzdálenosti.

```python
from time import sleep
from util.pinout import set_pinout

pinout = set_pinout()

from hcsr04 import HCSR04
print("ulrasonic distance sensor")
echo = HCSR04(trigger_pin=pinout.PWM2_PIN, echo_pin=pinout.PWM1_PIN)

while True:
    echo_cm = echo.distance_cm()
    print(echo_cm)
    sleep(1)

```

🡒 [pinout](#pinout)

[examples/ultrasonic.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/ultrasonic.py)

---


### ![hwsoc](img/database.png){: style="width:28px" } pubsub

Nástroj pro předávání hodnot mezi nezávislými komponenty v rámci projektu a to i v samostatně běžících vláknech. Pracuje na principu **publish and subscribe**. Fork z [basecue/micropython-pubsub](https://github.com/basecue/micropython-pubsub).

Zdrojový kód knihovny: [./lib/pubsub.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/lib/pubsub.py)

Základ práce: jedno vlákno (nebo část programu) publikuje získané hodnoty metodou `publish` kde parametrem je `topic` a hodnota `value`. Například`pubsub.publish('topic', value)`. (value může být libovolný objekt). V jednoduché ukázce  jednou za vteřinu generujeme náhodná čísla, která "publikujeme". (pozor, používáme `while True:` - je to blokující, lepší je použít `timer`)


```python
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

```python
import pubsub
from utils.octopus import disp7_init

d7 = disp7_init()  # 8 x 7segment display init


@pubsub.subscriber("value")
def display_num(value):
    d7.show(value)
```

🡒 [Disp7](#disp7)

Ukázky jsou z vybraných příkladů pro pubsub: 
[examples/pubsub](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython/examples/pubsub)

---


### ![hwsoc](img/bt.png){: style="width:28px" } BLE
Jelikož obecná problematika BLE (Bluetooth low energy) je poměrně obsáhlá, tak i modul BLE je dost robustní. Zahrnuje několik částí: `blesync`, `blesync_client`, `blesync_server` a samostatný modul `blesync_uart`. Každopádně funguje velmi dobře a snahou bylo, aby práce s ním byla srozumitelná a přitom umožnila využít všechny možné výhody, které BLE obecně přináší.
Projekt má svůj vlastní repozitář: [/blesync](https://github.com/blesync).

Následující příklad umožní z mobilní aplikace nalézt ESP zařízení jako `octopus-led-UID`, kde UID je čás unikátního ID, které má každé ESP.
Pomocí mobilní aplikace šipkami nahoru (Up) a dolů (DOWN) pak ovládáme vestavěnou Led diodu.


```python
import blesync_server
import blesync_uart.server
import utils.ble.bluefruit as bf

from shell.terminal import getUid
uID5 = getUid(short=5)

from time import sleep
from components.led import Led
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

Vytvořili jsme si pomocnou knihovnu pro "překládání" jimi definovaných kódů, která je zatím zde `./utils/ble/blefruit.py`:

```python
UP =   b'!B516'
DOWN = b'!B615'
LEFT = b'!B714'
RIGHT = b'!B813'
...
```

S touto knihovnou pak pracujeme takto:
```python
import utils.ble.bluefruit as bf
...
    if message == bf.UP:
        led.value(1)
    if message == bf.DOWN:
        led.value(0)
```

---

## Ostatní podpůrné moduly

### ![hwsoc](img/database.png){: style="width:28px" } Config

Micropython má elegantně propacovanou práci se soubory (nahrávání a čtení) a i s `json` formátem, proto jsme toho využili pro externí konfigurační soubory. V adresáři `/config` jsou nahrány jednotlivé "jsony", které v sobě obsahují nějaké konstanty, nastavení a podobně. Proto můžeme daný projekt dynamicky konfigurovat. Využíváme to i v nastavení PINů jednotivých zařízení `device.json` nebo pro uložení přístupů k WiFi `wifi.json`.

Zdrojový kód knihovny: [./config/__init__.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/config/__init__.py)

#### Jednotlivé **metody** pro základní varianty používání:

1) Vytvořením pomocí konstruktoru: `myConfig = Config("myConfigFile",keys)`        
Vyžaduje předefinici klíčových "metrik": `keys = ["tempMax","tempMin"]`

- `setup()`
- `print()` # for keys

Mějme ukázkový projekt **termostat**, který na základě změřené teploty pustí buď topení, nebo chlazení (ventilátor). Volitelně si můžeme v programu definovat `keys`, kde máme uloženy názvy podstatných konstant. Instanci pak vytváříme `conf = Config("your_file", keys)`, kde "your_file" je název - nejčastěji shodný s názvem projektu. Například "termostat". Se souborem se pak dá pracovat několika metodami, například: `setup()` (interaktivní mód - používáme nejčastěji), `create_from_query()`, `set()`, `save()` ... 

```python
>>> from config import Config
>>> keys = ["tempMax","tempMin"]
>>> conf = Config("termostat", keys) # > config/termostat.json
>>> conf.setup()

==================================================
        S E T U P - config/termostat.json
==================================================
[ 1] -          tempMax -
[ 2] -          tempMin -
[q] - Quit from json setup
==================================================
select:

```

Vidíme, že nastavení `config` je snadné. Stačí vyplnit nebo modifikovat interaktivní tabulku.


2) Vytvořením pomocí konstruktoru bez `keys`: `myConfig = Config("myConfigFile")`

- `print_all()`
- `get("key")`
- `set("key",value)`
- `create_from_query("a=1&b=2")` # key1 = "a", value1 = 1 ...
- `save()`


```python

# vytvoření konfigu: a = 1, b = 2
>>> conf = Config("your_config")
>>> conf.create_from_query("a=1&b=2")
{'a': '1', 'b': '2'}
>>> conf.set("c",3)
>>> conf.save()
Writing new config item to file config/your_config.json
>>> conf.print_all()
-----------------------------------------
                  a - 1
                  c - 3
                  b - 2
-----------------------------------------
>>>
```

---

Ve svém programu pak `config` použijeme následovně:

```python
from config import Config
conf = Config("your_config")
a =  conf.get("a") # 1
b =  conf.get("b") # 2

```

### ![hwsoc](img/database.png){: style="width:28px" } octopus_lib

#### I2C
`i2c_init()`

```python
>>> from utils.octopus_lib import i2c_init
>>> i2c = i2c_init()
>>> i2c.scan()
```

```python
# I2C address:
OLED_ADDR = 0x3c
LCD_ADDR = 0x27
bhLight = 0x23
bh2Light = 0x5c
tslLight = 0x39

# PCF8574           PCF8574A
# AAA - hex (dec)
# 210
# 000 - 0x20 (32)   0x38 (56)
# 001 - 0x21 (33) * 0x39 (57)
# 010 - 0x22 (34)   0x3A (58)
# 011 - 0x23 (35) * 0x3B (59)
# 100 - 0x24 (36)   0x3C (60)
# 101 - 0x25 (37)   0x3D (61)
# 110 - 0x26 (38)   0x3E (62)
# 111 - 0x27 (39)   0x3F (63)
# * ROBOTboard

```


#### SPI
`spi_init()`

```python
from machine import Pin, SPI
from components.display7 import Display7
## from utils.pinout import set_pinout
from utils.octopus_lib import spi_init

print("--- spi-init ---")
## spi = SPI(1, baudrate=10000000, polarity=1, phase=0, sck=Pin(pinout.SPI_CLK_PIN), mosi=Pin(pinout.SPI_MOSI_PIN))
spi = spi_init()

ss = Pin(pinout.SPI_CS0_PIN, Pin.OUT)
#spi.deinit() #print("spi > close")
...
```


#### RTC

Modul reálného času má Micropython v poslední verzi doplněn i o ntp modulem `ntptime`.

Co se skrývá v ↠ [ntptime](https://github.com/micropython/micropython/blob/master/ports/esp8266/modules/ntptime.py)?
Především metoda `settime()`, pomocí které získáme přesný čas ze serveru `pool.ntp.org`.


```python
from ntptime import settime
from machine import RTC
from utils.octopus import w
from utils.octopus_lib import get_hhmm, setlocal

rtc = RTC()
w() # připojení k internetu
settime()
print(get_hhmm(rtc))

# + 2 h.
setlocal(2)
print(get_hhmm(rtc))

```

Zdroj ukázky 🡒 [test_rtc_ntp.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/test_rtc_ntp.py)

---

### ![hwsoc](img/database.png){: style="width:28px" } pinout

Práci s PINy nám ulehčuje přednastanený **pinout**, který je uložený v konfiguračním souboru. Konfigurační soubory pro jednotlivé hw moduly jsou v samostatném adresáři `/pinouts`. Podle toho, jakou máme HW platformu, máme přesně svázány konstanty (čísla PINů) s jejich názvy.
Vybrané soubory zapojení pinů jsou na samostatné stránce 🡒 [pinouts](/pinouts).

Zdrojový kód knihovny: 🡒 [utils/pinout](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/utils/pinout.py)

**Princip je jednoduchý:**
máme definovány číselné konstanty (v programu se neměnící čísla), například pro vestavěnou Led diodu: `BUILT_IN_LED = const(číslo)`. **Číslo** je zde číslo PINu a může se lišit podle dané desky (deska je nastavena příkazem `>>> setup()`).
Tato konstanta je uložena v souborech `pinouts/file_name`. Pro ROBOTboart je to `2`, takže v souboru pro definici pinů najdete řádek `BUILT_IN_LED = const(2)`. Výchozí společné piny jsou v [/pinouts/olab_esp32_base.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/pinouts/olab_esp32_base.py) a ROBOTboard je přebírá.


Jak se s modulem pinout pracuje? Můžete si zkusit z terminálu Micropythonu: `>>>`

```python
>>> from utils.pinout import set_pinout
>>> pinout = set_pinout()
```
A už máme dostupné piny na `pinout.NAZEV_PINU`, dají se zjistit i osatní PINy, po `pinout` tečka `TAB`:

```python
>>> pinout.
__class__       __name__        const           __file__
WS_LED_PIN      ONE_WIRE_PIN    PIEZZO_PIN      MOTOR_12EN
MOTOR_34EN      MOTOR_1A        MOTOR_2A        MOTOR_3A
MOTOR_4A        ANALOG_PIN      PWM1_PIN        PWM2_PIN
PWM3_PIN        SERVO_MIN       SERVO_MAX       I39_PIN
DEV1_PIN        DEV2_PIN        BUILT_IN_LED    HALL_SENSOR
I2C_SCL_PIN     I2C_SDA_PIN     SPI_CLK_PIN     SPI_MISO_PIN
SPI_MOSI_PIN    SPI_CS0_PIN     RXD0            TXD0
BUTT1_PIN       BUTT2_PIN       BUTT3_PIN       DEV3_PIN
...

>>> pinout.BUILT_IN_LED
2
```
Vidíme, že pro `BUILT_IN_LED` nám "dohledá" číslo deklarované `2`, takže se to dá použít:


```python
led = Led(pinout.BUILT_IN_LED)      # BUILT_IN_LED = 2
```
je shodné s:
```python
led = Led(2)
```
ale číslo `2` si nemusíme pamatovat, navíc u různých modulů se může lišit.

*Celá ukázka pro blikání vestavěné Ledky na různých modulech - může být na PINu `2` nebo také na `15`... nebo úplně jiném.
A my toto číslo při správné konfiguraci modulu (desky) nemusíme řešit a k vestavěné Ledce přistupujeme názvem PINu: `BUILT_IN_LED`.*

```python
from components.led import Led
from utils.pinout import set_pinout   # import library

pinout = set_pinout()   # set board pinout

led = Led(pinout.BUILT_IN_LED)

# start main loop
while True:
    led.blink()
```
🡒 [Led](#led)

---


### ![hwsoc](img/database.png){: style="width:28px" } Dekorátor

Možná jste si v některých našich ukázkách všimnuli speciálního použití `@` před definicí funkce, například v 🡒 [pubsub](#pubsub)
```python
@pubsub.subscriber("value")
def display_num(value):
    d7.show(value)
```


nebo v 🡒 [button](#button)
```python
@led_button.on_press
def on_press_top_button():
    print("on_press_top_button")
    built_in_led.on()
```


Dekorátor v Pythonu je **funkce**, která dostane jeden argument (funkci) a vrátí jednu hodnotu - opět funkci, která je modifikovanou verzí funkce původní. *Původní funkce ja takzvaně "odekorovaná".*

Použití dekorátorů velmi zjednoduší a zpřehlení váš kód. Používá se na registraci, modifikaci a podobně. 


```python
@dekorator
def funkce():
    pass

# je stejné jako:

def funkce():
    pass
funkce = dekorator(funkce)
```

### Zrychlení práce procesoru

- [speed_python](http://docs.micropython.org/en/v1.9.3/pyboard/reference/speed_python.html)

---

## Web server - IDE - jednoduché ovládání

Jsme vyčlenili samostatně - zatím zde: [micropython-web-ide](https://www.octopuslab.cz/micropython-web-ide/)

### Web server

ESP32 má dostatečný výkon, aby na něm mohl běžet jednoduchý **webový server** (server s jednoduchými "html" stránkami, k kterému se v lokální síti připojíme přes IP ESPčka)

```python
>>> from utils.octopus import w, web_server
>>> w()
>>> web_server() 

```
