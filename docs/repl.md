# ![logo](img/logo_small.png){: style="width:39px" } REPL

**REPL** je zkratka pro styl programovacího (nebo přesněji skriptovacího) a ladícího cyklu **Read–eval–print loop**.
Jedná se o "interaktivní MicroPython prompt", který funguje přes USB sériovou linku i vzdáleně přes [WebRrepl](#webrepl).

V originální dokumentaci [docs.micropython.org/repl](https://docs.micropython.org/en/latest/esp8266/tutorial/repl.html) se o REPLu můžete dozvědět, že je v ESP připojen na `UART0` sériové linky, která je na PINech `GPIO1` pro **TX** and `GPIO3` pro **RX**. Rychlost přenosu (Baudrate) je **115200**. To je důvod, proč pro vlastní sériovou linku používáme `UART1`.

!!! hint "Výčet klávesových zkratek pro práci s REPLem"

    - CTRL-A  (on a blank line, enter raw REPL mode)
    - CTRL-B  (on a blank line, enter normal REPL mode)
    - **CTRL-C**  (interrupt a running program)
    - **CTRL-D**  (on a blank line, do a soft reset of the board)
    - CTRL-E  (on a blank line, enter paste mode)

    Nejčastěji potřebujeme CTRL-C (zastavení programu) nebo CTRL-D (reset)

---

## WebRepl

Vzdálené připojení se provádí přes "webovou aplikaci" [micropython.org/webrepl](https://micropython.org/webrepl/).

Pokud ESP připojejí k wifi a následně se spustí `webrepl.start()`, zařízení je na adrese `ws://192.168.4.1:8266/` (port `8266` zatím zůstává historicky z éry ESP8266).

```python
import network
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect('ssid', 'password')

import esp
esp.osdebug(None)

import webrepl
webrepl.start()
```


