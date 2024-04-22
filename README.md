# CircuitPython
This repository will actually serve as an aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Neopixel](#Neopixel)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [Distance_Sensor](#Distance_Sensor)
* [Motor_Control](#Motor_Control)
* [Photointerrupter](#Photointerrupter)
* [Hangar](#Hangar)
* [Swing_Arm](#Swing_Arm)
* [IR_Sensor](#IR_Sensor)
* [Stepper_Motor](#Stepper_Motor)
* [Rotary_Encoder](#Rotary_Encoder) 
---

## Neopixel
### Description & Code
This assignment was about using the neopixel on the board as well as the rgb led with circuit python to get it to light up in a rainbow pattern. I was able to do both of these and used code from the library package to help understand it. 
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
This assignment was a good introduction to how circuit python works. This assignment taught me how to use rgb LEDs, both on the board and plugged into it. If I were to do it again, I would have used the library code to base my code off of. I would also have looked up rgb values for different colors. 



## CircuitPython_Servo

### Description & Code
This assignment required us to figure out how to use a servo with circuit python and how to use buttons as well. One button moved the servo to the right, and the other moved it to the left. I used online resources on the adafruit site to help me figure this out. 
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
Video: https://drive.google.com/file/d/1mK-RP5ewB0l2BjiGcWdgzII8yKjS32TA/view?usp=sharing
![servo-sweeping](https://github.com/ldengel3718/Engr3/assets/143533539/e7bc0941-81fa-479f-aa34-4f226bd29ee9)


Image Credit to Arduino
### Wiring
![Capture](https://github.com/ldengel3718/Engr3/assets/143533539/946ec9f5-aa5e-43f6-85f8-bd1cee2f63c1)

### Reflection

This assignment was challenging, as I didn't know how to use servos and buttons. I was able to find these online, and used them together to create the code. I learned how to control the angle of the servo and how to use button inputs. I would tell someone doing this project to use the servo example code in the circuit python library and to find code online to help you understand the code. 




## Distance_Sensor

### Description & Code
For this assignment we had to first get the serial to print the distance from the distance sensor. Then we had to show this with a corresponding color: in order going further from the sensor, red, then blue, then green. I wasn't able to figure out the second part.

```python
import time
import board
import adafruit_hcsr04
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6) #gets distance
cm = 0
while True:
    try:
        cm = sonar.distance #assigns distance to variable
        print((cm)) #prints the variable
    except RuntimeError:
        print("Retrying!") #if it doesn't read anything, prints "Retrying!"
    time.sleep(0.1)

```

### Evidence
Video: https://drive.google.com/file/d/1tg2j9kiaf6lywfgwjtjQZqQANztIj7cN/view?usp=sharing

![Arduino-Ultrasonic-Sensor-Tutorial-0007-Adding-an-LCD-character-display](https://github.com/rkish3721/Eng3/assets/143533512/e204a3d0-4657-4320-b3c4-b8fe1ea702f5)



Image Credit to Arduino
### Wiring
![unnamed](https://github.com/rkish3721/Eng3/assets/143533512/f964e1ce-5fe3-4822-bf0c-4d395d91436c)

### Reflection
The first part of this assignment was easy, as all we had to do was print a value. I learned how to get the input from the distance sensor in this part. In the second, I was supposed to find out how to show the distance with a color on an rgb. I could not figure the math out, so I will come back for this later. I think if I were to try again, I would make a spreadsheet or some type of organizer to visualize it for me. 
## Motor_Control
### Description & Code
For this assignment, we had to control a motor's speed by moving a potentiometer up and down, corresponding to the speed. We had to wire up a 6v battery as well as this, which took some time and help. I was able to complete this in two classes, and I think my code is pretty simple. 
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
Video: https://drive.google.com/file/d/1frKmkspSRPbky9wnn8oCSADj2EgPggAO/view?usp=sharing
![6297701662400067268](https://github.com/rkish3721/Eng3/assets/143533512/a70487e8-a2c6-43ee-8b03-771ed4fc47b3)



Image Credit to Arduino
### Wiring
![image](https://github.com/rkish3721/Eng3/assets/143533512/d47290d6-20cf-4512-8c84-e43c0f87e50c)

### Reflection
This project was easy once I got the wiring done. I learned how to write values and speeds to the motor as well as how to get the input of the potentiometers. To any other student starting this, I would say to try to do this in as few lines of code as possible, as it is much simpler when you do it like that. 

## Photointerrupter
### Description & Code
The goal of this assignment was to make it so a number was displayed showing how many times the photointerrupter was triggered between intervals of 4 seconds. We had to use a function other than sleep to wait for counting the time between intervals. We then told the amount of interrupts at the end of the invervals, in a complete sentence. I was able to fully complete this assignment.
```python
from digitalio import DigitalInOut, Direction, Pull
import time
import board
#pins
interrupter = DigitalInOut(board.D7)
interrupter.direction = Direction.INPUT
interrupter.pull = Pull.UP

counter = 0

photo = False
state = False

max = 4 #sets interval
start = time.time()
while True:
    photo = interrupter.value #sets variable to interruptet value
    if photo and not state: #if it's interrupted, increase counter by one
            counter += 1
    state = photo

    remaining = max - time.time()

    if remaining <= 0: #if interval time is up, then reset counter
        print("The Number of Interrupts is: ", str(counter))
        max = time.time() + 4
        counter = 0
```


### Evidence
Video: https://drive.google.com/file/d/1DhBedgn5tXwBwM79UuF_Xf-eRlL-ySZK/view?usp=sharing

![image](https://github.com/rkish3721/Eng3/assets/143533512/bc990605-05be-4ef1-bba6-c86dcaf8b5c6)


Image Credit to Arduino
### Wiring
![image](https://github.com/rkish3721/Eng3/assets/143533512/410f3b8a-ff6a-4074-bc3e-f0a827d9f493)


### Reflection
This assignment was much longer and took more time to figure out because it required longer code and more complicated logic. I learned how to use time functions and the photointerrupter. If I were to do this project again, I would try and find a more simple way of doing it, because I felt like my code was long and messy.


## Swing_Arm

### Assignment Description

The goal with this assignment was to create a swing arm with variable distances in certain dimensions. We had to do this off of sketches that were given to us as well as 2 different sets of variables. I was able to complete this after some difficulty with finding the right things to dimension. 

### Evidence
![image](https://github.com/rkish3721/Eng3/assets/143533512/6b71707a-2bd4-442b-b4b6-7bf840749076)
![image](https://github.com/rkish3721/Eng3/assets/143533512/fc428a0a-9ea0-4ffd-9b46-62a4de0cad18)
![image](https://github.com/rkish3721/Eng3/assets/143533512/79214081-1c8a-421c-9e13-e83eba0ff08f)


### Part Link 

[https://cvilleschools.onshape.com/documents/dc746cfb186d07053b5e0e5a/w/0bd438ac8a7d80cc744575f2/e/dbb2c604f01a1726824c346c?renderMode=0&leftPanel=false&uiState=652020c39e6e0e4d8aa4e6c4](https://cvilleschools.onshape.com/documents/8a3131d7295d5fcba5a5fb46/w/18bc800323359c4ed220c16e/e/f967bfbc066e21d6992bfc97?renderMode=0&uiState=6520232cc410cf73ca87c904)

### Reflection

This part was much more diffucult. I had issues in almost every part of the process. I had issues with sketching, extruding, and applying the fillets. Most of this was because of the confusing diagrams and the amount of constraints. With help from Mr. Miller, I was able to find the mistakes and find the correct mass. I learned how to make my sketches flexible, when I need to put in multiple variables for different steps and measurements. For any other students, I would say to take your time and not assume what dimentions go where, as they might not be used when you change the measurements of other dimensions. 
&nbsp;

## Hangar

### Assignment Description

The goal of this assignment was to create a simple hangar based on sketches with dimensions. I was able to complete this will skills I learned last year, like dimensioning, filleting, and extruding. 
### Evidence

![image](https://github.com/rkish3721/Eng3/assets/143533512/51443432-cf77-46bf-b1d9-54301aa0e0fc)
![image](https://github.com/rkish3721/Eng3/assets/143533512/b0fb2115-0cc3-4a9e-b8dd-24f8e68b7cb9)
![image](https://github.com/rkish3721/Eng3/assets/143533512/8979645f-96c6-4570-b436-c828686e4133)

### Part Link 

https://cvilleschools.onshape.com/documents/dc746cfb186d07053b5e0e5a/w/0bd438ac8a7d80cc744575f2/e/dbb2c604f01a1726824c346c?renderMode=0&leftPanel=false&uiState=652020c39e6e0e4d8aa4e6c4

### Reflection

This part was realively easy and a good way to get back into onshape. The curves on the top were that hardest part to figure out, but if you use the tangent tool it becomes easy. I didn't really learn anything new, just was able to bring back some skills from last year into this project. For any other student, I would say to use basic onshape and CAD skills for this project, because it's easy to overcomplicate it. 
&nbsp;

## IR_Sensor

### Description & Code
For this assignment we had to create a program to detect when an object was near the sensor and change the color of the neopixel accordingly. This was pretty simple, logically, and just took some googling on the parameters and documentation to find the proper commands to use. 
```python

import board
import digitalio
import neopixel 

# Initialize the on-board neopixel and set the brightness.
led = neopixel.NeoPixel(board.NEOPIXEL, 1)
led.brightness = 0.3

# Set up the IR Sensor using digital pin 2. 
ir_sensor = digitalio.DigitalInOut(board.D2)
ir_sensor.direction = digitalio.Direction.INPUT # Set the IR sensor as an input.
ir_sensor.pull = digitalio.Pull.UP              # Use the internal pull-up resistor.


# While loop runs the code inside continuously. 
while True:
    if ir_sensor.value == False: #If something is close, then turn neopixel to red
        led.fill((255,0,0))
        led.show()
    elif ir_sensor.value == True: #if something isn't close, then turn neopixel to green
        led.fill((0,255,0))
        led.show()
```

### Evidence

![IR-Sensor-Upload-Mode](https://github.com/rkish3721/Eng3/assets/143533512/b4af2a07-3688-4e12-8225-a89f6b20ee0b)

Image Credit to Arduino

### Wiring
![image](https://github.com/rkish3721/Eng3/assets/143533512/8eb0f130-1841-4f78-8fbc-ba99ee2f9529)

### Reflection
I learned how to use Ir sensors and how to use the distance for something somewhat useful. Other students would probably find example code useful as it does most of the hard work. I had some trouble with figuring out how to get the input in whole numbers, but was able to use google to look it up. 

## Stepper_Motor

### Description & Code
For this assignment we had to use a stepper motor to press a limit switch to rotate the motor the other 180 degrees. This was the most difficult project of the year in my opinion as it introduced two brand new components into my code.
```python

import asyncio
import board
import keypad
import time
import digitalio
from adafruit_motor import stepper


DELAY = 0.01   # Sets the delay time for in-between each step of the stepper motor.
STEPS = 100    # Sets the number of steps. 100 is half a full rotation for the motor we're using.

# Set up the digital pins used for the four wires of the stepper motor.
coils = (
    digitalio.DigitalInOut(board.D9),   # A1
    digitalio.DigitalInOut(board.D10),  # A2
    digitalio.DigitalInOut(board.D11),  # B1
    digitalio.DigitalInOut(board.D12),  # B2
)

# Sets each of the digital pins as an output.
for coil in coils:
    coil.direction = digitalio.Direction.OUTPUT

# Creates an instance of the stepper motor so you can send commands to it (using the Adafruit Motor library).
motor = stepper.StepperMotor(coils[0], coils[1], coils[2], coils[3], microsteps=None)

motor.onestep()

motor.onestep(direction=stepper.BACKWARD) # tells the motor to go backwards

style=stepper.DOUBLE #how much it does it.

for step in range(STEPS): # tells the motor how to work
    motor.onestep(style=stepper.DOUBLE)
    time.sleep(DELAY)


for step in range(STEPS):
    motor.onestep(direction=stepper.BACKWARD, style=stepper.DOUBLE)
    time.sleep(DELAY)

async def catch_pin_transitions(pin):
    # Print a message when pin goes low and when it goes high.
    with keypad.Keys((pin,), value_when_pressed=False) as keys:
        while True:
            event = keys.events.get()
            if event:
                if event.pressed:
                    print("Limit Switch was pressed.")
                    motor.onestep(direction=stepper.BACKWARD, style=stepper.DOUBLE)

                elif event.released:
                    print("Limit Switch was released.")
                    motor.onestep(direction=stepper.FORWARD, style=stepper.DOUBLE)
                await asyncio.sleep(0)

async def run_motor():
    while(True):
        motor.onestep(style= stepper.DOUBLE)
        time.sleep(DELAY)
        motor.onestep(direction=stepper.BACKWARD, style=stepper.DOUBLE)
        time.sleep(DELAY)

        await asyncio.sleep(0)

async def main():
    while(True):
        interrupt_task = asyncio.create_task(catch_pin_transitions(board.D2))
        asyncio.create_task(run_motor())
        motor.onestep(style-stepper.DOUBLE)
        time.sleep(DELAY)
        motor.onestep(direction=stepper.BACKWARD, style=stepper.DOUBLE)
        time.sleep(DELAY)
        await asyncio.gather(interrupt_task,
                            catch_pin_transitions(board.D2))
       

asyncio.run(main())
```

### Evidence

![image](https://github.com/rkish3721/Eng3/assets/143533512/b8a13bbc-f2a7-4208-b544-7484801334aa)


Image Credit to Mr. Miller's Slides

### Wiring
![0](https://github.com/rkish3721/Eng3/assets/143533512/35cdb1b7-4e31-4b05-8c51-2388915b8591)


### Reflection
In this project I learned how to use stepper motors and limits. I like stepper motors better than regular motors b/c theyre easier to control. I think other students would find it helpful to take the two components one at a time, and figure out how they work in different files first. I liked this project overall, but i think i would've understood it more if they were individual projects. 

## Rotary_Encoder

### Description & Code

```python
import rotaryio
import board
import neopixel
import digitalio
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface

enc = rotaryio.IncrementalEncoder(board.D4, board.D3, divisor = 2)

lcd = LCD(I2CPCF8574Interface(board.I2C(), 0x27), num_rows = 2, num_cols = 16)

led = neopixel.NeoPixel(board.NEOPIXEL, 1)
led.brightness = 0.3
led[0] = (255, 0, 0)

button = digitalio.DigitalInOut(board.D2)
button.direction = digitalio.Direction.INPUT
button.pull = digitalio.Pull.UP
button_state = None  

menu_index = 0

 
while True:
    menu_index = enc.position
    menu = ["stop", "caution", "go"]
    last_index = None
    menu[0] = "stop"
    menu[1] = "caution"
    menu[2] = "go"  
    menu_index_lcd = menu_index % 3
    lcd.set_cursor_pos(0,0)
    lcd.print("Push for: ")
    lcd.set_cursor_pos(1,0)
    lcd.print ("           ")
    lcd.set_cursor_pos(1,0)
    lcd.print(menu[menu_index_lcd])
    print(menu_index_lcd)
    if not button.value and button_state is None:
        button_state = "pressed"
    if button.value and button_state == "pressed":
        print("Button is pressed")
        button_state = None
    if menu_index_lcd == 0:
        led[0] = (255, 0, 0)
    if menu_index_lcd == 2:
        led[0] = (0, 255, 0)
    if menu_index_lcd == 1:
        led[0] = (255, 255, 0)
```

### Evidence

![unnamed](https://github.com/rkish3721/Eng3/assets/143533512/c5ee3756-d99e-4d7c-8e8a-1cc440f16c91)

Image Credit to arduino

### Wiring

https://private-user-images.githubusercontent.com/143732572/297813229-5004adef-d614-4104-99fa-f9543e0774cc.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTMxOTQyNzcsIm5iZiI6MTcxMzE5Mzk3NywicGF0aCI6Ii8xNDM3MzI1NzIvMjk3ODEzMjI5LTUwMDRhZGVmLWQ2MTQtNDEwNC05OWZhLWY5NTQzZTA3NzRjYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNDE1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDQxNVQxNTEyNTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iNzA4MWM0NDY2NWZlMmVmMzY1ODFlMTFkODQ5OTdkNWY1ZTQ5NmVlZWViMDk5YzIxZDUxOTExYzNiNTg0Y2JjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.mtNC6EMDFdeoi2cvozj0_Ojw-HYsbLtQyjtcPKWzckg
### Reflection
In this project I relearned how to use LCD's and Rotary Encoders. I think it would be useful for other students to look back on the projects from last year to figure out how to do them again. I had some trouble with the rotation of stop, go, and caution, but was able to figure it out with the help of Henry. 
