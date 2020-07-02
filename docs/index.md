# ![logo](img/logo_small.png){: style="width:39px" } OctopusLab

Tohle je základní dokumentace, kde se prolínají popisy knihoven, příklady, návody, tutoriály, části workshopů, projektů a ukázek použití.
Všechny podklady tohoto "manuálu" píšeme v [markdownu](https://cs.wikipedia.org/wiki/Markdown) a jsou veřejně na [GitHubu](https://github.com/octopusengine/docs_octopuslab_cz), budeme rádi za vaše připomínky a nápady https://github.com/octopusengine/docs_octopuslab_cz

![github](img/github.jpg){: style="width:90px" } [Co to je? A jak se s ním pracuje?](/github)

---

## Vývojové a výukové moduly

Co vlastně děláme? Vymýšlíme různé hardwarové moduly (zaměření na ESP32 a Micropython). Vyrábíme desky plošných spojů, které se dají podle potřeby proměnit v celou řadu zajímavých projektů.
**Námi navržené vývojové a experimentální desky, slouží i jako finálně zapojitelné moduly pro projekty nebo jejich části. Jednoduché (nebo částečně zapojené) projekty výborně pomáhají i při výuce.**
Další informace jsou na našem webu http://www.octopuslab.cz

---
## ESP32

![hwsoc](img/hwsoc.png){: style="margin:15px;float:left;" } Na destičce *vypadající jako známka* je mikrokontrolér spolu s několika klíčovými komponenty včetně krystalu, antény pro WiFi a Bluetooth. ESP32 je tak okamžitě připraveno k integraci do koncových produktů. 

![esp32](https://www.octopuslab.cz/wp-content/uploads/2020/06/esp32-s.png)

ESP32 má:

- dvě CPU jádra s nastavitelnou taktovací frekvencí do 240 MHz
- klasické Bluetooth i podporu Bluetooth Low Energy (BLE)
- 4MB Flash paměť
- 3 bloky paměti RAM v celkové velikosti 520kB
- periferie zahrnují kapacitní dotykové senzory, Hallův snímač, zesilovač s nízkým šumem, rozhraní pro SD kartu, Ethernet, vysokorychlostní SPI, UART, I2S a I2C

*Takže má dostatečný výkon, aby na něm mohl běžet i robustnější systém, jako je Micropython.*


---
## Micropython

![uPy](img/upy.jpg){: style="width:90px;float:left;" } Micropython je "odlehčená" verze populárního programovacího jazyka Python. *Je to přesněji softwarová implementace vyššího programovacího jazkyka kompatibilního s Python 3.x. Je napsaný v C a optimalizovaný pro použití v mikrokontrolétech.*


<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #8a6d3b;; background-color: #fcf8e3; border-color: #faebcc;">
Toto není výuka programování – ale jen ukázky a experimenty s přihlédnutím na sadu knihoven a modulů <b>octopusLab</b> pro práci s vybraným HW.
</div>


Pro podrobnější proniknutí do tajů programování v Pythonu doporučujeme: 

- [naucse.python.cz](https://naucse.python.cz/)
- [naucse.python.cz/course/mi-pyt/intro/micropython](https://naucse.python.cz/course/mi-pyt/intro/micropython/)
- [howto.py.cz](http://howto.py.cz/index.htm)

Python je ale velmi jednoduchý, proto se alespoň zmíníme velmi stručně o syntaxi Pythonu (**syntaxe** = forma, jak se "to" píše*):

- logické členění se provádí pomocí striktního odsazování bloků
- pozor na závorky u metod a funkcí `print("řetězec“)` a uvozovky pro takzvané *řetězce (shluky písmen, co nejsou číslo)*
- pozor na dvojtečku za deklarací funkce, cyklu nebo podmínky:

```python
def funkce(parametr):
… co se má dělat
```

---

## Jak se zapojit?

Chobotnice je ráda za každý komentář :like:

```
      ,'''`.
     /      \
     |(@)(@)|
     )      (
    /,'))((`.\
   (( ((  )) ))
   )  \ `)(' / (
```


![github](img/github.jpg){: style="width:90px" } [octopusengine/docs_octopuslab_cz](https://github.com/octopusengine/docs_octopuslab_cz)

<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #31708f; background-color: #d9edf7; border-color: #bce8f1;">
Každý může navrhovat doplnění, hlásit chyby a libovolným způsobem přispívat. Vždy, když se navrhovaná změna schválí (commit) do hlavní větve (master branch), automaticky se publikuje na těchto stránkách. Budeme rádi, když nám dáte vědět, jak se Vám s naším dokumentem pracuje. Vypadá to jenom jako taková blost, ale fakt to dalo dost práce.
[Co je to github a jak se s ním pracuje?](/github)
</div>

Za tým octopusLABu: *Honza Čopák, Petr Kracík, Vašek Chalupníček, Vladimír Jiříček, Jan Češpivo, Milan Špaček, Metěj Suchánek a další*

---