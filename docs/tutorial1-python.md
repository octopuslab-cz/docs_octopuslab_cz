# ![logo](img/logo_small.png) Tutorial 1


## Pár prvních pokusů s Micropythonem

Většina ukázek z tohoto tutoriálu bude fungovat i na běžném počítači při použití Pythonu. Cílem je pochopení a procvičení elementárních základů. Pokračování, kde už využijeme ESP32 s Micropythonem, je na samostatné stránce: [Tutorial2](/tutorial2-micropython-esp). Pro ten už si ale musíte [nainstalovat](/install) Micropython na ESP.

---

### CTRL-C

Po restartu nám ESP32 posílá do našeho počítače na terminál první zprávy.
Zeleně jsou systémové informace, které nás v tuto chvíli nezajímají.
Po stisknutí **CTRL-C** se přeruší běh programu a uvidíme verzi Micropythonu:
```
MicroPython v1.11-180-g8f55a8fab-dirty-build-octopusLAB on 2019-07-29; 
module with ESP32                                                                                                             
Type "help()" for more information.
```

!!! hint "Výčet klávesových zkratek pro práci s REPLem"

    - CTRL-A  (on a blank line, enter raw REPL mode)
    - CTRL-B  (on a blank line, enter normal REPL mode)
    - **CTRL-C**  (interrupt a running program)
    - **CTRL-D**  (on a blank line, do a soft reset of the board)
    - CTRL-E  (on a blank line, enter paste mode)

    Nejčastěji potřebujeme CTRL-C (zastavení programu) nebo CTRL-D (reset)


### >>>

`>>>` toto je takzvaný "prompt", terminálová výzva, abychom tam něco napsali - příkaz nebo "posloupnost příkazů".

```
>>> a = 123      # do proměnné se uložila hodnota (číslo 123)
>>> a            # vytiskne / zobrazí hodnotu proměnné 
123              # nebo print(a) 
                
>>> a + 10
133              # zobrazí vypočtenou hodnotu (jako kalkulačka)
```

*Python zde běží v takzvaném interaktivním módu. Po každém vložení řádku (nebo bloku řádků) se okamžitě napsaný příkaz (nebo skupina příkazů) provede a čeká na další výzvu zobrazením `>>>`. 
Je to výhodné pro testování jednotlivých příkazů, pro výuku nebo průběžné modifikace.*

---

### Math

Někdy chceme použít i složitější matematické výrazy, než je 
`+` sčítání | `-` odčítání | `*` násobení | `/` dělení

Pro další matematické funkce a konstanty použijeme knihovnu `math`.

```
>>> import math        # knihovnu importujeme, až když ji potřebujeme,
                       # jinak nám zbytečně blokuje operační paměť

>>> math.log10(1000)   # funkce logaritmus o základu deset je jednou z metod knihovny math
3.0

>>> math.pi            # konstanta Pí (není to metoda!)
3.141593               # a počet desetinných míst je omezený
```

