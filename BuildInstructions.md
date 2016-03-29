# Introduction #

The build Instructions.


# Details #
I of course do not take any warranty whatsoever for the instructions below. Do it at your own risk. Read and understand all of the information below before you begin.

## Stuff you will need ##
  * an open 9x based transmitter with audio and frsky telemetry modifications
  * an Arduino Pro Mini 5V 16Mhz you need the ATmega328 version. The ATmega168 will NOT work!
  * a FTDI cable ( e.g. FTDI Basic) that provides the DTR Signal to autoreset the arduino when programming)
  * a 5V MS5611 Sensor Module for around 15€-20€ on eBay
  * a suitable Fr-Sky telemetry enabled receiver with a RS232 port or alternativly one free analog input signal (A1 or A2) to transfer the lift/sink rate.
  * a standard servo cable
  * one single lead and connector pin from a servo connector (or a female header pin and a piece of cable.
  * a 2pin 2.54mm header ( to easiliy mount the more common MS5611 modules
  * some heat shrink tube for the variometer(I used a 28mm one)
  * some smaller heat shrink tube for the female header pins used to connect the openXvario to the receiver's RS232 / A1/2 port

## Connecting the Arduino to the receiver and MS5611 module ##
WARNING: make sure you are using only one Power Source for the Arduino. If you connect the arduino to the PC, always disconnect the 5V to the receiver first!

You can use a standard servo cable to connected the Arduino to a free servo port of the frsky receiver.
Pins to be connected:
```
(nano pin names in bracket if different)
=== Powering the Arduino : ===
     Arduino GND   --------------------- Receiver GND (Servo Plug)
     Arduino RAW(VIN)  ----------------- Receiver +5V (Servo Plug)

=== Optional PPM Input from servo port to the arduino: ===
     Arduino Pin 2(D2) ----------------- Receiver PPM Signal (Servo Plug)

=== Output of the data to the receiver: ===
     Arduino Pin 4(D4) ----------------- Receiver RX Pin (If there is a RS232 Port on the receiver)
  or
     Arduino Pin 3(D3) ----------------- Receiver A1 or A2 (If there is NO RS232 Port on the receiver)

=== connecting the MS56711 module to the receiver ===
     Arduino Pin A4   ------------------ MS5611 SDA
     Arduino Pin A5   ------------------ MS5611 SCL
     Arduino VCC (5V) ------------------ MS5611 5V
     Arduino GND      ------------------ MS5611 GND
	 
```

There are various different MS5611 Modules available. I have used the following so far:

---

## the GY-63 module ##

![https://openxvario.googlecode.com/svn/wiki/images/GY-63_200x.jpg](https://openxvario.googlecode.com/svn/wiki/images/GY-63_200x.jpg)

This is one of the more common modules.
i normaly mount it on the back of the arduino (back to back) using a 2pin Header (without the plastic spacer) on the A4+A5 pins

![https://openxvario.googlecode.com/svn/wiki/images/BuildInstructionGY63B.png](https://openxvario.googlecode.com/svn/wiki/images/BuildInstructionGY63B.png)

![https://openxvario.googlecode.com/svn/wiki/images/gy63bSteps.png](https://openxvario.googlecode.com/svn/wiki/images/gy63bSteps.png)


---

## the CJMCU-5611 module ##
![https://openxvario.googlecode.com/svn/wiki/images/CJMCU200x.jpg](https://openxvario.googlecode.com/svn/wiki/images/CJMCU200x.jpg)

The CJMCU-5611module in the above picture is not the most common module, but works fine. It even has 2 seperated I2C bus connectors for the 2 different voltages (3.3V/5V). I got this one from a seller located in UK over ebay. It is slightly bigger than the GY63. I mounted it on top of the arduino.
![https://openxvario.googlecode.com/svn/wiki/images/Wiring%20Diagram%20V2.png](https://openxvario.googlecode.com/svn/wiki/images/Wiring%20Diagram%20V2.png)

### Optional: connect analog climb rate signal to A1 or A2 ###
In case you receiver only has A1 or A2 for telemetry you can still try to use the analog output mode for the climb rate: AnalogClimbRate

## Programming the Arduino ##
The code to put on your Arduino can be customized in various way. Check the CompileOptions page for details

here is the Arduino sketch you have to put on the Arduino: https://openxvario.googlecode.com/svn/branches/openxvario/openxvario.ino

SparkFun has a nice tutorial in which they describe the programming of the Arduino pro mini: http://www.sparkfun.com/tutorials/244 just use the .INO file you can download on this page.
As a programmer i recommend the "FTDI basic" type of programmers which is available on ebay. I got one that has male headers directly on the programmer, so you can place the arduino directly on those headers.
![http://openxvario.googlecode.com/svn/wiki/images/programming.jpg](http://openxvario.googlecode.com/svn/wiki/images/programming.jpg)

If yours hasn´t got those male headers, just plug some header pins into the female headers of the programmer and the other end directly into the arduino pro mini.

## Configuring open9x ##

visit the ConfigureVarioSettingsInOpen9x to learn how to set the configuration in open9x

Now where your openXvario is hopefully happily beeping on your desk, (and soon in the air) you might want to consider donating a small amount:
![https://www.paypalobjects.com/de_DE/DE/i/btn/btn_donateCC_LG.gif](https://www.paypalobjects.com/de_DE/DE/i/btn/btn_donateCC_LG.gif)
[Paypal Donate](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4GNGDMV5VP2US)

Have fun,

rainer