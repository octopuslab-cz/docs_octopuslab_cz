# ![logo](img/logo_small.png) EDU-KIT1

![edu-kit1](https://www.octopuslab.cz/wp-content/uploads/2020/05/edu_kit1-2020-05-v2.png)

- Základem je deska ROBOTboard: [vyvojove-desky/robot-board](https://www.octopuslab.cz/vyvojove-desky/robot-board/)

- Samostatná stránka projektu: [octopuslab.cz/edu-kit1](https://www.octopuslab.cz/edu-kit1/)

- Repozitář na Githubu: [octopusengine/octopuslab-edu-kit1](https://github.com/octopusengine/octopuslab-edu-kit1)

Úvodní seznámení je popsáno v samostatném [Tutoriálu (EDU_KIT1)](/tutorial3-edukit1)

---

# Náhodně blikajíci ledka

```python
from utils.octopus_lib import randint
from components.led import Led

led = Led(2)

# random blink
def randblink(n):
    for _ in range(n):
       delay = randint(100,500)
       print(delay)
       led.blink(delay)


>>> randblink(10)
```
