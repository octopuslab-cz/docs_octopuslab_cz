# ![logo](img/logo_small.png) Tutorial 1


## Pár prvních pokusů s Pythonem

Většina ukázek z tohoto prvního tutoriálu bude fungovat i na běžném počítači při použití **Pythonu** *(verze 3.5+)*. Cílem je základní představení, částečné pochopení a procvičení elementárních základů. Pokračování, kde už využijeme ESP32 s MicroPythonem, je v samostatném tutoriálu: [Tutorial2](/tutorial2-micropython-esp). Pro ten už si ale musíte [nainstalovat](/install) MicroPython na ESP.

---

### CTRL-C

Po restartu nám ESP32 posílá do našeho počítače na terminál první zprávy s využitím [REPL](/repl) (Read–eval–print loop).
*Zeleně jsou systémové informace, které nás v tuto chvíli nezajímají.*
Po stisknutí **CTRL-C** se přeruší běh programu a uvidíme verzi MicroPythonu:
```
MicroPython v1.13-7-g5060270c6-build-octopusLAB on 2020-09-05; 
ESP32 module (spiram) with ESP32
Type "help()" for more information.
>>>

```

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

Zkuste si napsat `help()`. V Pythonu uvidíte asi něco jiného než v obecném MicroPythonu.

<details>
<summary><b>více... </b><br />
(klikněte pro obsah) V MicroPythonu pro ESP se po <code>help()</code> vypíše:</summary>
<pre><code>>>> help()
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
For a list of available modules, type help('modules')</code></pre>
</details>
<p><hr /></p>



### Výpis dostupných modulů
```
>>> help("modules")
```

<details>
<summary><b>více... </b><br />
(klikněte pro obsah), Které "moduly" jsou aktuálně v Micropythonu dostupné <code>help("modules")</code></summary>
<pre><code>>>> help()
 
*(Verze 1.13)*:

__main__          inisetup          ubluetooth        ure
_boot             machine           ucollections      urequests
_onewire          math              ucryptolib        uselect
_thread           micropython       uctypes           usocket
_uasyncio         neopixel          uerrno            ussl
_webrepl          network           uhashlib          ustruct
apa106            ntptime           uhashlib          usys
btree             onewire           uheapq            utils/octopus_initial
builtins          ssd1306           uio               utils/wifi_connect
cmath             uarray            ujson             utime
dht               uasyncio/__init__ umqtt/robust      utimeq
ds18x20           uasyncio/core     umqtt/simple      uwebsocket
esp               uasyncio/event    uos               uzlib
esp32             uasyncio/funcs    upip              webrepl
flashbdev         uasyncio/lock     upip_utarfile     webrepl_setup
framebuf          uasyncio/stream   upysh             websocket_helper
gc                ubinascii         urandom
Plus any modules on the filesystem
</code></pre>
</details>
<p><hr /></p>


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

Víceřádkové "dočasné definice vlastních funkcí" se provádí pomocí `def název(parametry):` - odsazení za nás udělá [REPL](/repl) `...` nezapomenout na dvojtečku!

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
    Když chcete v Pythonu nebo MicroPythonu něco napsat, naučte se využívat TABulátor (klávesa `TAB`). Když například po promptu `>>>` chcete napsat `octopus_initial.setup()`, zkuste napsat pouze prvních pár písmen a pak zmáčknout `TAB`:
    `>>> oc [TAB]` a systém vám doplní nebo dá vybrat. Stejně tak po tečce: `octopus_initial.` stačí napsat `se` a pak `TAB` - a "našeptávač" automaticky doplní `setup` (nezapomeňte na závorky `()`, je to metoda).

---

Python umožňuje i složitější "konstrukce" typu:

```
# vyfiltruj sudá čísla do desítky:
>>> list(filter(lambda x: x%2 == 0, range(10)))

[0, 2, 4, 6, 8]

# do listu (pole) specifické trojice:
>>> list(5 * x + y for x in range(5) for y in [3, 2, 1])

[3, 2, 1, 8, 7, 6, 13, 12, 11, 18, 17, 16, 23, 22, 21]

```

Zkuste se obeznámit s některými "datovými strukturami" typu: řetězec, pole, seznam, slovník nebo pokročilejší databáze.
Tomuto tématu se podrobněji věnujeme v samostatném workshopu:
[ws-python-data](/ws-python-data) 
