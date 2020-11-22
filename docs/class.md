# ![logo](img/logo_small.png){: style="width:39px" } Class

## Magické slovo třída (class) v objektovém programování (OOP)

Letmý úvod do objektového programování si naznačíme na tradičním *hello world* projektu: **blikání ledky**. Svítivá dioda (LED) je malá součástka, kterou snad nemusíme představovat. Takže jak je to s těmi "objekty"?

Všechno v Pythonu je **objekt**. Základní vlastnost objektů (v programu) je to, že obsahují jak data (informace), tak předpis chování – instrukce nebo metody, které s těmito daty pracují. U svítivé diody budou *data* (vlastnosti / property) *1* nebo *0* - podle toho, jestli svítí nebo nesvítí. A metoda bude třeba `blikni` nebo v případě `sviť` je to přesněji: změň hodnotu (value) na *1* `value(1)` nebo pro `zhasni` je to: změň hodnotu na *0* `value(0)`.

**Předpis objektu je ve třídě** `class()`. Podle tohoto předpisu vytváříme takzvanou instanci, do závorek se dávají případné vstupní parametry. Na PINU **2** máme připojenu LED a chceme s ní pracovat pomocí dostupných metod pro třídu Led? Mikrokontroléru to řekneme takto:

`led = Led(2)` **Což znamená:** vytvoř novou instanci `led` podle vzoru `Led` s parametrem `2` (což je číslo PINu, na kterém tuto ledku chceme mít). Je vhodné dodržet nepsané pravilo, že **třída začíná vždy velkým písmenem**. Abychom odlišili `led` od `Led`

`led.value(1)` Syntaxe je pak: instance objektu `led` "tečka" metoda `value` "( parametry )" `(1)`, ze pouze *1*, možno i *True*

Chceme jinou Led? Na jiném pinu? Třeba druhou na PINu 33? Vytvoříme instanci stejného objektu:
`led2 = Led(33)` > a pak jí používáme "stejně": `led2.value(1)`


Na rozdíl od proměnné: `a = 123` *Metoda nebo funkce data získá nebo na základě parametrů zpracuje, proměnná je obsahuje*.


**Třída** je jako formička na vánoční cukroví. `Kolečko, Hvězdička, Prasátko` - to je určení tvaru. A **instance** jsou jednotlivé kousky cukroví touto formičkou vyrobené. Můžeme si vytvořit tucet hvězdiček, podobným způsobem si můžeme připojit více LEDek (každou na jiném PINu)

- `led1 = Led(20)`
- `led2 = Led(2)`
- `led3 = Led(33)`

rozsvícení druhé ledky je: `led2.value(1)` no a zhasnutí třetí je `led3.value(0)`

!!! attention "Shrnutí:"
    Téměř vše v Pythonu je objekt. **Objekt** je kolekce dat (proměnných) a **metod** (funkcí), které s danými daty pracují. Prototypem objektů jsou **třídy**, z nichž jsou všechny **objekty** (čísla, řetězce, funkce, moduly, metody, atp) odvozeny coby **instance**.

---