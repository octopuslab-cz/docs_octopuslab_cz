# ![logo](img/logo_small.png) Tutorial 2

V [prvním díle](/tutorial1-python) jsme se seznámili s úplnými základy.
V tomto druhém pokračování základního tutoriálu už budeme potřebovat ESP32.

## Rozsvítíme LED diodu?

Na velké části ESP modulů máme k dispozici vestavěnou svítivou diodu na PINU 2. Nejjednodušší, jak nastavit hodnotu `value()` na pinu `Pin` je následující způsob:

```python
from machine import Pin
led = Pin(2, Pin.OUT)
led.value(1)
```

## Teplota u procesoru
```python
>>> import esp32
>>> esp32.raw_temperature()
127
```

## Hallova sonda - magnetického pole
```python
>>> import esp32
>>> esp32.hall_sensor()
129 # cca standard hodnota
```

```python
>>> esp32.hall_sensor() 
976 # po přiložení magnetu 
```

Pro další pokus je vhodné mít už kromě modulu i nějakou možnost připojid další LED diodu nebo například malý piezzo "pípák":

![breadboard](https://www.octopuslab.cz/wp-content/uploads/2019/08/Sn%C3%ADmek-obrazovky-22-768x525.png)

```python
from components.buzzer import Buzzer
piezzo = Buzzer(18)
piezzo.beep()
 
# napřímo přes octopus():
beep()                   
# základní pípnutí (1000,50) > 1kHz na 50ms

beep(440,500)            
# komorní a 440Hz na 0.5s 

>>> from components.buzzer import notes 
>>> Notes.A4                
440    
#k dispozici jsou tóny C3-C7 
>>> buzzer.play_tone(Notes.A4)   # = tone(440) 
```


---