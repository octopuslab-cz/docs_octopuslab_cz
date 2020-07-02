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

---