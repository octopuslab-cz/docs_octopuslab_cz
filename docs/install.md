# ![logo](img/logo_small.png) Instalace systému - společná část

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

!!! note
    Celý **proces je rozdělen do tří bloků**

    Instalaci MicroPythonu do [ESP32](/esp32) říkáme **flashování**. ("Naflešovat" znamená nahrát do vnitřní **flash** paměti ESP.) Postup se liší podle toho, jaký používáte počítač a operační systém, viz dále - kroky 1 a 2.

    1. ###### Příprava počítače
    Červená šipka: Do počítače stáhneme nástroj `esptool` | python nebo exe
    
    2. ###### Instalace Micropythonu do ESP
    Fialové šipky: Do počítače stáhneme `Micropython.bin` (binární soubor) a pomocí esptool ho nahrajeme do ESP

    3. ###### Instalace "workframe" octopus do ESP
    Zelená a oranžová:  Pomocí terminálu (`screen` nebo `Putty`) dokončíme instalaci dalších knihoven *"octopus framework"*


## 1. 2. Instalace Micropythonu a octopus "workframe"

První dva body se liší podle použité platformy (operačního systému):

- [GNU/Linux](/install_linux)
- [Windows](/install_win)
- [Mac_OS](/install_mac)


Pokud je na Vašem **ESP32** úspěšně nahrán **Micropython**, můžete pokračovat dalším krokem tři:

## 3. První spuštění a instalace "workframe" octopus

Posledními kroky jsou:

- **připojit se** USB kabelem k zařízení - *už v tomto kroku je možno projít si základní* [Tutorial1-python](/tutorial1-python)
- **spustit setup** - z prostředí Micropythonu nastavit wifi, připojit se na wifi. 
- **stáhnout poslední verzi** "workframe" Octopus pomocí *octopus_initial.setup*. (Celý systém se stahuje z Internetu přímo do ESP32 přes WiFi.)

### • octopus_initial.setup()

Pro ulehčení instalace máme vlastní fork Micropythonu, do kterého jsme zaintegrovali malý modul `octopus_initial` s metodou `setup()`.

!!! hint " **uPip**"
    Když chcete použít základní (vanilla) verzi Micropythonu, máte možnost stáhnout si "lite" verzi instalátoru i pomocí uPip, která přidává lite modul `micropython-octopuslab-installer` s metodou `deploy()`. 
    Podrobněji na samostatné stránce 🡒 [upip](../pip).



!!! hint " **Vychytávka [TAB]**"
    Když chcete v Pythnou nebo Micropythonu něco napsat, naučte se využívat TABulátor (klávesa `TAB`). Když například po promptu `>>>` chcete napsat `octopus_initial.setup()`, zkuste napsat pouze prvních pár písmen a pak zmáčknout `TAB`:
    `>>> oc [TAB]` a systém vám doplní nebo dá vybrat. Stejně tak po tečce: `octopus_initial.` stačí napsat `se` a pak `TAB` - a "našeptávač" automaticky doplní `setup` (nezapomeňte na závorky `()`, je to metoda).


```bash
>>> octopus_initial.setup()

      ,'''`.
     /      \
     |(@)(@)|
     )      (
    /,'))((`.\
   (( ((  )) ))
   )  \ `)(' / (
       
==============================
         S E T U P
==============================
 [w]   - wifi submenu
 [cw]  - connect wifi
 [cl]  - connect LAN
 [sd]  - system download
 [q]   - quit setup
==============================
select:
```
Zvolte `w` [enter].

### • Nastavení WiFi: 
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
Zvolte `a` *(add wifi)* a stiskněte [enter] pro přidání vaší wifi sítě do zařízení a vyplňte správně:

**SSID:** název Vaší wifi | **PASSWORD:** a heslo do ní. Nastavení WiFi se uloží do flash ESP (v *config/wifi.json*) a **je uchováno** i pro další použití.


### • System download -  Deploy

Pro připojení do Internetu se ve volbě **select:** napíše:
`cw` *(conect wifi)* [enter] a ESP se připojí k internetu. Pak už můžeme zadat `sd` *(system download - from url octopus)* [enter], které provede stažení **TARu** z našeho cloudu - vše se do ESP samo nahraje a rozbalí. Průběžně uvidíte všechny soubory (včetně podadresářů).

