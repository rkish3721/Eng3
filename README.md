# CircuitPython
This repository will actually serve as an aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Neopixel](#Neopixel)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [Distance_Sensor](#Distance_Sensor)
* [Motor_Control](Motor_Control)
---

## Neopixel
### Description & Code
This assignment was about using the neopixel on the board as well as the rgb led with circuit python to get it to light up in a rainbow pattern.
```python
# SPDX-FileCopyrightText: 2022 ladyada for Adafruit Industries
# SPDX-License-Identifier: MIT

import time
import board
from rainbowio import colorwheel
import neopixel

NUMPIXELS = 1 # Update this to match the number of LEDs.
SPEED = 0.01  # Increase to slow down the rainbow. Decrease to speed it up.
BRIGHTNESS = 0.5  # A number between 0.0 and 1.0, where 0.0 is off, and 1.0 is max.
PIN = board.NEOPIXEL  # This is the default pin on the 5x5 NeoPixel Grid BFF.

pixels = neopixel.NeoPixel(PIN, NUMPIXELS, brightness=BRIGHTNESS, auto_write=False)


def rainbow_cycle(wait):
    for color in range(255):
        for pixel in range(len(pixels)):  # pylint: disable=consider-using-enumerate
            pixel_index = (pixel * 256 // len(pixels)) + color * 5
            pixels[pixel] = colorwheel(pixel_index & 255)
        pixels.show()
        time.sleep(wait)


while True:
    rainbow_cycle(SPEED)
```


### Evidence


<img src="https://learn.adafruit.com/system/assets/assets/000/029/993/original/adafruit_products_2945limorgif_BIG.gif?1453742429" style="width:200px;">



Image credit goes to Martin Ku



### Wiring
![Capture](https://github.com/ldengel3718/Engr3/assets/143533539/26ac5589-7d16-4440-88b8-915730de3213)

### Reflection
This assignment wasn't very hard. The wireing was quite simple, but I did need a little help getting back in the groove with the coding.



## CircuitPython_Servo

### Description & Code
This assignment required us to figure out how to use a servo with circuit python and how to use buttons as well. 
```python
# # SPDX-FileCopyrightText: 2018 Kattni Rembor for Adafruit Industries
#
# SPDX-License-Identifier: MIT

"""CircuitPython Essentials Servo standard servo example"""
import time
import board
import pwmio
from adafruit_motor import servo
from digitalio import DigitalInOut, Direction, Pull


# create a PWMOut object on Pin A2.


pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

button = DigitalInOut(board.D2)
button.direction = Direction.INPUT
button.pull = Pull.DOWN

button2 = DigitalInOut(board.D5)
button2.direction = Direction.INPUT
button2.pull = Pull.DOWN


current_angle = 90  # Initialize the angle
my_servo.angle=current_angle

while True:
    if button.value:  # Button is pressed (remember, we're assuming it's pull-down)
        print(current_angle)
        current_angle = current_angle + 10
        current_angle = max(0, min(180, current_angle))
        my_servo.angle = current_angle  # Set the new angle

    if button2.value:  # Button is pressed (remember, we're assuming it's pull-down)
        print(current_angle)
        current_angle = current_angle - 10
        current_angle = max(0, min(180, current_angle))
        my_servo.angle = current_angle  # Set the new angle
    time.sleep(.
    01)  # Small delay to avoid excessive checking
```

### Evidence
Pictures / Gifs of your work should go here.  You need to communicate what your thing does.
Remember you can insert pictures using Markdown or HTML



![servo-sweeping](https://github.com/ldengel3718/Engr3/assets/143533539/e7bc0941-81fa-479f-aa34-4f226bd29ee9)

### Wiring
![Capture](https://github.com/ldengel3718/Engr3/assets/143533539/946ec9f5-aa5e-43f6-85f8-bd1cee2f63c1)

### Reflection

This assignment was a fun and challenging way. I had trouble starting, but I got some help from Josh, Ryan and Mr. Helmstetter. This helped me figure out some things and finish the assignment.





## Distance_Sensor

### Description & Code
For this assignment we had to first get the serial to print the distance from the distance sensor. Then we had to show this with a corresponding color. 

```python
import time
import board
import adafruit_hcsr04
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)
cm = 0
while True:
    try:
        cm = sonar.distance
        print((cm))
    except RuntimeError:
        print("Retrying!")
    time.sleep(0.1)

```

### Evidence
![Arduino-Ultrasonic-Sensor-Tutorial-0007-Adding-an-LCD-character-display](https://github.com/rkish3721/Eng3/assets/143533512/e204a3d0-4657-4320-b3c4-b8fe1ea702f5)

### Wiring
![unnamed](https://github.com/rkish3721/Eng3/assets/143533512/f964e1ce-5fe3-4822-bf0c-4d395d91436c)

### Reflection
This assignment was relatively easy, at least the beginning. I couldn't figure out how to do the second part, but will try it later.

## Motor_Control
### Description & Code
For this assignment, we had to control a motor's speed by moving a potentiometer. 
```python
import time 
import board
from analogio import AnalogIn
import pwmio
from digitalio import DigitalInOut

#pins
potentiometerpin = AnalogIn(board.A0)
motorpin = pwmio.PWMOut(board.D3)

#prints the potentiometer value then writes it to the motor
while True:
    print(potentiometerpin.value)
    time.sleep(0.1)
    motorpin.duty_cycle = potentiometerpin.value
```


### Evidence

![6297701662400067268](https://github.com/rkish3721/Eng3/assets/143533512/a70487e8-a2c6-43ee-8b03-771ed4fc47b3)

### Wiring
![image](https://github.com/rkish3721/Eng3/assets/143533512/d47290d6-20cf-4512-8c84-e43c0f87e50c)

### Reflection
This project was easy once I got the wiring done. Thankfully, the code already existed for the conversion so I didn't have to figure it out myself


