## Win

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

### Stažení Octopus MicroPython

Pracujte v novém, prázdném adresáři, např. `projects/esp32`.

Pro rychlý start práce s knihovnami OctopusLab si stáhněte do pracovního adresáře binárku Micropythonu s [Octopus Micropython pro ESP32](https://octopusengine.org/download/micropython/micropython-octopus.bin) `https://octopusengine.org/download/micropython/micropython-octopus.bin` - náš fork [oficiálního MicroPythonu](https://micropython.org/download/esp32/)

Po připojení ESP modulu přes kabel USB (typicky microUSB) musíme zjistit, na kterém COM portu ho máme. Typicky `WIN + X` a v menu `Správce zařízení / Porty (COM a Lpt)` najdeme zařízení `Silicon Labs  CP210x USB to UART`.


### Flashování Octopus MicroPython

Nyní jde o zprovoznění sériové linky do zařízení a nainstalování nástroje `esptool` pro nahrávání `.bin` souborů. 
Pro `esptool` je třeba mít [nainstalovaný Python3](https://naucse.python.cz/lessons/beginners/install/), ale je i varianta stáhnout si spustitelný program `esptool.exe`,  který si stáhnete zde: https://dl.espressif.com/dl/esptool-2.6.1-windows.zip

Pak ho budete mít uložen například takto (ano staré win rozlišují `/` a  `\`):
```bash
esptool.exe --chip esp32 -p COM6 erase_flash 
esptool.exe --chip esp32 -p COM6 write_flash -z 0x1000 ./download/micropython-octopus.bin
```

### Terminál

Používáme program [putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) a nastavením: `Serial, rychlost 115200, váš COMport`. Po nastavení zavoláme `open`, ukáže se nové okno terminálu.

Pokud se na obrazovce nic nezobrazuje zmáčněte <kdb>ENTER</kdb> a měl by se vám zobrazit prompt interaktivního Pythonu `>>>`. Gratulujeme, máte funkční MicroPython!
