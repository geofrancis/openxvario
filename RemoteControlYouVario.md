# Introduction #

The openXvario sensitivity can be remotly controlled via a free channel or even if you do not have a spare channel left!

# Details #
by connecting the openXvario to a servo channel you can use it´s value to remotely adjust your variometer sensitivity.
You should enable the
```
#define SEND_KalmanRasT2 
```
option to get the numeric value displayed in the T2 field.

then enable the following define to choose the permant use of a ppm signal to adjust the sensitivity.
```
#define PPM_AllwaysUsed   
```

there are 2 possible ways of using this remote control option:
## Method 1: Remote Control with a dedicated Servo channel ##
just connect the ppm signal of one of your receivers free servo ports to the pin defined in the following line (default=2).
```
#define PIN_PPM 2
```

Configure a free potentiometer in your 9x to send a its value to this channel and you´re done.
To use it, after turning on the openXvario and your transmitter you once have to turn your potentiometer to the min and max positions, as the routine in openXvario has to learn the range before it can use it properly.

## Method 2: programming mode ##

I implemented the new programming mode. This is how it works.

```
#define PPM_AllwaysUsed   
```
### 1.Starting the programming mode ###
Turn on Receiver and open your telemetry data screen
You should enable the following additional fields on it:

==> T1 (will be used for the countdown timer)

==> RPM (will be used to display the sensitivity value (in steps of 30, real value might be a bit different)

==> DIST (will be used to indicate the start/end of programming mode)


### 2. Turn on your power for your plane ###
The openXvario should be connected to the same port as the rudder servo.

### 3. Enter Programming mode ###
the T1 and the DIST field will count down for 5 seconds and a led on the openXvario will blink every 500ms. During these 5 seconds you can move the rudder stick (or whichever channel you are connected to) to the left to enter the programming mode.

==> the oXv will detect this and indicate the start of the programming mode to the pilot in 2 ways:

on the openXvario: the led will blink in this pattern:
1 sec ON, 3 Flashes 100ms, 1 sec ON

on the transmitter in the telemetry display screen:
in the DIST field: 1111, the last stored sensitivity value and again 1111

4. In the Programming mode:
Now for the next 30 seconds (configurable) the oXv will be in programming mode.

==> The remaining time in programming mode will be displayed as a countdown on your open9X in the T1 field.

==> The T1 Field will now display the current Sensitivity setting.

Move the rudder stick once the full way from left to right. the oXv will learn the range by this.
Now change the sensitivity by moving the rudder stick to the desired position.

### 5. End of Programming mode ###
As soon as the countdown in the T1 field reaches 0 the new senitivity will be written to the eeprom the end of the programming mode will be signalled via another flash sequence of the LED and by sending 9999, the sensitivity value and again 9999 to the dist field.

The T1 and Dist field now display whichever fields you configured for them. enjoy flying.

if you want to reenter programming mode turn off/on the power or press reset followed by moving the rudder stick to the left