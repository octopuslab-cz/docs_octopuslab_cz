## Win

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

Po připojení ESP modulu přes kabel USB (typicky microUSB) musíme zjistit, na kterém COM portu ho máme. Typicky `WIN + X` a v menu `Správce zařízení / Porty (COM a Lpt)` najdeme zařízení `Silicon Labs  CP210x USB to UART`.


### Flashování Octopus MicroPython

Pokud chcete zkusit nejrychlejší verzi bez Pythonu v počítači – stačí pouze do vaší pracovní složky rozbalit *exe* soubor `esptool.exe` *(*1)*,  který si stáhnete zde: https://dl.espressif.com/dl/esptool-2.6.1-windows.zip
Pak ho budete mít uložen například takto (ano staré win rozlišují `/` a  `\`):
```bash
esptool.exe --chip esp32 -p COM6 erase_flash 
esptool.exe --chip esp32 -p COM6 write_flash -z 0x1000 ./download/micropython-octopus.bin
```
(stačí psát pouze se musí odklikat „Security & Privacy“.esptool`)

Používáme program [putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) a nastavením: `Serial, rychlost 115200, váš COMport`. Po nastavení zavoláme `open`, ukáže se nové okno terminálu.

Pokud se na obrazovce nic nezobrazuje zmáčněte <kdb>ENTER</kdb> a měl by se vám zobrazit prompt interaktivního Pythonu `>>>`. Gratulujeme, máte funkční MicroPython!
