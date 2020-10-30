# ![logo](img/logo_small.png) Workshop IoT

---

## WiFi

[referenční příručka / wifi_connect](/basicdoc/#wificonnect)

## Influx

[referenční příručka / influxDB](/basicdoc/#influxdb)

## MQTT

[docs/MQTT](/mqtt)

## Webserver

[docs/webserver](/webserver)

## Simple API

Bez dalšího komentáře uvádíme některé naše ukázky, na kterých vysvětlujeme možnosti vzdáleného připojení ale především rizika připojení nezabezpečeného - některé metody dostupné v octopus() - a následně ukázková stránka na našem serveru:

*Ukázky knihoven jsou dostupné v utils.octopus/ nebo utils.octopus_lib*


```python
>>> getApiJson()
```

🡒 http://www.octopusengine.org/api/onoff.php


Většina prvních příkladů je koncipována takto, ale je to spíš **ukázka, jak se to dělat nemá** - především pro hned několik bezpečnostních chyb.

- **http** nahradit zabezpečeným https
- **GET** nahradit POSTem
- cílit na **ID** a raději ještě zabezpečit **heslem**

*message - POSTem, MD5(UID), "device" jen pro kontrolu*

---

```python
>>> getApiText()
```

🡒 https://octopusengine.org/api/text19.php

trochu lepší - https, zabezpečeno alespoň s heslem ) ale "veřejným"
a také už dbáme na ID zařízení, které může sloužit i jako heslo pro přístup do "IoT sítě" (proto UID pokud nemusíme - veřejně neuvádíme)

---

```python
>>> SetApiValue()
```

připravujeme, ale můžete si zkusit sami - aktuální hodnoty (nebo i log či instalované verze systému) pak uvidíte v aplikaci - zatím je to ve fázi hrubé rozpracovanosti:

🡒 https://www.octopusengine.org/api/last.php

---
