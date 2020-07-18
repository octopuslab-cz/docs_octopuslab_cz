# ![logo](img/logo_small.png) Pinouts

## Hlavní moduly

Nejčastěji budeme používat dva zákldaní moduly, s ESP32:
### Modul ESP32 DoIt 2x15

![DoIt](https://www.octopuslab.cz/wp-content/uploads/2020/06/ESP32-doit-2x15-1.png)

### Modul OctopusLAB ESP32board

![ESP32board](https://www.octopuslab.cz/wp-content/uploads/2020/06/esp32board-a-1024x683.png)

---

## Pinouts file

Celý komplet souborů [pinouts](https://github.com/octopusengine/octopuslab/tree/master/esp32-micropython/pinouts) je na Githubu.
Zaměříme se proto jen na některé hlavní části:

### base.py

```
# Base abstract pinouts without any, this base can be replaced by any board specific settings
# Here should be definiton of every pins used in Octopus library

BUILT_IN_LED = None
HALL_SENSOR  = None

# I2C
I2C_SCL_PIN = None
I2C_SDA_PIN = None

# SPI
SPI_CLK_PIN  = None
SPI_MISO_PIN = None
SPI_MOSI_PIN = None
SPI_CS0_PIN  = None

# Default basic pins
ANALOG_PIN   = None
BUTT1_PIN    = None
PIEZZO_PIN   = None
WS_LED_PIN   = None
ONE_WIRE_PIN = None

# Input pins
I39_PIN = None
I34_PIN = None
I35_PIN = None

# IoT Specific pins
RELAY_PIN = None
MFET_PIN  = None

BUTT1_PIN = None
BUTT2_PIN = None
BUTT3_PIN = None

# PWM pins
PWM1_PIN = None
PWM2_PIN = None
PWM3_PIN = None

# DEV pins
DEV1_PIN = None
DEV2_PIN = None
DEV3_PIN = None

# DC motors
MOTOR_12EN = None
MOTOR_34EN = None
MOTOR_1A = None
MOTOR_2A = None
MOTOR_3A = None
MOTOR_4A = None

# Witty specifiv
LED_RED = None
LED_GRE = None
LED_BLU = None

# UART
RXD0 = None # Used for REPL
TXD0 = None # Used for REPL
RXD1 = None
TXD1 = None

```

### olab_esp32_robot_board1.py

```
"""
This is octopusLab basic library for robotBoard PCB and esp32 soc
I2C / SPI / MOTORs / SERVO / PWM...
Edition: --- 2.12.2018 ---
"""
from micropython import const
from pinouts.olab_esp32_base import *

##WS_LED_PIN 13          # Robot Board v1
WS_LED_PIN = const(15)   # Robot Board v2 - WS RGB ledi diode
ONE_WIRE_PIN = const(32)  #one wire (for Dallas temperature sensor)
PIEZZO_PIN = const(27)

# DC motors
MOTOR_12EN = const(25)
# Select version of robot board
##MOTOR_34EN 15          # Robot Board v1
MOTOR_34EN = const(13)   # Robot Board v2
MOTOR_1A = const(26)
MOTOR_2A = const(12)
MOTOR_3A = const(14)
MOTOR_4A = const(27)

#main analog input (for power management)
ANALOG_PIN = const(36)

#PWM/servo:
PWM1_PIN = const(17)
PWM2_PIN = const(16)
PWM3_PIN = const(4)
#pwm duty for servo:
SERVO_MIN = const(38)
SERVO_MAX= const(130)

#inputs:
I39_PIN = const(39)
I34_PIN = const(34)
I35_PIN = const(35)

#temp
MFET_PIN = const(17) # PWM1
RELAY_PIN = const(16) # PWM2

# DEV pins
DEV1_PIN = const(32)
DEV2_PIN = const(33)
```

### esp32-micropython/pinouts/olab_esp32_esp32_board1.py

Toto bude postupem času hlavní OctopusLAB modul:
```
"""
This is octopusLab basic library for ESP32 board PCB and esp32 soc
Edition: --- 10.8.2019 ---
"""
from micropython import const
from pinouts.olab_esp32_base import *

BUTT1_PIN = const(0)

PWM1_PIN = const(17)
PWM2_PIN = const(16)
PWM3_PIN = const(25)

DEV1_PIN = const(32)  # RAM
DEV2_PIN = const(33)  # RAM
DEV3_PIN = const(27)

#inputs:
I34_PIN = const(34)
I39_PIN = const(39)
I35_PIN = const(35)

# UART 1
RXD1 = const(36)
TXD1 = const(4)

PIEZZO_PIN = const(27) # hack on DEV3

```

