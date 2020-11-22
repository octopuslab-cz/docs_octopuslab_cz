# ![logo](img/logo_small.png) Setup

Pokud píšeme vlastní programy, což se bude týkat i většiny našich ukázek v `/examples` (adresář v ESP), základ **nastavení** bývá zahrnut v nich. Testovací a prototypovací systém umožní mít konkrétní nastavení i někde uloženo – a k tomu slouží konfigurační soubor `config/ios.json` – input output setup ([nastavení vstupů a výstupů](#nastaveni-vstupu-a-vystupu)).
Nastavení se provádí v základním Micropythonu, kde akci vyvoláme pomocí metody setup:

```microprython
>>> setup()
```

!!! hint "**octopus_initial.setup() | setup()**"
    Z prostředí Micropythonu `>>>` spouštíme **úplně napoprvé** inicializační `octopus_initial.setup()`, který je součástí našeho forku Micropythonu. Pak se nám stáhne aktuální verze *Octopus Framework* a pro další nastavování už používáme pouze `setup()`, který je rozšířenou verzí `octopus_initial.setup()`.

Rozšířené možnosti nastavení:

```bash
>>> setup()
      ,'''`.
     /      \
     |(@)(@)|
     )      (
    /,'))((`.\
   (( ((  )) ))
   )  \ `)(' / (

Hello, this will help you initialize your ESP
ver: 0.68 / 30.6.2020 (c)octopusLAB
Press Ctrl+C to abort

==============================
        S E T U P
==============================
[w]   - wifi submenu
[cw]  - connect wifi
[cl]  - connect LAN
[sd]  - system download > stable octopus modules from URL
[sde] - system download > examples (from URL) /[sdh] hydroponics
[sdp] - system download > petrkr (Beta octopus modules from URL)
[sdo] - system download > octopus (Alfa octopus modules from URL)
[ds]  - device setting
[ios] - I/O setting submenu
[mq]  - mqtt() and sending data setup
[si]  - system info
[wr]  - run web repl
[q]   - quit setup
==============================
select:
```

## Základní nastavení: 

### Nastavení desky

V prvním kroku nejdříve napíšeme `ds` (**device setting**) nastavení desky - (deskou rozumíme jeden z HW modulů pro ESP)
Pro naše ukázky budeme používat nejvíce variantu `5` pro [ROBOTboard](https://www.octopuslab.cz/vyvojove-desky/robot-board/) nebo `9` pro [ESP32board](https://www.octopuslab.cz/esp32-board/).
Pro jiné desky nebo moduly se mění nastavení [pinouty](/basicdoc/#pinout).

---

### Nastavení WiFi

**Wifi submenu** umožní nastavit další Wifi síť. Nastavení WiFi se uloží do flash ESP (v **config/wifi.json**) a je uchováno i pro další použití. Po zvolení `w` s ukáže toto menu nižší úrovně:

```bash
==============================
      S E T U P - W I F I
==============================
 [a]  - Add wifi network
 [r]  - Remove wifi network
 [s]  - Show configuration  
==============================
select:
```

Zvolte `a` (**add wifi**) a stiskněte [enter] pro přidání vaší WiFi sítě do zařízení a vyplňte správně:

**SSID:** název Vaší wifi | **PASSWORD:** a heslo do ní. Nastavení WiFi se uloží do flash ESP (v *config/wifi.json*) a **je uchováno** i pro další použití.

---

### Update

`w`/ `cw`, `sd`/ `sde`

### Ukázkové programy

Můžeme si z cloudu také stáhnout ukázkové programy (budou pak v adresáři /examples)
Postupně zvolte:
`cw` Wifi by se měla připojit, nastaveno už máme od minula) a následně `sde` (system download examples) stáhne opět několik desítek ukázkových souborů.

---

### Nastavení vstupů a výstupů

`ios` (**I/O setting submenu**) - nastavení periférií, není nezbytné, kromě oled (I2c) nebo disp7 (SPI) - pokud chcete využít "chytré" [pinouty](/basicdoc/#pinout) [Octopus FrameWork](/framework).

![ios](https://www.octopuslab.cz/wp-content/uploads/2019/07/workshop-upy201907-2.jpg)

---