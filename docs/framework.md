# ![logo](img/logo_small.png){: style="width:39px" } Octopus FrameWork


!!! hint "**Framework**"
    Framework (aplikační rámec) je softwarová struktura, která slouží jako podpora při programování a vývoji a organizaci jiných softwarových projektů. Může obsahovat podpůrné programy, knihovny API, podporu pro návrhové vzory nebo doporučené postupy při vývoji.

    *(Zdroj: Wikipedia)*


## 1. Micropython

<pre>
+-------------+
| MicroPython |
+----+--------+
     |
     +--- Vanilla ---> <a href="/pip/#micropython-octopus-installer">micropython-octopus-installer</a> -+
     |                                                | 
     +--- Octopus ------+-----------------------------+
                        |
                        |
         <a href="/install/#octopus_initialsetup">octopus_initial.setup()</a>
</pre>

---

## 2. Setup

- WiFi
- FTP
- ...

Podrobnější popis na samostatné stránce [setup](/setup).

---

## 3. UpyShell

Malý modul, které se na první pohled chová jako klasický Linuxový shell (příkazová řádka v terminálu pro práci se soubory a pod.)

Podrobnější popis je na samostatné stránce [upyshell](/upyshell).

## 4. Editor

Jednoduchý [řádkový editor](/upyshell/#editor) testových souborů (zdrojových kódů).

---

## 5. Components / Utils

- config
- pubsub
- databáze
- BLE
- ...

## 6. Webserver

Ne ESP32 se dá spustit jednoduchý webový server. V lokální síti pak na dané IP adrese spustíte klasickou webovou stránku,
přes kterou se s ESP dá komunikovat.

Podrobnější popis je na samostatné stránce [webserver](/webserver).

--- 


