# ![logo](img/logo_small.png){: style="width:39px" } OCTOPUS Examples - ukázky

### • examples/x.py

V souboru s názvem komponenty by měla být základní ukázka, nejčastěji nejjednodušší nebo nejkratší s využitím **octopus workframe**

- analog
- button
- dcmotor
- display7

- ...

pro mnohé elementární dvouřádkové "návody" ani samostatný soubor ukázky neexistuje. Například pro **led** by vypadal takto:

```python
from components.led import Led
led = Led(2)
led.blink()
```
A dal by se tedy snadno testovat i z příkazové řádky REPLu:
```python
>>> from components.led import Led
>>> led = Led(2)
>>> led.blink() # jednou blikne
```

**Travalé blikání LEDkou?** Ukázkový a testovací příklad, který v nekonečné smyčce provádí `blink()`
```python
...
while True:
    led.blink()
```

Celý zdrojový kód je na Githubu [/examples/blink.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/blink.py)
a z emulátoru terminálu se dá spustit příkazem `run examples/blink.py`:
```
>>> shell()
uPyShell:~/$ run examples/blink.py
```

🡒 [Led](/basicdoc/#led) 🡒 [UpyShell](/upyshell)

---

Podobně pak pro **oled** displej, inicializace přímo na displeji něco "napíše":
```python
from utils.octopus import oled_init
oled = oled_init()
```
🡒 [Oled](/basicdoc/#oled)

### • examples/x_basic.py

ukázka, která ale podrobněji vysvětlí použítí obecnějšího přístupu, naopak oproti předchozímu - je zcela bez využití **octopus workframe**

- [oled_basic](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/examples/oled_basic.py)
- ... (chystáme další)

🡒 [Oled](/basicdoc/#oled)

---

### • examples/test_x.py

Tyto ukázky slouží zároveň i jako soubor "hardwarových" testů jednotlivých komponent, a jsou volány z testovacího adresáře `tests`. Vyznačují se tím, že vždy **pouze jednou** provedou nějakou akci nebo soubor akcí a pak program skončí, aby se případně mohlo pokračovat dalším.
Například pro otestování [EDU_KIT1](/proj-edukit1): voláme soubor [/tests/main-test_sw1.py](https://github.com/octopusengine/octopuslab/blob/master/esp32-micropython/tests/main-test_sw1.py) který spouští následující ukázka/testy:

```python
import examples.test_esp32
import examples.test_led
import examples.test_rgb
import examples.test_display7
import examples.test_analog
```

### • eaxamples/subdir

Specifické ukázky jsou v podaresářích:

- eaxamples/ble
- eaxamples/pubsub
- eaxamples/asyncio
- eaxamples/database
- eaxamples/param

---
