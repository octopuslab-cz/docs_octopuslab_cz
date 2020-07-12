# ![logo](img/logo_small.png) Tutorial 1


## Pár prvních pokusů s Micropythonem

Většina ukázek z tohoto tutoriálu bude fungovat i na běžném počítači při použití Pythonu. Cílem je pochopení a procvičení elementárních základů. Pokračování, kde už využijeme ESP32 s Micropythonem je na samostatné stránce: [Tutorial2](/tutorial2-micropython-esp). Pro ten už si ale už musíte [nainstalovat](/install) Micropython na ESP.

---

### CTRL+C

Po restartu nám ESP32 posílá do našeho počítače na terminál první zprávy.
Zeleně jsou systémové inforamce, které nás v tuto chvíli nezajímají.
Po stisknuté **CTL+C** se přeruší běh programu a uvidíme verzi Micropythonu
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


### >>>

`>>>` toto je takzvaný "prompt", terminálová výzva, abychom tam něco napsali - příkaz nebo "posloupnost příkazů".

```
>>> a = 123      #do proměnné se uložila hodnota (číslo 123)
>>> a            #vytiskne / zobrazí hodnotu proměnné 
123              #nebo print(a) 
                
>>> a + 10
133              #zobrazí vypočtenou hodnotu (jako kalkulačka)
```

---

### Help

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

---

### Math

Někdy chceme složitější matematické výrazy, než je 
`+` sčítání | `-` odčítání | `*` násobení | `/` dělení

Pro další matematické funkce a konstanty použijeme knihovnu `math`.

```
>>> import math        # knihovnuimportuje me, až když jí potřebujeme,
                       # jinak nám zbytečně blokuje operační paměť

>>> math.log10(1000)   # funkce logaritmus je jenou z metod knihovny math
3.0

>>> math.pi            # konstanta Pí (není to metoda!)
3.141593               # a počet desetinných míst je omezený
```

!!! note
      Toto není výuka programování – ale jen ukázky a experimenty s přihlédnutím na sadu knihoven a modulů **octopusLab** pro práci s vybraným hardware. Pro podrobnější proniknutí do tajů programování v Pythonu doporučujeme: 

      - [naucse.python.cz](https://naucse.python.cz/)
      - [naucse.python.cz/course/mi-pyt/intro/micropython](https://naucse.python.cz/course/mi-pyt/intro/micropython/)
      - [howto.py.cz](http://howto.py.cz/index.htm)


!!! hint "**Python je jednoduchý**"

    - logické členění se provádí pomocí striktního odsazování bloků
    - pozor na závorky u metod a funkcí `print("řetězec")` a uvozovky pro takzvané *řetězce (shluky písmen, co nejsou číslo)*
    - pozor na dvojtečku za deklarací funkce, cyklu nebo podmínky: def funkce(parametr)`:`

```
>>> hodnota = 123
>>> print(hodnota)      # > 123 | vypíše obsah proměnné s názvem hodnota (korektně)
>>> print(math.pi)      # > 3.141593
```

### Výpis dostupných modulů
```
>>> help("modules")
```

Více řádkové "dočasné definice vlastních funkcí" pomocí `def název(parametry):` - odsazení za nás udělá REPL ... nezapomenout na dvojtečku!

```
def suma(x, y):
... return x + y

>>> suma (1, 2)
3
```

### Čekací prodlevy
- program bude pokračovat až po uplynutí dané doby 
```
from time import sleep, sleep_ms # importujeme jen potřebné knihovny

sleep(1)           # 1 sekund pauza
sleep_ms(100)      # 100 mili sec.
sleep_us(50)       # 50 micro sec.
```

### Nekonečný cyklus
Ještě drobná vsuvka - cykly a podmínky zmíníme v další části, ale už nyní použijeme jednu základní formu: "nekonečný cyklus"
```
while podmínka:
... prováděj_pokud_je_splněná_podmínka()
```

```
a = 0
while True: 
... a += 1
... print(a)
```
v nekonečné smyčce maximální rychlostí vypisuje obsah zvětšující se proměnné "a"

### Generátor náhodných čísel

Občas se nám v programu hodí vygenerovat pseudonáhodné číslo (pro testování, jednoduché hry, nebo speciální efekty)

```python
>>> from os import urandom
>>> urandom(1)[0]
42
```


---

!!! hint " **Vychytávka [TAB]**"
    Když chcete v Pythnou nebo Micropythonu něco napsat, naučte se využívat TABulátor (klávesa `TAB`). Když například po promptu `>>>` chcete napsat `octopus_initial.setup()`, zkuste napsat pouze prvních pár písmen a pak zmáčknout `TAB`:
    `>>> oc [TAB]` a systém vám doplní nebo dá vybrat. Stejně tak po tečce: `octopus_initial.` stačí napsat `se` a pak `TAB` - a "našeptávač" automaticky doplní `setup` (nezapomeňte na závorky `()`, je to metoda).

