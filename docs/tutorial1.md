# ![logo](img/logo_small.png) Tutorial 1


## Pár prvních pokusů s Micropythonem

Většina ukázek z tohoto tutoriálu bude fungovat i na běžném počítači při použití Pythonu. Cílem je pochopení a procvičení elementárních základů. Pokračování, kde už využijeme ESP32 s Micropythonem je na samostatné stránce: [Tutorial2](/tutorial2)

---

![ufo-gr](img/ufo-gre.gif){: style="width:23px" }  CTRL+C

Po restartu nám ESP32 posílá do našeho počítače na terminál první zprávy.
Zeleně jsou systémové inforamce, které nás v tuto chvíli nezajímají.
Po stisknuté **CTL+C** se přeruší běh programu a uvidíme verzi Micropythonu
```
MicroPython v1.11-180-g8f55a8fab-dirty-build-octopusLAB on 2019-07-29; 
module with ESP32                                                                                                             
Type "help()" for more information.
```

![ufo-sil](img/ufo-sil.gif){: style="width:23px" }  Výčet klávesových zkratek pro práci s REPLem: 

```
CTRL-A     # on a blank line, enter raw REPL mode
CTRL-B     # on a blank line, enter normal REPL mode
CTRL-C     # interrupt a running program
CTRL-D     # on a blank line, do a soft reset of the board
CTRL-E     # on a blank line, enter paste mode
```

![ufo-gr](img/ufo-gre.gif){: style="width:23px" }  **>>>**

`>>>` toto je takzvaný "prompt", terminálová výzva, abychom tam něco napsali - příkaz nebo "posloupnost příkazů".

```
>>> a = 123      #do proměnné se uložila hodnota (číslo 123)
>>> a            #vytiskne / zobrazí hodnotu proměnné 
123              #nebo print(a) 
                
>>> a + 10
133              #zobrazí vypočtenou hodnotu (jako kalkulačka)
```

---

![ufo-or](img/ufo-ora.gif){: style="width:23px" } 
někdy chceme složitější matematické výrazy, než je 
`+` sčítání | `-` odčítání | `*` násobení | `/` dělení

Pro další matematické funkce a konstanty použijeme knihovnu `math`.

```
>>> import math        # importujeme knihovnu, až když jí potřebujeme,
                       # jinak nám zbytečně blokuje operační paměť

>>> math.log10(1000)   # funkce - logaritmus
3.0

>>> math.pi            # konstanta Pí
3.141593               # počet desetinných míst je omezený                 
```


Více řádkové "dočasné definice vlastních funkcí" pomocí `def název(parametry):` - nezapomenout na dvojtečku!

```
def suma(x, y):
... return x + y

>>> suma (1, 2)
3
```

**čekací prodlevy**   - program bude pokračovat až po uplynutí dané doby 
```
from time import sleep, sleep_ms # importujeme jen potřebné knihovny

sleep(1)           # 1 sekund pauza
sleep_ms(100)      # 100 mili sec.
sleep_us(50)       # 50 micro sec.
```