!!! tip "**Co obsahuje stable.tar**"

    Vybrané knihovny, které jsou veřejně dostupné na [github.com/octopusengine/octopuslab](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython) po našem otestování jsou převedeny do `.mpy` a uloženy do souboru `stable.tar`, který je v našem **cloudu** *(vzdálené internetové úložiště)*

    Ukázka jak v octopusLABu "kompilujeme" `.py` do `.mpy` (to vy dělat nemusíte)
    
    ```./precompile.sh 
    Compile file deploy/lib/blesync_uart/__init__.py
    Compile file deploy/lib/blesync_uart/client.py
    Compile file deploy/lib/blesync_uart/server.py
    Compile file deploy/lib/blesync.py
    Compile file deploy/components/oled/__init__.py
    Compile file deploy/components/__init__.py
    Compile file ...
    ...
    ```

---

### • Examples - je adresář plný příkladů

Pokud si chcete nahrát velký balíček ukázek a testů, máme k dispozici opět "zabalený" `.tar` soubor u nás v cloudu.
Provedeme reset zařízení. Pak spustíme `setup()` a opět postupně `cw` (connect wifi) a tentokrát `sde` (system download examples).
Více o ukázkách se dozvíte v dokumentaci: [/basicdoc/#octopus-examples](/basicdoc/#octopus-examples).

---
## Setup - nastavení systému

Pro některé projekty a ukázky musíme mít správně nastavenou platformu (desku) a některé další periferie. Příkazem `setup()` nastavujeme i další WiFi sítě. 


!!! hint "**octopus_initial.setup() | setup()**"
    Z prostředí Micropythonu `>>>` spouštíme úplně poprvé inicializační `octopus_initial.setup()`, který je součástí našeho forku Micropythonu. Pak se nám stáhne aktální verze *octopus framework* a pro další nastavování už používáme pouze `setup()`, který je rozšířenou verzí *octopus_initial.setup()*.

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

### Základní nastavení: 

- První nastavení desky - `ds` *(device setting)* - nejčastěji se používá `5` pro [ROBOTboard](https://www.octopuslab.cz/vyvojove-desky/robot-board/) nebo `9` pro [ESP32board](https://www.octopuslab.cz/esp32-board/) - i na "prázdném" ESP je vhodné zvolit alespoň jednu z variant (až podle konkrétních periferíí a především pak podle druhu sběrnic, se řeší, co dál)
- `ios` - nastavení periférií, není nezbytné, kromě oled(I2c) nebo disp7 (SPI) - pokud chcete využít "chytré" [pinouty](/basicdoc/#pinout) "octopus frameworku".
- `w`/ `cw`, `sd`/ `sde` - pro update

---
  
## Práce se soubory - uPyshell | Ampy | Thonny

Pro přesouvání souborů do ESP máme víc možností. Jednoduché úpravy a přímé kopírování se dají rovnou provádět v ESP pomocí emulátoru [uPyShell](/upyshell). Tam se dá využít příkaz `edit` a pak `cp`. Ještě je tu i možnost `wget` pro stažení libovolného souboru z internetu.
(pro `wget` musí být vytvořen adresář `download`)


Další  varianta, kterou jsme dříve využívali i pro `deploy` (sestavení systému) je program `ampy`, přímo určený pro vzdálenou práci se soubory na ESP. Tomu se věnujeme obšírněji na samostatné stránce 🡒 [ampy](/ampy).


Existuje jednoduché IDE s přímým připojením k ESP - opět v samostatném bloku 🡒 [Thonny](/thonny).
(Je k dispozici pro Win, Mac i Linux). 
Aplikace **Thonny** v posledních verzích prošla řadou změn a tak si jistě zaslouží Vaší pozornost.

---

## Shrnutí

Velmi zjednodušeně: Instalce Micropythonu nebo forku OctopusLAB Micropythonu `uPy` je úvodní částí. 
Dále chceme instalovat soubor knihoven `lib` - a nakonec pracovat s hlavním programem `main.py`.


```
             |  uPy  |  lib  |"main.py"
--------------------------------------------
esptool      |   V   |   ~   |   -   |
ampy         |   -   |   V   |   V   |
upip         |   -   |   V   |   ~   |
             |       |       |       |
web_server   |   -   |   ~   |   V   |
thonny       |   -   |   ~   |   V   |
shell editor |   -   |   -   |   V   |
--------------------------------------------
V ... vhodné
~ ... použitelné
- ... nevhodné

```




*Původní verze tohoto dokumentu je na https://www.octopuslab.cz/micropython-octopus/*


 