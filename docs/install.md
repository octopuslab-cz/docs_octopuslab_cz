# ![logo](img/logo_small.png) Instalace systému - společná část

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

!!! note
    Celý **proces je rozdělen do tří bloků**

    Instalaci MicroPythonu do [ESP32](/esp32) říkáme **flashování**. ("Naflešovat" znamená nahrát do vnitřní **flash** paměti ESP.) Postup se liší podle toho, jaký používáte počítač a operační systém, viz dále - kroky 1 a 2.

    1. ###### Příprava počítače
    Červená šipka: Do počítače stáhneme nástroj `esptool` | python nebo exe
    
    2. ###### Instalace Micropythonu do ESP
    Fialové šipky: Do počítače stáhneme `Micropython.bin` (binární soubor) a pomocí esptool ho nahrajeme do ESP

    3. ###### Instalace "framework" octopus do ESP
    Zelená a oranžová:  Pomocí terminálu (`screen` nebo `Putty`) dokončíme instalaci dalších knihoven *"octopus framework"*


## 1. 2. Instalace Micropythonu a octopus "workframe"

První dva body se liší podle použité platformy (operačního systému):

- [GNU/Linux](/install_linux)
- [Windows](/install_win)
- [Mac_OS](/install_mac)


Pokud je na Vašem **ESP32** úspěšně nahrán **Micropython**, můžete pokračovat dalším krokem tři:

## 3. První spuštění a instalace "octopusLAB FrameWork"

Posledními kroky jsou:

- **připojit se** USB kabelem k zařízení - *už v tomto kroku je možno projít si základní* [Tutorial1-python](/tutorial1-python)
- **spustit setup** - z prostředí Micropythonu nastavit wifi, připojit se na wifi. 
- **stáhnout poslední verzi** "framework" Octopus pomocí *octopus_initial.setup*. (Celý systém se stahuje z Internetu přímo do ESP32 přes WiFi.)

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

Celý popis `setup()` je na samostatné stránce 🡒 [setup](/setup).

---
  
## Práce se soubory - uPyshell | Ampy | Thony

Pro přesouvání souborů do ESP máme víc možností. Jednoduché úpravy a přímé kopírování se dají rovnou provádět v ESP pomocí emulátoru [uPyShell](/upyshell). Tam se dá využít příkaz `edit` a pak `cp`. Ještě je tu i možnost `wget` pro stažení libovolného souboru z internetu.
(pro `wget` musí být vytvořen adresář `download`)


Další  varianta, kterou jsme dříve využívali i pro `deploy` (sestavení systému) je program `ampy`, přímo určený pro vzdálenou práci se soubory na ESP. Tomu se věnujeme obšírněji na samostatné stránce 🡒 [ampy](/ampy).


Existuje jednoduché IDE s přímým připojením k ESP - opět v samostatném bloku 🡒 [Thony](/thony).
(Je k dispozici pro Win, Mac i Linux). 
Aplikace **Thonny** v posledních verzích prošla řadou změn a tak si jistě zaslouží Vaší pozornost.

---

## Shrnutí

Velmi zjednodušeně: Instalace *vanilla* [Micropythonu](http://micropython.org/download/esp32/) nebo forku [OctopusLAB Micropythonu](https://octopusengine.org/download/micropython/micropython-octopus.bin) `uPy` je úvodní částí. 
Dále chceme instalovat **Octopus LAB Frame Work**, což je soubor knihoven `lib` (modulů). A pak chceme pracovat s hlavním programem `main.py` nebo dalšími knihovnami a moduly.

---

<pre>
             |  uPy  |  lib  | *.py  | Terminal  IDE
-------------------------------------------------------
<a href="/install_win/#2-instalace-micropythonu-do-esp">esptool</a>      |   V   |   ~   |   -   |    -    |   -
<a href="/ampy">ampy</a>         |   -   |   V   |   V   |    -    |   -
<a href="/rshell">rshell</a>       |   -   |   V   |   V   |    V    |   ~
<a href="/pip">upip</a>         |   -   |   V   |   ~   |    -    |   -
<a href="/ftp">FTP</a>          |   -   |   V   |   V   |    -    |   -
<a href="">web_server</a>   |   -   |   ~   |   V   |    V    |   V
<a href="/thony">Thonny</a>       |   V   |   ~   |   V   |    V    |   V
<a href="/espy">EsPy</a>         |   ~   |   ~   |   V   |    V    |   V
<a href="/mu">Mu</a>           |   ~   |   ~   |   V   |    V    |   V
<a href="/upyshell">shell editor</a> |   -   |   -   |   V   |    -    |   ~
-------------------------------------------------------
V ... vhodné
~ ... použitelné
- ... nevhodné
(lib  | *.py - přesun celých knihoven nebo jen dílčí přesun souborů)
</pre>

---


*Původní verze tohoto dokumentu je na https://www.octopuslab.cz/micropython-octopus/*


 