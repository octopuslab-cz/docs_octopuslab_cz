# ![logo](img/logo_small.png){: style="width:39px" } Thony

Alternativou k IDE + [Ampy](https://docs.octopuslab.cz/ampy/) (i [esptool](https://github.com/espressif/esptool)) je tento jednoduchý nástroj (program běžící na PC). V prvním vydání byl takřka nepoužitelný (až na pár tutoriálových výjimek), ale novější verze, po odstranění řady zásadních nedostatků, už běží mnohem lépe. **Pro velmi jednoduché a paměťově nenáročné pokusy** funguje podle očekávání, ale když chcete připojení k WiFi a zároveň BlueTooth, tak nejspíš narazíte. Občas i běžící program znemožní korektní start `Thony`, a jelikož se tluče komunikace na sériovém portu, **musíte si osvojit specifické rutiny, jak to provozovat. Pomáhají opakované restarty jak ESP tak Aplikace Thony, což není úplně komfortní**, ale za zkoušku to stojí.


Nastavení v `Tools/Options/Interpreter`, by mělo být zvoleno v **Interpreter** `MicroPython (ESP32)`
a v **Port** Vaše USB připojení k ESP - například `Silicon Labs CP210x USB to UART Bridge (COM6)`.

---

![thony1](https://www.octopuslab.cz/wp-content/uploads/2020/10/thony1-1200x765.png)

Pak v levém sloupci vidíte i soubory dostupné v ESP, které můžete v hlavním okně (horní) editovat, v okně dolním pak bývá přednastaven terminál (shell).

---

Tato speciální aplikace *Thonny - Python IDE for beginners*, je ke stažení zde: 🡒 https://thonny.org/

---

Pár (anglických) odkazů (ale nebojte se použít [google](https://www.google.com/search?sxsrf=ALeKk024xpsufvjOrJskDFK_Od76pAVBvg%3A1602843167094&ei=H3KJX8OiBaSzgwe_7qaoAw&q=thony+esp32&oq=thony+esp32&gs_lcp=CgZwc3ktYWIQAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwA1AAWABgokhoAXAAeACAAQCIAQCSAQCYAQCqAQdnd3Mtd2l6yAEIwAEB&sclient=psy-ab&ved=0ahUKEwiDruuM8LjsAhWk2eAKHT-3CTUQ4dUDCA0&uact=5)):

- [randomnerdtutorials.com/getting-started-thonny-micropython](https://randomnerdtutorials.com/getting-started-thonny-micropython-python-ide-esp32-esp8266/)

- [youtube.com/Saravanan...](https://www.youtube.com/watch?v=lvmNLuHj25o)




