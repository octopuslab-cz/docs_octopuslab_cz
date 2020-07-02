# ![logo](img/logo_small.png) uPyShell

Emulátor Linuxového shellu:

Samostatné stránky:
[octopuslab.cz/upyshell](https://www.octopuslab.cz/upyshell/)
[octopuslab.cz/upyshell2](https://www.octopuslab.cz/upyshell2/)

Zdrojové kódy: 
[octopusengine/micropython-shell](https://github.com/octopusengine/micropython-shell)

Popis:

### help

```batch
   --------+--------------------------+--------------------
           | F: file name             |
           | M: "main.py"             | octopusLAB 2019-20
  ---------+--------------------------+--------------------
     clear | clear display            |   
      free | free RAM (memory)        |
        df | Disk Free (flash)        |
        cd | Change Directory         | cd examples / cd ..
       pwd | Print Working Dir.       |
        ls | LiSt files and dir.      | ls examples
     mkdir | make directory           | mkdir newdir
        cp | CoPy F (defaul M)        | cp test.py back.py
        rm | ReMove F                 | rm test.py
       top | main proces info         | 
      wifi | wireless "fidelity"      | wifi on / wifi scan
      ping | Packet InterNet Groper   | ping google.com
  ifconfig | wifi InterFace conf.     |
      wget | wget URL subdir download | wget https://my.web/f.py  
      find | find "text"              | find oled 
       cat | concatenate F (defaul M) | cat back.py
       edit| edit (defaul M)          | simple "line editor"
        ./ | run F                    | ./examples/blink.py
           | run F & > process/thread | run examples/blink.py &
      exit | back to uPy              | > Micropython
  ---------+--------------------------+---------------------
```
---

### práce se soubory

```batch
uPyShell:~/$ ls                            # list = výpis adresářů
uPyShell:~/$ mkdir test                    # vytvoření podadresáře "test"
uPyShell:~/$ cd test
uPyShell:~/$ cp main.py test/main_copy.py  # kopírování souboru
uPyShell:~/$ cat test/main_copy.py         # prohlížení obsahu souboru
uPyShell:~/$ rm test/main_copy.py          # smazání souboru

```

---

### wifi
```batch
uPyShell:~/$ wifi scan
uPyShell:~/$ wifi off
uPyShell:~/$ wifi on
uPyShell:~/$ ifconfig
uPyShell:~/$ ping
uPyShell:~/$ wget https://your_url.path/file.py
```

---

### editor

Občas je potřeba udělat jen malou úpravu v krátkém programu. Nejčastěji je to postupné měnění nějakých parametrů, kterým si chceme ověřit funkčnost programu nebo otestovat různé varianty. To byl důvod, proč jsme se dospěli k na první pohled šílenému nápadu vytvořit alespoň "řádkový" editor v **Micropythonu**.
```batch
uPyShell:~/$ edit main.py
...
h 
```
`h` jako *help* vyvolá tuto stručnou nápovědu:

```batch
  h      print this help
  p      print file (current state in buffer)
  l      toggle line numbers (copy mode)
  q      quit
  q! x   quit without saving changes
  w      write file (save)
  wq     write into file and quit

  i<int> [<str>]   insert new line at given position [int], containing [str] or empty
  a<int> [<str>]   insert new line after given [int], containing [str] or empty
  e<int> [<str>]   edit line number [int], replace line with [str] or will be prompted
  d<int>           delete line number [int]
  c<int>[-<int>]   comment/uncomment line [int] with a #, or multiple lines if a range is provided (does each line separately)

NOTE: New line at the end of every non empty file is enforced.

WARNING: Do not use for editing lines exceeding your terminal width - you may BREAK TOUR FILE!
```

---

### spouštění procesů

V shellu napíšeme pro spuštění programu:
`$ run examples/blink.led`
a by měla blikat Ledka. Běh programu se přeruší CTRL+C, program blink se zastaví, ledka přestane blikat, ale zůstáváme pořád v shellu.

*V tomto popisu dominantně použijeme tradiční „projekt“ blikání ledkou. Je to takový „hello-word“ – základní a nejjednodušší případ, který se dá obvykle aplikovat na většinu další složitějších úloh. Takže když někde uvidíte slovní spojení „blikání ledky“, nemusíte hned nasazovat posměšný úšklebek. Představit si pod tím lze „můj program“ nebo třeba konkrétní „ovládání robotického vozítka“.*

**Odbočka:**
Jak docílíme toho, aby se blikání Ledky samo spouštělo hned po startu? Program main.py v kořenovém adresáři, je po boot.py přesně ten, který se po startu spustí. Takže si můžeme v shellu jednoduše blikání zkopírovat:
`$ cp examples/blink.py main.py`

---