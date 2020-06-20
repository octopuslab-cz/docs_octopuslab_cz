# ![logo](img/logo_small.png) uPyShell

Emulátor Linuxového shellu:

Samostatná stránka:
[octopuslab.cz/upyshell2](https://www.octopuslab.cz/upyshell2/)

Zdrojové kódy: 
[octopusengine/micropython-shell](https://github.com/octopusengine/micropython-shell)

Popis:

### help

```
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

### wifi

### editor

---

### spouštění procesů

V shellu napíšeme pro spuštění programu:
`$ run examples/blink.led`
a by měla blikat Ledka. Běh programu se přeruší CTRL+C, program blink se zastaví, ledka přestane blikat, ale zůstáváme pořád v shellu.

*V tomto popisu dominantně použijeme tradiční „projekt“ blikání ledkou. Je to takový „hello-word“ – základní a nejjednodušší případ, který se dá obvykle aplikovat na většinu další složitějších úloh. Takže když někde uvidíte slovní spojení „blikání ledky“, nemusíte hned nasazovat posměšný úšklebek. Představit si pod tím lze „můj program“ nebo třeba konkrétní „ovládání robotického vozítka“.*

**Odbočka:**
Jak docílíme toho, aby se blikání Ledky samo spouštělo hned po startu? Program main.py v kořenovém adresáři, je po boot.py přesně ten, který se po startu spustí. Takže si můžeme v shellu jednoduše blikání zkopírovat:
`$ cp examples/blink.py main.py`