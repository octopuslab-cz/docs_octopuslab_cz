# ![logo](img/logo_small.png){: style="width:39px" } WebServer


Naše verze robustnějšího systému je součástí OctopusLAB FrameWorku [micropython-web-ide](https://www.octopuslab.cz/micropython-web-ide/)

---

## MicroWebSrv

Jedna z prvních variant (verze 1) 🡒 https://github.com/jczic/MicroWebSrv

A její nejjednodušší **implementace**:

```python
>>> from utils.octopus_lib import w
>>> w() # wifi connect

>>> from microWebSrv import MicroWebSrv
>>> mws = MicroWebSrv(webPath="www/test")
>>> mws.Start(threaded=True)

```

Na ESP uložená stránka `/www/test.htm`:

```html
<html>
<head>
<title>octopusLAB-ESP32</title>
<meta charset="utf-8" />
<link href="main.css" rel="stylesheet" type="text/css" />
</head>

<body>
    <div class="main">
    <h1>test</h1>
    <div class="radius_100">
    pokus
    </div>
</body>
</html>
```

---

**Ukázkový projekt: WebServer control**
Led (on/off) PWM nebo RGB 🡒 [github.com/...//esp32-micropython-webserver-control](https://github.com/octopuslab-cz/esp32-micropython-webserver-control)

HTML + CSS s využitím Java Scriptu, data se předávají v JSON.

![webserver20](https://www.octopuslab.cz/wp-content/uploads/2020/10/webserv-control20-1200x649.png)


```
{Info} ESP32 UID & RAM Free
{Led} On/Off control & PWM
{RGB Led}
{Command}
{Java script} simple test
{SVG} dynamic chart

```


Další ukázky (například opět "jen" ovládání RGB Ledky) 🡒 [github.com/.../webserver1](https://github.com/octopusengine/octopuslab/tree/master/projects/webserver1)

---

## MicroWebSrv2

Novější verze využívá knihovnu 🡒 [MicroWebSrv2](https://github.com/jczic/MicroWebSrv2)


p ř i p r a v u j e m e 

---
