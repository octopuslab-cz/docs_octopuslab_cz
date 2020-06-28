# ![logo](img/logo_small.png) Tutorial 2

V druhém pokračování základního tutoriálu už budeme potřebovat ESP32.

teplota u procesoru:
```
>>> import esp32
>>> esp32.raw_temperature()
127
```

hallova sonda - magnetického pole:
```
>>> import esp32
>>> esp32.hall_sensor()
129 # cca standard hodnota
```

```
>>> esp32.hall_sensor() 
976 # po přiložení magnetu 
```

```

---