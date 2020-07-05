## Win

![esp-flash](https://www.octopuslab.cz/wp-content/uploads/2019/08/esp-flash-1.jpg)

*Pro instalaci MicroPythonu na vaše ESP32 je třeba "naflashovat" Micropython na náš kontroler. Podrobněji si rozebereme následující kroky:* 

!!! attention "**Stručně:**"
    - pracujeme stále v jednom podadresáři, do kterého musíme
    - stáhnout a *rozzipovat* [esptool.exe](https://dl.espressif.com/dl/esptool-2.6.1-windows.zip)
    - stáhnnout [Octopus Micropython pro ESP32](https://octopusengine.org/download/micropython/micropython-octopus.bin)
    - připojit ESP a *detekovat* **COM** port
    - pomocí `esptool` přehrát Micropython na ESP
    - stáhnout si [putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
    - spustit putty a nastavit "serial", baudrate `115200`, a **COM** port
    - reset ESP (možno jen CTRL+C) a měli bychom v terminálu putty vidět `>>>`
    
    uf - a teď podrobněji:


### 1. Příprava počítače

Ve všech případech (Linux i Mac) budeme pracovat v příkazovém řádku. *Terminálové okno* se vyvolá příkazem `cmd`.
Po kliknutí na ikonu Windows (`WIN`) napíšeme `cmd` a měl by se nám nabídnout "program" **Příkazový řádek**.

Pracujte v novém, prázdném adresáři, např. `projects/esp32`. *Takže byste měli mít osvojeny základy `mkdir`, `cd`, `dir` a pod.*

Pro rychlý start práce s knihovnami OctopusLab si stáhněte do pracovního adresáře binárku Micropythonu z [Octopus Micropython pro ESP32](https://octopusengine.org/download/micropython/micropython-octopus.bin) `https://octopusengine.org/download/micropython/micropython-octopus.bin` - náš fork [oficiálního MicroPythonu](https://micropython.org/download/esp32/)

Po připojení ESP modulu přes kabel USB (typicky microUSB) musíme zjistit, na kterém COM portu ho máme. Typicky `WIN + X` a v menu `Správce zařízení / Porty (COM a Lpt)` najdeme zařízení **Silicon Labs  CP210x USB to UART**. A tam bývá `COM + číslo` (COM3, COM6...)

---

### 2. Instalace Micropythonu do ESP

Nyní půjde o zprovoznění sériové linky do zařízení a nainstalování nástroje `esptool` pro nahrávání `.bin` souborů. 
Pro klasický `esptool` je třeba mít [nainstalovaný Python3](https://naucse.python.cz/lessons/beginners/install/), ale je i varianta stáhnout si spustitelný program `esptool.exe`,  který si stáhnete zde: https://dl.espressif.com/dl/esptool-2.6.1-windows.zip

Pak v příkazovém řádku zadáme postupně:

```bash
esptool.exe --chip esp32 -p COM6 erase_flash 
esptool.exe --chip esp32 -p COM6 write_flash -z 0x1000 ./micropython-octopus.bin
```
*(pozor, staré win10- rozlišují `/` a  `\`)*


První část instalace Micropythonu `erase_flash`, kdy se po spuštění esptool vypisuje sekvence 
`Connecting........_____....._____....._____....._____....._____.....`

někdy je nutno v tuto chvíli na ESP zmáčknout `BOOT`. Více je o tom zde: https://www.esp32.com/viewtopic.php?t=5682

---

### Terminál (putty)

Tato část je také součástí přípravy počítače.

Používáme program [putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) a nastavením: `Serial, rychlost 115200, váš COMport`. Po nastavení zavoláme `open`, ukáže se nové okno terminálu.

![putty](https://www.octopuslab.cz/wp-content/uploads/2019/11/putty1.png)

Pokud se na obrazovce nic nezobrazuje zmáčněte <kdb>ENTER</kdb> a měl by se vám zobrazit prompt interaktivního Pythonu `>>>`. Gratulujeme, máte funkční MicroPython!

Dále můžete pokračovat podkapitolou [první spuštění a instalace octopus workframe](/install/#prvni-spusteni-a-instalace-workframe-octopus).
