# ![logo](img/logo_small.png){: style="width:39px" } UpyShell

*V Octopus LAB se zaměřujeme na ESP32 ve spojení s Micropythonem. Hledáme limity a možnosti maximálního zjednodušení práce s mikrokontrolerem. Využíváme výborných vlastností Micropythonu (objektové, modulární, file-sytem…) v tuto chvíli už trochu na doraz, zápolíme s rychlostí i s velikostí paměti RAM i s omezeními dostupných standardních knihoven.*

## Emulátor Linuxového shellu

Přímo v Micropythonu jsme si napsali užitečný **nástroj** pro práci v Micropythonu, který se na první pohled chová jako klasický Linuxový shell *(příkazová řádka v terminálu pro práci se soubory a pod.)*

Jak to celé funguje můžete vidět v krátkém *(zhruba dvouminutovém)* videu:
🡒 [youtube-upyshell](https://www.youtube.com/watch?time_continue=30&v=97gLfae7_AI&feature=emb_logo)

Zdrojový kód je na Githubu 🡒 [/micropython-shell](https://github.com/octopusengine/micropython-shell)

Po úspěšném dokončení [instalace octopusLAB frameworku](/install/#3-prvni-spusteni-a-instalace-workframe-octopus), máme "uPyShell" k dispozici po zadání příkazu `shell()` v Micropythonovém REPLu  - poznáte ho podle promptu `>>>`.

```
>>> shell()
uPyShell:~/$
```

![shell-files](https://www.octopuslab.cz/wp-content/uploads/2020/01/shell1.jpg)

Jak vidíte, změnil se "prompt" na "linuxovou" verzi: `uPyShell:~/$`. Od této chvíle nepíšete **metody Micropythonu**, které musí mít závorky `()`, ale píšete "klasické" příkazy, např. `ls` *(list - výpis souborů aktuálního adresáře)*

```
uPyShell:~/$ ls
uPyShell:~/$ run examples/...
uPyShell:~/$ top
...
```

---

## Práce se soubory

```
uPyShell:~/$ help
...
        cd | Change Directory         | cd examples / cd ..
       pwd | Print Working Dir.       |
        ls | LiSt files and dir.      | ls examples
     mkdir | make directory           | mkdir newdir
        cp | CoPy F (default M)       | cp test.py back.py
        rm | ReMove F                 | rm test.py
```

## Editor
![shell-editor](https://www.octopuslab.cz/wp-content/uploads/2020/02/shell2-thread.png)

## Práce s WiFi
![shell-wifi](https://www.octopuslab.cz/wp-content/uploads/2020/02/shell-ifconfig.png)

## Spouštění procesů

### Více „souběžně běžících procesů“
Na test se dá použít příkaz `sleep 10` (pauza 10 vteřin). Když se spustí s `&` na konci: `sleep 10 &`, tak se rozběhne v samostatném vlákně / procesu. Stejně tak spouštíme ukázku – blikání ledky:
`run examples/blink.py &`
Běžící procesy pak vidíme v `top` – zatím není jednoduché je ukončit, máme značná omezení – takže řešíme dočasně resetem – ale pracujeme na tom.

![shell-run](https://www.octopuslab.cz/wp-content/uploads/2020/02/shell3threads.png)

Pro základní seznámení doporučujeme samosatnou stránku workshopu 🡒 [workshop UpyShell](/ws-upyshell)

---