!!! note
      Toto není výuka programování – ale jen ukázky a experimenty s přihlédnutím na sadu knihoven a modulů **octopusLab** pro práci s vybraným hardware. Pro podrobnější proniknutí do tajů programování v Pythonu doporučujeme: 

      - [naucse.python.cz](https://naucse.python.cz/)
      - [naucse.python.cz/course/mi-pyt/intro/micropython](https://naucse.python.cz/course/mi-pyt/intro/micropython/)
      - [howto.py.cz](http://howto.py.cz/index.htm)


```
>>> hodnota = 123
>>> print(hodnota)      # > 123 | vypíše obsah proměnné s názvem hodnota (korektně)
>>> print(math.pi)      # > 3.141593
```

### Help

Zkuste si napsat `help()`

```
>>> help()
Welcome to MicroPython on the ESP32!

For generic online docs please visit http://docs.micropython.org/

For access to the hardware use the 'machine' module:

import machine
pin12 = machine.Pin(12, machine.Pin.OUT)
pin12.value(1)
pin13 = machine.Pin(13, machine.Pin.IN, machine.Pin.PULL_UP)
print(pin13.value())
i2c = machine.I2C(scl=machine.Pin(21), sda=machine.Pin(22))
i2c.scan()
i2c.writeto(addr, b'1234')
i2c.readfrom(addr, 4)

Basic WiFi configuration:

import network
sta_if = network.WLAN(network.STA_IF); sta_if.active(True)
sta_if.scan()                             # Scan for available access points
sta_if.connect("<AP_name>", "<password>") # Connect to an AP
sta_if.isconnected()                      # Check for successful connection

Control commands:
  CTRL-A        -- on a blank line, enter raw REPL mode
  CTRL-B        -- on a blank line, enter normal REPL mode
  CTRL-C        -- interrupt a running program
  CTRL-D        -- on a blank line, do a soft reset of the board
  CTRL-E        -- on a blank line, enter paste mode

For further help on a specific object, type help(obj)
For a list of available modules, type help('modules')
```

### Výpis dostupných modulů
```
>>> help("modules")
```
Pokud vás zajímá, které "moduly" jsou aktuálně v Micropythonu dostupné 
*(Verze 1.12-599)*:
```
__main__          inisetup          ubinascii         urandom
_boot             machine           ubluetooth        ure
_onewire          math              ucollections      urequests
_thread           micropython       ucryptolib        uselect
_uasyncio         neopixel          uctypes           usocket
_webrepl          network           uerrno            ussl
apa106            ntptime           uhashlib          ustruct
btree             onewire           uhashlib          utils/octopus_initial
builtins          ssd1306           uheapq            utils/wifi_connect
cmath             sys               uio               utime
dht               uarray            ujson             utimeq
ds18x20           uasyncio/__init__ umqtt/robust      uwebsocket
esp               uasyncio/core     umqtt/simple      uzlib
esp32             uasyncio/event    uos               webrepl
flashbdev         uasyncio/funcs    upip              webrepl_setup
framebuf          uasyncio/lock     upip_utarfile     websocket_helper
gc                uasyncio/stream   upysh
Plus any modules on the filesystem
```

A po importu se můžete dotázat na každý modul samostatně (podobně i `math.` + TAB):
```
>>> import math
>>> help(math)
object <module 'math'> is of type module
  __name__ -- math
  e -- 2.718282
  pi -- 3.141593
  sqrt -- <function>
  pow -- <function>
  exp -- <function>
  expm1 -- <function>
  log -- <function>
  log2 -- <function>
  log10 -- <function>
  cosh -- <function>
  sinh -- <function>
  tanh -- <function>
  acosh -- <function>
  asinh -- <function>
  atanh -- <function>
  cos -- <function>
  sin -- <function>
...
```

!!! hint "**Python je jednoduchý**"

    - logické členění se provádí pomocí striktního odsazování bloků
    - pozor na závorky u metod a funkcí `print("řetězec")` a uvozovky pro takzvané *řetězce (shluky písmen, co nejsou číslo)*
    - pozor na dvojtečku za deklarací funkce, cyklu nebo podmínky: def funkce(parametr)`:`

---

### Blok programu na více řádků a odsazování

Víceřádkové "dočasné definice vlastních funkcí" se provádí pomocí `def název(parametry):` - odsazení za nás udělá REPL `...` nezapomenout na dvojtečku!

```
>>> def suma(x, y):
...    return x + y

>>> suma (1, 2)
3
```

!!! error "**Odsazování**"

    - zmínili jsme už, že logické členění se provádí pomocí striktního **odsazování** bloků
    - při psaní jednořádkových pokusů v terminálu (po `>>>`) Vám po řádku končícím dvojtečkou Python sám předvyplní 
    symbolické tři tečky `...` jako odsazení *viz předchozí ukázka*, ale pozor! Při psaní programu do souboru se odsazuje pomocí mezer 
    (doporučeno 3 nebo 4) nebo TABulátorem. 
    A musí to být stále stejně! Kombinace mezer a TAB je také **syntaktická chyba**.

*Píšeme-li postupně řádek po řádku - příkaz po příkaze, odsazování není potřeba. Až v definování procedur, v cyklech nebo podmínkách - tedy "po dvojtečce" `:`*

---

### Čekací prodlevy
- program bude pokračovat až po uplynutí dané doby:
```
from time import sleep, sleep_ms # importujeme jen potřebné knihovny

sleep(1)           # 1 sekunda pauza
sleep_ms(100)      # 100 milisekund pauza
sleep_us(50)       # 50 mikrosekund pauza
```

### Generátor náhodných čísel

Občas se nám v programu hodí vygenerovat **pseudonáhodné** číslo (pro testování, jednoduché hry nebo speciální efekty).

```python
>>> from os import urandom
>>> urandom(1)[0]
42
```


### Smyčky | Cykly 

```python
i = 0
while (i < 3):
    print(i)
    i += 1
```
Vypíše:
```
1
2
3
```

S "dospělým" Pythonem si můžete vyzkoušet více ↠ [naucse.python/cykly](https://naucse.python.cz/course/pyladies/sessions/loops/)

### Podmínky

```python
from os import urandom
num = urandom(1)[0]
if (num < 100):
   print("number {0} < 100".format(num))
```

Povšimněte si konstrukce `format`, kdy můžeme do řetězce vložit proměnnou, aniž bychom ho postupně "slepovali".

S "dospělým" Pythonem si můžete vyzkoušet více ↠ [naucse.python/podminky](https://naucse.python.cz/course/pyladies/beginners/comparisons/)


### Nekonečný cyklus
Ještě drobná vsuvka - cykly a podmínky jsme zmínili v předchozí části, nyní použijeme jednu základní formu: "nekonečný cyklus":
```
>>> while podmínka:
...    prováděj_pokud_je_splněná_podmínka()
```

```
>>> a = 0
>>> while True: 
...    a += 1
...    print(a)
```


v nekonečné smyčce se maximální rychlostí vypisuje obsah zvětšující se proměnné "a".

---

!!! hint " **Vychytávka [TAB]**"
    Když chcete v Pythonu nebo Micropythonu něco napsat, naučte se využívat TABulátor (klávesa `TAB`). Když například po promptu `>>>` chcete napsat `octopus_initial.setup()`, zkuste napsat pouze prvních pár písmen a pak zmáčknout `TAB`:
    `>>> oc [TAB]` a systém vám doplní nebo dá vybrat. Stejně tak po tečce: `octopus_initial.` stačí napsat `se` a pak `TAB` - a "našeptávač" automaticky doplní `setup` (nezapomeňte na závorky `()`, je to metoda).

---

Python a následně i Micropython umožňuje i složitější "konstrukce" typu:
```
>>> list(5 * x + y for x in range(10) for y in [4, 2, 1])
```


Zkuste se obaznámit s některými "datovými strukrurami" typu: řetězec, pole, seznam, slovník nebo pokročilejší databáze.
Tomuto tématu se podrobněji věnujeme v samostatném workshopu:
[ws-python-data](/ws-python-data) 
