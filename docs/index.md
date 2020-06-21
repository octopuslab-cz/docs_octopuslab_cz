# ![logo](img/logo_small.png) OctopusLab

Tohle je základní dokumentace, kde se prolínají popisy knihoven, příklady, návody, tutoriály, části workshopů, projektů a ukázek použití.
Celý zdrojový kód tohoto "manuálu" je na githubu: [octopusengine/docs_octopuslab_cz](https://github.com/octopusengine/docs_octopuslab_cz).

*Každý může navrhovat doplnění, hlásit chyby a libovolným způsobem přispívat. Vždy když se navrhovaná změna schválí (commit) do hlavní větve (master branch), automaticky se publikuje na našich stránkách [docs.octopuslab.cz](https://docs.octopuslab.cz/). Budeme rádi, když nám dáte vědět, jak se Vám s naším dokumentem pracuje. Vypadá to jenom jako taková blost, ale fakt to dalo dost práce.*

Za tým octopusLABu: *Honza Čopák, Petr Kracík, Vašek Chalupníček, Vladimír Jiříček, Jan Češpivo, a další*

---

```
      ,'''`.
     /      \
     |(@)(@)|
     )      (
    /,'))((`.\
   (( ((  )) ))
   )  \ `)(' / (
```

---
**Jednotlivé ukázky se v mezích možností snažíme dělit na:**

![ufo-gr](img/ufo-gre.gif){: style="width:33px" } 
**Jednoduché základy**

Jedním nebo občas i několika po sobě jdoucími příkazy pouze "komandujeme" ESP mikrokontroler s připojenými periferiemi. Jedná se o základní  "početní úkony" a jednoduché metody práce s HW, ovládání LED (svítivé diody), RGB (barevné diody), piezo, jednoduchý podprogram... 


![ufo-gr](img/ufo-ora.gif){: style="width:30px" } 
**Lehce pokročilejší**

HW: Displeje a základní čidla... a mechatronika: servo motor 
SW: Podrobnější vysvětlení  (větvení programu - podmínka, cyklus, ...) > jednoduché projekty, hry a aplikace.


![ufo-gr](img/ufo-ora.gif){: style="width:30px" } ![ufo-gr](img/ufo-ora.gif){: style="width:30px" } 
**Trochu náročnější**

Pokud se toho bojíte, ani na to nekoukejte. Další programátorská teorie: pole, seznamy, slovníky a složité datové struktury... a speciální návody.


![ufo-gr](img/ufo-ora.gif){: style="width:30px" } ![ufo-gr](img/ufo-ora.gif){: style="width:30px" } ![ufo-gr](img/ufo-ora.gif){: style="width:30px" }
**Náročné**

Nic podobného Vám v tomto bloku neukážeme :-P


![ufo-gr](img/ufo-sil.gif){: style="width:30px" }
**Poznámka**

...nebo tak.


![ufo-gr](img/ufo-blu.gif){: style="width:30px" }
**Zajímavost**

Tady by to mohlo být modré celé


![ufo-gr](img/ufo-vio.gif){: style="width:30px" }
**Pozor!**

Nechceme nikoho stresovat, proto to moc nevyužijeme :-P


---
## Vývojové a výukové moduly

Co vlastně děláme? Vymýšlíme různé hardwarové moduly (zaměření na ESP32 a Micropython). Vyrábíme desky plošných spojů, které se dají podle potřeby proměnit v celou řadu zajímavých projektů.
**Námi navržené vývojové a experimentální desky, slouží i jako finálně zapojitelné moduly pro projekty nebo jejich části. Jednoduché (nebo částečně zapojené) projekty výborně pomáhají i při výuce.**

---
## ESP32

Na destičce o velikosti poštovní známky je mikrokontrolér spolu s několika klíčovými komponenty včetně krystalu, leptané antény pro WiFi a Bluetooth modul. Tím usnadňují použití ESP32 a jsou okamžitě připraveny k integraci do koncových produktů.

ESP32 má:

- dvě CPU jádra s nastavitelnou taktovací frekvencí do 240 MHz
- klasické Bluetooth i podporu Bluetooth Low Energy (BLE)
- 4MB Flash paměť
- 3 bloky paměti RAM v celkové velikosti 520kB
- periferie zahrnují kapacitní dotykové senzory, Hallův snímač, zesilovač s nízkým šumem, rozhraní pro SD kartu, Ethernet, vysokorychlostní SPI, UART, I2S a I2C

*Takže má dostatečný výkon, aby na něm mohl běžet i robustnější systém, jako je Micropython.*


![hwsoc](img/hwsoc.png)

---
## Micropython

Micropython je "odlehčená" verze populárního programovacího jazyka Python. *Je to přesněji softwarová implementace vyššího programovacího jazkyka kompatibilního s Python 3.x. Je napsaný v C a optimalizovaný pro použití v mikrokontrolétech.*

Toto není výuka programování – ale jen ukázky a experimenty s přihlédnutím na sadu knihoven a modulů **octopusLab** pro práci s vybraným HW.

- pro podrobnější proniknutí do tajů programování v Pythonu doporučujeme: [naucse.python.cz](https://naucse.python.cz/)
- [naucse.python.cz/course/mi-pyt/intro/micropython](https://naucse.python.cz/course/mi-pyt/intro/micropython/)
- [howto.py.cz](http://howto.py.cz/index.htm)

Python je ale velmi jednoduchý, proto se alespoň zmíníme velmi stručně o syntaxy Pythonu (**syntaxe** = forma, jak se "to" píše*):

- logické členění se provádí pomocí striktního odsazování bloků
- pozor na závorky u metod a funkcí `print(„řetězec“)` a uvozovky pro takzvané řetězce (shluky písmen, co nejsou číslo)
- pozor na dvojtečku za deklarací funkce, cyklu nebo podmínky:

```
def funkce(parametr):
… co se má dělat
```

---
## Instalace systému

Připravujeme, zatím na: [octopuslab.cz/micropython-octopus](https://www.octopuslab.cz/micropython-octopus/)

### Linux
### Win
### Mac

---
