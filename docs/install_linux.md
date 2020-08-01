## GNU/Linux

### Stažení Octopus MicroPython

Pracujte v novém, prázdném adresáři, např. `projects/esp32`.

Pro rychlý start práce s knihovnami OctopusLab si stáhněte do pracovního adresáře binárku Micropythonu s [Octopus Micropython pro ESP32](https://octopusengine.org/download/micropython/micropython-octopus.bin) `https://octopusengine.org/download/micropython/micropython-octopus.bin` - náš fork [oficiálního MicroPythonu](https://micropython.org/download/esp32/)

Nyní jde o zprovoznění sériové linky do zařízení a nainstalování nástroje `esptool` pro nahrávání `.bin` souborů. Pro `esptool` je třeba mít [nainstalovaný Python3](https://naucse.python.cz/lessons/beginners/install/). 

*Tyto instrukce jsou laděné pro Ubuntu 20.04, pokud používáte jinou distribuci, bude tento postup pravděpodobně také fungovat.*

### Terminál

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

### Instalace nástroje `esptool`

*(*1)* Nástroj `esptool` budeme instalovat do [Pythonového virtualenvu](https://naucse.python.cz/course/pyladies/beginners/venv-setup/) - oddělíme jej od systému.

```bash
python3 -m venv venv
source venv/bin/activate
pip install esptool
```

### Flashování Octopus MicroPython

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

Dále můžete pokračovat podkapitolou [první spuštění a instalace octopus workframe](/install/#3-prvni-spusteni-a-instalace-workframe-octopus).