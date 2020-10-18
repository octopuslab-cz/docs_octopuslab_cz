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


Řetězcový tahák 🡒 [/strings-cs.pdf](https://pyvec.github.io/cheatsheets/strings/strings-cs.pdf)

---

## Pole / seznamy

```python
# definice seznamu
>>> s = [3, 1, 2]
>>> list(s)
```

Zjednodušně můžeme navázat na řetězec, který je vlastně seznamem znaků a proto některé operace budou velmi podobné. Například spojení `+`,
opakování `*`, přístup k prvku `[index]`... a více dalších. Seznamy a řetězce mají své speciální příkazy `split` a `join`.

```python
>>> slova = "první druhé třetí"
>>> slova.split()    #Rozdělí řetězec na slova

>>> data = "123,42,66"
>>> data.split(",")  #Rozdělí "vstup" daným oddělovačem (zde čárka)

>>> ''.join(['o', 'c', 't','o', 'p', 'u', 's'])  #Spojí s do jednoho řetězce
...
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

## Struktury

Pro složitější struktury využíváme objektové vlastnosti při definici tříd. Můžeme vytvářet libovolnou složitost, propojování a vnořování. 
*Klidně se může jednat i o "pole objektů tvořených slovníky a dalšími objekty".*

---

## Databáze

Micropython má implementovánu jednoduchou "databázi" `btree`.
Tuto jsme trochu rozšířili a zpřístupnili pro práci s našimi projekty.
Stručně v octopusLAB frameworku 🡒 [/docs/database](/basicdoc/#database)

---

## Config

Framework Octopus má třídu `Config`, která usnadní práci s externím nastavováním.
V adresáři confih je uližen `json` soubor, do (a ze) kterého se ukládají (načítají) data.

Podrobněji na 🡒 [basicdoc/config](/basicdoc/#config).

Modifikovaná ukázka práce s Configem:

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
