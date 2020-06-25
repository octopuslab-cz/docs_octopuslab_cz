## Instalace systému

Pracujte v novém, prázdném adresáři, např. `projects/esp32`.

Stáhněte si do pracovního adresáře binárku s [Octopus Micropython pro ESP32](https://octopusengine.org/download/micropython/micropython-octopus.bin) - náš fork [oficiálního MicroPythonu](https://micropython.org/download/esp32/) pro rychlý start práce s knihovnami OctopusLab: `https://octopusengine.org/download/micropython/micropython-octopus.bin`

Teď je třeba binární image "naflashovat" na náš kontroler. Instrukce se liší podle toho, jaký používáte operační systém.

V základu jde o zprovoznění sériové linky do zařízení a nainstalování nástroje `esptool` pro nahrávání .bin souborů. Pro `esptool` je třeba mít [nainstalovaný Python3](https://naucse.python.cz/lessons/beginners/install/).

### Linux

Po připojení ESP modulu přes kabel USB (typicky microUSB) se zpřístupní serial device, obvykle v `/dev/ttyUSB0`, pokud chcete název zařízení zjistit, spusťte v terminálu `dmesg -w` před tím, než připojíte USB kabel.

K seriové konzoli se můžeme připojit pomocí příkazu `screen /dev/ttyUSB0 115200`

Vyskočení z `screen` je lehce komplikované, musíte použít sekvenci klávesových zkratek. Postupně zmáčkněte <kbd>CTRL+A</kbd> a potom <kbd>K</kbd>. Dole se zobrazí prompt, zmáčkněte <kbd>Y</kbd> pro potvrzení. Pokud ze screenu vyskočíte jinak, tak se vám může stát, že zůstane připojení "viset" a nebudete moci nahrávat soubory apod., v takovém případě stačí vytáhnout a zastrčit USB kabel.

#### Instalace nástroje `esptool` pro Ubuntu 20.04

Přidat uživatele do skupiny `dialout` pro přístup k sériové lince `sudo adduser <username> dialout`

Nástroj `esptool` budeme instalovat do [Pythonového virtalenvu](https://naucse.python.cz/course/pyladies/beginners/venv-setup/) - oddělíme jej od systému.

```
python3 -m venv venv
source venv/bin/activate
pip install esptool
```


#### Flashování Octopus MicroPython

```
cd projects/esp32
```

Aktivujte vytvořené virtuální prostředí.

```
source venv/bin/activate
```

Stažení aktuální verze

```
wget https://octopusengine.org/download/micropython/micropython-octopus.bin
```

POZOR: následující příklad je pro zařízení `/dev/ttyUSB0`, zkontrolujte přes `dmesg` jaké máte zařízení, riskujete ztrátu dat!

```bash
esptool.py --chip esp32 -p /dev/ttyUSB0 erase_flash 
esptool.py --chip esp32 -p /dev/ttyUSB0 write_flash -z 0x1000 ./micropython-octopus.bin
```

U některých modulů bude pro úspěšné provedení prvního příkazu třeba pro potvrzení zmáčnout tlačítko `BOOT`.

Po úspěšném naflashování se zkuste připojit k MicroPython REPL přes sériovou linku.

```
screen /dev/ttyUSB0 115200
```

Pokud se na obrazovce nic nezobrazuje zmáčněte <kdb>ENTER</kdb> a měl by se vám zobrazit prompt interaktivního Pythonu `>>>`. Gratulujeme, máte funkční MicroPython!

---

### Win

Připravujeme, zatím na: [octopuslab.cz/micropython-octopus](https://www.octopuslab.cz/micropython-octopus/)

---


Po připojení ESP modulu přes kabel USB (typicky microUSB) musíme zjistit, na kterém COM portu ho máme. Typicky `WIN+X` a v menu `Správce zařízení / Porty (COM a Lpt)`.

Pokud chcete zkusit nejrychlejší verzi bez Pythonu v počítači – stačí pouze do vaší pracovní složky rozbalit exe soubor `esptool.exe`,  který si stáhnete zde: https://dl.espressif.com/dl/esptool-2.6.1-windows.zip
Pak ho budete mít uložen například:
```
D:\vas-adresar\esptool.exe
```



#### Flashování Octopus MicroPython

esptool.exe --chip esp32 -p COM6 erase_flash 
esptool.exe --chip esp32 -p COM6 write_flash -z 0x1000 ./download/micropython-octopus.bin

---

### Mac

Připravujeme

---

## První spuštění

- připojit se k zařízení
- spustit initial setup
- nastavit wifi
- připojit se na wifi
- stáhnout poslední verzi prostředí Octopus

```
octopus_initial.setup()
```
