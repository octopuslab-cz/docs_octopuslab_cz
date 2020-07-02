# ![logo](img/logo_small.png) Tutorial 2

V [prvním díle](/tutorial1-python) jsme se seznámili s úplnými základy.
V tomto druhém pokračování základního tutoriálu už budeme potřebovat ESP32.

## Teplota u procesoru
```
>>> import esp32
>>> esp32.raw_temperature()
127
```

## Hallova sonda - magnetického pole
```
>>> import esp32
>>> esp32.hall_sensor()
129 # cca standard hodnota
```

```
>>> esp32.hall_sensor() 
976 # po přiložení magnetu 
```

---