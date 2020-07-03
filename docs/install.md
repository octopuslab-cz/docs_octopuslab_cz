# ![logo](img/logo_small.png) Instalace systému - společná část

*Původní verze tohoto dokumentu je na https://www.octopuslab.cz/micropython-octopus/*

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

!!! note
    Celý **proces je rozdělen do tří bloků**

    *Pro instalaci MicroPythonu na vaše ESP32 je třeba "naflashovat" Micropython na náš kontroler. Postup se liší podle toho, jaký používáte operační systém, viz dále.* 

    1. ###### Příprava počítače
    Červená šipka: Do počítače stáhneme nástroj esptool | python nebo exe
    
    2. ###### Instalace Micropythonu do ESP
    Fialové šipky: Do počítače stáhneme Micropython (binární soubor) a pomocí esptool ho nahrajeme do ESP

    3. ###### Instalace "workframe" octopus do ESP
    Zelená a oranžová:  Pomocí terminálu (screen nebo Putty) dokončíme instalaci knihoven v modulu octopus

První dva body se liší podle použité platformy (operačního systému):

- [GNU/Linux](/install_linux)
- [Windows](/install_win)
- [Mac_OS](/install_mac)

Pokud je na Vašem ESP úspěšně nahrán Micropython, můžete pokračovat dalším krokem tři:

---

## První spuštění a instalace "workframe" octopus


- **připojit se** USB kabelem k zařízení - *už v tomto kroku je možno projít si základní* [Tutorial1](/tutorial1)
- **spustit setup** - z prostředí Micropythonu nastavit wifi, připojit se na wifi
- **stáhnout poslední verzi** "workframe" Octopus pomocí *octopus_initial.setup*

### octopus_initial.setup()

Pro ulehčení instalace máme vlastní fork Micropythonu, do kterého jsme zaintegrovali malý modul `octopus_initial`.

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
```
zvolte `w` [enter]

### Nastavení WiFi: 
```bash
==============================
      S E T U P - W I F I
==============================
 [a]  - Add wifi network
 [r]  - Remove wifi network
 [s]  - Show configuration  
==============================
```
zvolte `a` a stiskněte [enter] 
pro přidání vaší wifi sítě do zařízení 
(uloží se do flash ESP v config/wifi.json) 

`SSID:` název Vaší wifi

`PASSWORD:` a heslo do ní


### System download -  Deploy
Po připojení do Internetu se v select setupu napíše:
`cw` [enter] (conect wifi)
ESP se připojí k WiFi

`sd` [enter] (system download - from url octopus), které provede stažení **TARu** z našeho cloudu - vše se do ESP samo nahraje a rozbalí. Průběžně uvidíte všechny soubory (včetně podadresářů).
*(*3)*

---

### Examples - je adresář plný příkladů

Pokud si chcete nahrát velký balíček ukázek a testů, máme k dispozici opět "zabalený" `.tar` soubor u nás v cloudu.
Provedeme reset zařízení. Pak spustíme `setup()` a opět postupně `cw` (connect wifi) a tentokrát `sde` (system download examples).

---


