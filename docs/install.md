## Instalace systému

*Původní verze tohoto dokumentu je na https://www.octopuslab.cz/micropython-octopus/*

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

Celý **proces je rozdělen do tří bloků** - na této stránce je označujeme *(*1) (*2) a (*3)*

**1) Příprava počítače** (PC s Windows, IOS nebo Linux)
Červená šipka > Do počítače stáhneme nástroj esptool
(python nebo exe)

**2) Instalace Micropythonu do ESP**
Fialové šipky > Do počítače stáhneme Micropython a pomocí esptool ho nahrajeme do ESP

**3) Instalace "workframe" octopus**
Zelená a oranžová > Pomocí terminálu Putty dokončíme instalaci knihoven v modulu octopus()
3.1 octopus Micropython: pomocí octopus_initial.setup()
3.2 Micropython „vlastní“: pomocí deploy – úplně na konci

---


Pro instalaci MicroPythonu na vaše ESP32 je třeba binární image "naflashovat" na náš kontroler *(*2)*. Instrukce se liší podle toho, jaký používáte operační systém, viz dále.

Pracujte v novém, prázdném adresáři, např. `projects/esp32`.

Pro rychlý start práce s knihovnami OctopusLab si stáhněte do pracovního adresáře binárku Micropythonu s [Octopus Micropython pro ESP32](https://octopusengine.org/download/micropython/micropython-octopus.bin) `https://octopusengine.org/download/micropython/micropython-octopus.bin` - náš fork [oficiálního MicroPythonu](https://micropython.org/download/esp32/)

Nyní jde o zprovoznění sériové linky do zařízení a nainstalování nástroje `esptool` pro nahrávání `.bin` souborů. Pro `esptool` je třeba mít [nainstalovaný Python3](https://naucse.python.cz/lessons/beginners/install/). Pokračujte kapitolou pro váš operační systém.


### GNU/Linux

*Tyto instrukce jsou laděné pro Ubuntu 20.04, pokud používáte jinou distribuci, bude tento postup pravděpodobně také fungovat.*

Po připojení ESP modulu přes kabel USB (typicky microUSB) se zpřístupní serial device, obvykle v `/dev/ttyUSB0`. K seriové konzoli se můžeme připojit pomocí příkazu 
```bash
screen /dev/ttyUSB0 115200
```

!!! note "Jak zjistím, zda se mi zařízení hlásí jako `/dev/ttyUSB0`?"
    pokud chcete název zařízení zjistit, spusťte v terminálu `dmesg -w` před tím, než připojíte USB kabel.

Pokud koukáte do prázndé obrazovky s kurzorem vlevo nahoře, je to správně. Nyní máte nastartovaný `screen` na seriové lince, znamená to, že máte nízkoúrovňový přístup k zařízení a můžete ho tedy přeprogramovat (flashnout).

Pokud příkaz končí chybou oprávnění, přidejte vašeho uživatele do skupiny `dialout` pomocí příkazu `sudo adduser <username> dialout` - pozor pro načtení nových oprávnění se musíte odhlásit a přihlásit (nestačí nové okno terminálu) - pokud nevíte, jak to udělat, tak počítač restartujte.

Vyskočení z programu `screen` je lehce komplikované, musíte použít sekvenci klávesových zkratek. Postupně zmáčkněte <kbd>CTRL+A</kbd> a potom <kbd>K</kbd>. Dole se zobrazí prompt, zda chcete opravdu ukončit (kill), zmáčkněte <kbd>Y</kbd> pro potvrzení. Pokud ze screenu vyskočíte jinak, tak se vám může stát, že zůstane připojení "viset" a nebudete moci nahrávat soubory apod., protože na sériové lince může být připojena pouze jedna aplikace, v takovém případě stačí vytáhnout a zastrčit USB kabel.

---

#### Instalace nástroje `esptool`

*(*1)* Nástroj `esptool` budeme instalovat do [Pythonového virtualenvu](https://naucse.python.cz/course/pyladies/beginners/venv-setup/) - oddělíme jej od systému.

```bash
python3 -m venv venv
source venv/bin/activate
pip install esptool
```

#### Flashování Octopus MicroPython

*(*3)*
```bash
cd projects/esp32
```

Aktivujte vytvořené virtuální prostředí.

```bash
source venv/bin/activate
```

Stažení aktuální verze

```bash
wget https://octopusengine.org/download/micropython/micropython-octopus.bin
```

!!! danger "POZOR"
    následující příklad je pro zařízení `/dev/ttyUSB0`, zkontrolujte přes `dmesg` jaké máte zařízení, riskujete ztrátu dat!"

```bash
esptool.py --chip esp32 -p /dev/ttyUSB0 erase_flash 
esptool.py --chip esp32 -p /dev/ttyUSB0 write_flash -z 0x1000 ./micropython-octopus.bin
```

U některých modulů bude pro úspěšné provedení prvního příkazu třeba pro potvrzení zmáčnout tlačítko `BOOT`.

Po úspěšném naflashování se zkuste připojit k MicroPython REPL přes sériovou linku.

```bash
screen /dev/ttyUSB0 115200
```

Pokud se na obrazovce nic nezobrazuje zmáčněte <kdb>ENTER</kdb> a měl by se vám zobrazit prompt interaktivního Pythonu `>>>`. Gratulujeme, máte funkční MicroPython!

---

### Win

Po připojení ESP modulu přes kabel USB (typicky microUSB) musíme zjistit, na kterém COM portu ho máme. Typicky `WIN + X` a v menu `Správce zařízení / Porty (COM a Lpt)` najdeme zařízení `Silicon Labs  CP210x USB to UART`.


#### Flashování Octopus MicroPython

Pokud chcete zkusit nejrychlejší verzi bez Pythonu v počítači – stačí pouze do vaší pracovní složky rozbalit *exe* soubor `esptool.exe` *(*1)*,  který si stáhnete zde: https://dl.espressif.com/dl/esptool-2.6.1-windows.zip
Pak ho budete mít uložen například takto (ano staré win rozlišují `/` a  `\`):
```bash
esptool.exe --chip esp32 -p COM6 erase_flash 
esptool.exe --chip esp32 -p COM6 write_flash -z 0x1000 ./download/micropython-octopus.bin
```
(stačí psát pouze `esptool`)

Používáme program [putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) a nastavením: `Serial, rychlost 115200, váš COMport`. Po nastavení zavoláme `open`, ukáže se nové okno terminálu.

Pokud se na obrazovce nic nezobrazuje zmáčněte <kdb>ENTER</kdb> a měl by se vám zobrazit prompt interaktivního Pythonu `>>>`. Gratulujeme, máte funkční MicroPython!

---

### Mac

Připravujeme - *základ je podobný více Linuxu, z příkazové řádky*.

---

## První spuštění

- **připojit se** k zařízení - *už v tomto kroku je možno projít si základní* [Tutorial1](/tutorial1)
- **spustit setup** - nastavit wifi, připojit se na wifi
- **stáhnout poslední verzi** prostředí Octopus *(3)*

### octopus_initial.setup()

Pro ulehčení instalace máme vlstní fork Micropythonu, do kterého jsme zaintegrovali malý modul `octopus_initial`.

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


