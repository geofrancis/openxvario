# optional output of an analog climb rate signal #
![https://openxvario.googlecode.com/svn/wiki/images/Prototype2Back.jpg](https://openxvario.googlecode.com/svn/wiki/images/Prototype2Back.jpg)

Here is an example of an optional Filter that can be connected to the openXvario when needed. The capacitor + resistor are shrink wrapped and can be connected via a 2pin header to the openXvario.
On the openXvario there is a 2pin female header  to connect this filter to the arduino pins GND + ".

If you have a receiver with a RS232 interface, you do NOT have to connect this signal.
If you do not have a receiver with RS232 port, you could try the generation of the climb signal via a small filter. In that case you would need additionally:

  * a 1kOhm resistor
  * a 22uF Capacitor
to activate this function in the code you have to uncomment the line by removing the "//" at the beginning of the line
`//#define ANALOG_CLIMB_RATE`

## Creating a filter to convert the PWM Output to a DC voltage ##
As the arduino will output the lift/sink rate as a PWM signal, this signal has to be converted with the following small circuit:

```
ARDUINO               FrSky Receiver
pin 3 ----- R1 -----+----- A1 or A2
                    |
                    C1
                    |
gnd      ------------

R1= 1kOhm
C1= 10..100uF Electrolytic Capacitor  ( i currently use 22uF )
```

This is how you can put it together:
![https://openxvario.googlecode.com/svn/wiki/images/filterInstruction.png](https://openxvario.googlecode.com/svn/wiki/images/filterInstruction.png)

I do not own a scope, so somebody with the right equipment might want to fine tune these values a bit or come up with a better filter