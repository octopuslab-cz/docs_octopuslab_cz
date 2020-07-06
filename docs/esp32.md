# ![logo](img/logo_small.png){: style="width:39px" } ESP 32

![esp32](https://www.octopuslab.cz/wp-content/uploads/2020/06/esp32-s.png)

ESP32 má:

- dvě CPU jádra s nastavitelnou taktovací frekvencí do 240 MHz
- klasické Bluetooth i podporu Bluetooth Low Energy (BLE)
- 4MB Flash paměť
- 3 bloky paměti RAM v celkové velikosti 520kB
- periferie zahrnují kapacitní dotykové senzory, Hallův snímač, zesilovač s nízkým šumem, rozhraní pro SD kartu, Ethernet, vysokorychlostní SPI, UART, I2S a I2C

*Takže má dostatečný výkon, aby na něm mohl běžet i robustnější systém, jako je Micropython.*

---

Nejčastěji budeme používat dva zákldaní moduly, s ESP32:
## Modul ESP32 DoIt 2x15

![DoIt](https://www.octopuslab.cz/wp-content/uploads/2020/06/ESP32-doit-2x15-1.png)

## Modul OctopusLAB ESP32board

![ESP32board](https://www.octopuslab.cz/wp-content/uploads/2020/06/esp32board-a-1024x683.png)

Základem je **deska s pološnými spoji**, která se dá (do)osadit několika způsoby, podle projektu.
Volitelně: převodník USB-UART (FTDI), rozšíření paměti RAM, dva druhy stabilizátoru (klasický pro napájení ze zdroje, nebo úsporný pro napájení za baterky - Li-ion nejčastěji)

---