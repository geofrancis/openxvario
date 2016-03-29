# Introduction #

In this page you will learn how to setup the openXvario in the open9x Firmware.


# Telemetry Options #
![https://openxvario.googlecode.com/svn/wiki/images/Telemetry1.png](https://openxvario.googlecode.com/svn/wiki/images/Telemetry1.png)

Set the field PROTO to Hub
optionally: you can set the field voltage to FAS if you want do not have a better voltage source available (better one would be e.g. a voltage divider connected to A1 or A2)

![https://openxvario.googlecode.com/svn/wiki/images/Telemetry2.png](https://openxvario.googlecode.com/svn/wiki/images/Telemetry2.png)

set the field Source to VARIO
It would work as well with ALTI or ALTI+, but only the VARIO setting uses the transfered verticcal speed as calculated and transmitted by the openXvario.

## The Limits: the key to your audio generation ##
there are for values for the vario audio tone limits:
lower\_range\_limit,sink\_tone\_start,rise\_tone\_start,upper\_tone\_limit

### The outer limits: The Tone Range ###
The lower and upper limit will be used to define the range for the tone generation.
The range is -10..-3 for the lower and +3..+10 for the upper limit in 1m/s steps . Theses 2 values define the possible range of vertical speeds that will be mapped to different audio results.
If you want to have a sensitive audible feedback, you might want to set these to outer limit of -3 and +3. this will result in all the possible audio pitch and beep speeds to be used for vertical speeds of -3 to +3 m/s
above or below these limits, the tone will then change unchanged.

### The inner limits = Silence Window ###
The range here is -2..1 and -1..+2m/s in 0.1m/s steps These inner values will be used to define a silent area for the vario tone. you can set these for example to -1 to +0.20 . This will tell the vario to be quiet in all vertical speeds between sinking -1m/s to lift of 0.20m/s .

Play around with these to create a vario tone to your liking.

### Configuring your telemetry display ###
![https://openxvario.googlecode.com/svn/wiki/images/Telemetry3.png](https://openxvario.googlecode.com/svn/wiki/images/Telemetry3.png)


configure your telemetry screens to your liking..

# Setting up a switch to turn on the vario sound #
you need to create a custom function in openTX to activate the vario tone generation:

![https://openxvario.googlecode.com/svn/wiki/images/customFunctionVario.png](https://openxvario.googlecode.com/svn/wiki/images/customFunctionVario.png)