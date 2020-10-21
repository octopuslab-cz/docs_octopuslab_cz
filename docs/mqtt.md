# ![logo](img/logo_small.png) MQTT

*Internet věcí vyžaduje obrovskou škálovatelnost v síťovém prostoru, aby zvládl nárůst zařízení. IETF 6LoWPAN se používá k připojení zařízení k IP sítím. S miliardami zařízení, které jsou přidávány do internetového prostoru, hraje IPv6 hlavní roli při řešení škálovatelnosti síťové vrstvy. CoAP od IETF, ZeroMQ a MQTT poskytly odlehčený přenos dat. „MQ“ v „MQTT“ pochází z produktové řady IBM MQ řady zpráv:
(Message Queuing Telemetry Transport) 
Zdroj: Wikipedia*


**MQTT** je tedy jednoduchý centralizovaný protokol sloužící nejčastěji pro použití s nejrůznějšími senzory IoT (Internetu věcí).
Lze jej však využít i pro přenos mnoha jiných, například telemetrických dat. Základem je princip typu zveřejnit/odebírat (publish/subscribe). Zařízení s funkcí zveřejnit odesílají zprávy zprostředkovateli (**broker**), který na základě přihlášených odběrů provede třídění a přeposlání uživatelům. Klient-uživatel může zároveň publikovat (**publish**) i odebírat (**subscribe**).


Připravujeme samostatnou stránku zdrojů 🡒 [github.com/octopusengine/octopusLAB_mqtt](https://github.com/octopusengine/octopusLAB_mqtt)

---

🡒 https://github.com/micropython/micropython-lib/tree/master/umqtt.simple

🡒 https://github.com/micropython/micropython-lib/tree/master/umqtt.robust

Ukázky:

```python
# --- example_pub.py ---
from umqtt.simple import MQTTClient

# Test reception e.g. with:
# mosquitto_sub -t foo_topic

def main(server="localhost"):
    c = MQTTClient("umqtt_client", server)
    c.connect()
    c.publish(b"foo_topic", b"hello")
    c.disconnect()

if __name__ == "__main__":
    main()
```

```python
# --- example_sub.py ---
import time
from umqtt.simple import MQTTClient

# Publish test messages e.g. with:
# mosquitto_pub -t foo_topic -m hello

# Received messages from subscriptions will be delivered to this callback
def sub_cb(topic, msg):
    print((topic, msg))

def main(server="localhost"):
    c = MQTTClient("umqtt_client", server)
    c.set_callback(sub_cb)
    c.connect()
    c.subscribe(b"foo_topic")
    while True:
        if True:
            # Blocking wait for message
            c.wait_msg()
        else:
            # Non-blocking wait for message
            c.check_msg()
            # Then need to sleep to avoid 100% CPU usage (in a real
            # app other useful actions would be performed instead)
            time.sleep(1)

    c.disconnect()

if __name__ == "__main__":
    main()
```

---

## Mosquito - Raspberry Pi MQTT broker

Instalce:

```
sudo apt-get install mosquitto mosquitto-clients
```

Ukázka:

```

```



