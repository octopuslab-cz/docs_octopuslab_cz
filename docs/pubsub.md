# ![logo](img/logo_small.png){: style="width:39px" } PubSub

!!! note
    Nástroj pro předávání hodnot mezi nezávislými komponenty v rámci projektu a to i v samostatně běžících vláknech. Pracuje na principu **publish and subscribe**. Fork z [basecue/micropython-pubsub](https://github.com/basecue/micropython-pubsub).

    Zdrojový kód knihovny: [./lib/pubsub.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/lib/pubsub.py)

    Základ práce: jedno vlákno (nebo část programu) publikuje získané hodnoty metodou `publish` kde parametrem je `topic` a hodnota `value`. Například`pubsub.publish('topic', value)`. (value může být libovolný objekt). V jednoduché ukázce  jednou za vteřinu generujeme náhodná čísla, která "publikujeme". (pozor, používáme `while True:` - je to blokující, lepší je použít `timer`)

Základem je `import pubsub` a pak dekorátor `@pubsub.subscriber("value")` pro **subscribe** a `pubsub.publish('value', value)` pro **publish**.

## V jednom programu

Tato jednoduchá ukázka pouze naznačuje možnost funkčního použití. Její univerzálnost a robustnost oceníte až při rozsáhlejších projektech.

```python
from time import sleep
from os import urandom
import pubsub
from utils.octopus import disp7_init

print("display7 init")
d7 = disp7_init()  # 8 x 7segment display init

@pubsub.subscriber("value")
def display_num(value):
    d7.show(value)
    

print("start ps_random")

while True:
    value =  int(urandom(1)[0])
    print("rnd.: ", value)
    pubsub.publish('value', value)
    sleep(1)
```

## Samostatné programy / thready / moduly

*Jeden program nebo dva thready. Možnost testovat jako dva v threadu spustitelné programy:*

```python
import pubsub
from utils.octopus import disp7_init

d7 = disp7_init()  # 8 x 7segment display init

@pubsub.subscriber("value")
def display_num(value):
    d7.show(value)
```


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
---

## Zjednodušení na maximum

Jak použití pub sub zjednoduší program? Chceme v pravidelném intervalu zobrazovat náhodná čísla na displeji.
Jde to jednodušeji?

```python
import octopus.ps_display7
import octopus.ps_timer_rnd
```
