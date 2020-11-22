# ![logo](img/logo_small.png) Workshop Python DATA

## Řetězce

```python
#Accessing string characters in Python
str = 'octopus'
print('str = ', str)             #-> str = octopus
print('str[0] = ', str[0])       #-> o (první znak - s indexem [0])
print('str[-1] = ', str[-1])     #-> s (poslední znak)
print('str[1:5] = ', str[1:5])   #-> ctop ("substring" od-do)
print('str[3:-2] = ', str[3:-2]) #-> op (od-do odzadu)
...
```

Vybrané metody:


```python
>>> 'octopus'.upper() # převede na velká písmena
'OCTOPUS'

>>> 'hledej slovo jablko'.find("jablko") # pozice výskytu hledaného řetězce
13

>>> 'hledej slovo jablko'.find("meloun") # nenalezeno: -1
-1

>>> 'zamena slova jablko'.replace('jablko', 'meloun')
'zamena slova meloun'

>>> ...

```



Řetězcový tahák 🡒 [/strings-cs.pdf](https://pyvec.github.io/cheatsheets/strings/strings-cs.pdf)

---

## Pole / seznamy

```python
# definice seznamu
>>> s = [3, 1, 2]
>>> list(s)
```

Seznamy podporují, podobně jako řetězce, mnoho operací. Namátkou jmenujme spojování, násobení celým číslem, indexování, operace s podsekvencemi (slice) a další.
Zjednodušně tedy můžeme navázat na řetězec, který je vlastně seznamem znaků a proto některé operace budou obdobné. Například spojení `+`,
opakování `*`, přístup k prvku `[index]`... a více dalších. Seznamy a řetězce mají své speciální příkazy `split` a `join`.

```python
>>> slova = "první druhé třetí"
>>> slova.split()    #Rozdělí řetězec na slova

>>> data = "123,42,66"
>>> data.split(",")  #Rozdělí "vstup" daným oddělovačem (zde čárka)

>>> ''.join(['o', 'c', 't','o', 'p', 'u', 's'])  #Spojí s do jednoho řetězce
...
```

Rovnež lze přiřadit hodnotu urcité subsekvenci. Takto dokonce můžeme změnit i počet prvků seznamu:

```python
>>>  a = ["x", "y", 123, 567]

>>> # Změna prvků:
... a[0:2] = [11, 22]
>>> a
[11, 22, 123, 567]
>>> # Jejich odstranění:
... a[0:2] = []
>>> a
[123, 567]
>>> # Vložení nových:
... a[1:1] = ["abc", "octopus"]
>>> a
[123, ’abc’, ’octopus’, 567]
>>> a[:0] = a # Vložení kopie seznamu do sebe sama (stejně tak: a * 2)
>>> a
[123, ’abc’, ’octopus’, 567, 123, ’abc’, ’octopus’, 567]
...

```

*Je-li třeba iterovat přes prvky aritmetické posloupnosti, využijeme interní funkci `range()`, která vrací tuto
posloupnost jako klasický seznam. Funkci `range()` předáme konečnou hodnotu posloupnosti. Pro všechny prvky pak bude platit, že jsou menší než tato hodnota:*

```python
>>> range(7) # [0, 1, 2, 3, 4, 5, 6]
>>> range(5, 10) # [5, 6, 7, 8, 9]
>>> range(0, 15, 3) # [0, 3, 6, 9, 12]
>>> range(-10, -100, -30) # [-10, -40, -70]

for i in range(7):
     print(1,end="")

123456
```



Tahák na seznamy 🡒 [/lists-cs.pdf](https://pyvec.github.io/cheatsheets/lists/lists-cs.pdf)

---

## Slovníky

Uspořádané dvojice klíč `key` a hodnota `value` mají skvělé využití v mnoha algoritmizačních "problémech"
a často slouží jako základ jednoduchých databázových struktur.

```
dict = {"key","value"}
```

```python
# vytvoření slovníku
>>> barvy = {'jablko': 'cervena', 'hruska': 'zelena'} # Micropython bez diakritiky
>>> barvy['boruvka'] = 'modra'                        # nový záznam
>>> barva = barvy['jablko']

>>> hodnoty = dict(a=1, b=2) # z pojmenovaných argumentů
>>> hodnota = hodnoty['b']

# d.get(k)
# d.pop(k)
...

```

```python
# iterace: d.keys() d.values() d.items()
for ovoce, barva in barvy.items():
    print('{}: {}'.format(
    ovoce, barva))
```

```python
# json
import json
json.loads(s)
json.dumps(d)
json.dumps(d, indent=2, ensure_ascii=False) # : odsazení o 2 mezery, nekódovat diakritiku
```

Slovníkový tahák  🡒 [/dicts-cs.pdf](https://pyvec.github.io/cheatsheets/dicts/dicts-cs.pdf)

---

## Rozšíření

Micropython neobsahuje vše, co plnohodnotný Python, ale praktické věci můžeme řešit dodatečnou instalací rozšířujícího modulu.
Například pro práci s **iterátory** [itertools](/extension/#itertools).

---

## Struktury

Pro složitější struktury využíváme objektové vlastnosti při definici tříd. Můžeme vytvářet libovolnou složitost, propojování a vnořování. 
*Klidně se může jednat i o "pole objektů tvořených slovníky a dalšími objekty".*

---

## Databáze

Micropython má implementovánu jednoduchou "databázi" `btree`.
Tuto jsme trochu rozšířili a zpřístupnili pro práci s našimi projekty.
Stručně v [Octopus FrameWork](/framework) 🡒 [/docs/database](/basicdoc/#database)

---

## Config

Framework Octopus má třídu `Config`, která usnadní práci s externím nastavováním.
V adresáři config je uložen `json` soubor, do (ze) kterého se ukládají (načítají) data (hodnoty nastavení).

Podrobněji na 🡒 [/basicdoc/config](/basicdoc/#config).

Modifikovaná ukázka práce s Configem s využitím práce se seznamy a slovníky:

```python
>>> from config import Config
>>> promenne = "tempMax tempMin" # slova oddělená mezerami
>>> keys = promenne.split()      # keys = ["tempMax","tempMin"]
>>> conf = Config("termostat", keys) # > config/termostat.json
>>> conf.setup()

==================================================
        S E T U P - config/termostat.json
==================================================
[ 1] -          tempMax - 23
[ 2] -          tempMin - 18
[q] - Quit from json setup
==================================================
...

```
