from machine import Pin
from time import sleep_ms
import time
 
LEDintern = Pin('LED', Pin.OUT)
LEDpin0 = Pin(0, Pin.OUT)
LEDpin1 = Pin(1, Pin.OUT)
button = Pin(2, Pin.IN, Pin.PULL_DOWN)
 
zustand_leds = False
letzter_interrupt = 0
entprellzeit = 200
 
def isrTaster(Pin):
    global zustand_leds
    print("stst")
    zustand_leds = not zustand_leds
    
def handle_timer_interrupt(timer):
    print("Timer-Interrupt-ausgelöst!")
    
 
#ISR = Interrupt-Service-Machine
button.irq(trigger=Pin.IRQ_RISING , handler=isrTaster)
 
 
while True:
    if zustand_leds:  
         LEDintern.value(1)
         LEDpin0.value(0)
         LEDpin1.value(1)
         sleep_ms(40)
         LEDintern.value(0)
         LEDpin0.value(1)
         LEDpin1.value(0)
         sleep_ms(40)
    else:
        LEDintern.value(0)
        LEDpin0.value(0)
        LEDpin1.value(0)