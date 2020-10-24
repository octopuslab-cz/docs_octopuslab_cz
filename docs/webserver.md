# ![logo](img/logo_small.png){: style="width:39px" } Webserver


Naše verze robustnějšího systému je součástí OctopusLAB FrameWorku:
https://docs.octopuslab.cz/basicdoc/#web-server


---

## MicroWebSrv

Jedna z variant 🡒 https://github.com/jczic/MicroWebSrv

Nejjednodušší implementace:

```python
>>> from utils.octopus import w
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

Další ukázky (například ovládání RGB Ledky) 🡒 [github.com/.../webserver1](https://github.com/octopusengine/octopuslab/tree/master/projects/webserver1)

---

## MicroWebSrv2

Novější verze využívá knihovnu 🡒 [MicroWebSrv2](https://github.com/jczic/MicroWebSrv2)

---



