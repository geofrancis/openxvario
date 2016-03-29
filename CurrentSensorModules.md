# openXvario+C #

## Current sensor support in openXvario ##

There are plenty of real cheap current sensor modules available on eBay from far east sellers. Prices start at something between 2 and 3€ for a bidirectional current sensor in the +/- 5A,20A or 30A range.
![https://openxvario.googlecode.com/svn/wiki/images/ACS712%20current%20sensor%20module.png](https://openxvario.googlecode.com/svn/wiki/images/ACS712%20current%20sensor%20module.png)

Now you can directly connect these cheap current sensor modules to your openXvario.

![https://openxvario.googlecode.com/svn/wiki/images/CurrentSensorRepackaged.png](https://openxvario.googlecode.com/svn/wiki/images/CurrentSensorRepackaged.png)

this is a +-5A sensor repackaged for use in one of my DLG Gliders:



In open9x/openTx/Frsky Taranis this should enable the following telemetry fields:

CNSP => the consumed capactiy in mAh (calculated from current+time)
Curr => the current being measured
Watt => the current power... (  a measured voltage measured via A1/A2 as well)

## Connecting the current sensor modules to your openXvario ##
```
     Arduino GND   --------------------- Current Sensor Module GND 
     Arduino VCC   --------------------- Current Sensor Module VCC
     Arduino A2    --------------------- Current Sensor Module OUT
```

## Sensor types that should work ##
the oXv expects a uni or bi-directional current sensor with a linear voltage output representing the measured current.
most current sensor should be OK for this.
the sensors i tested can be powered directly from the arduino boards GND+VCC pin for this they have to accept an input voltage of 5V

A current sensor with a linear voltage relative to the measured output can be connected to the openXvario.
This has been tested using 3 different types of ACS712 Current sensor modules that can be purchased for 2-3€ from various far east ebay sellers.
these modules are bidirectional sensors

## Configuring the openXvario code for the current Sensor ##
the followin section of the souece code can be modified to configure the parameters needed for the current sensor functionality
```
/***************************************************************************************/
/* Optional Feature Current Mesaurement                                                */
/* Uncomment the #define sendCurrent toenable this feature.                            */
/***************************************************************************************/
#define SendCurrent  // Uncomment to enable a connected Current Sensor
#define MinCurrentMilliamps -37879    // the lowest measured current (=0v input voltage)
#define MaxCurrentMilliamps 37879     // the hioghest measured current (= input voltage= vRef)

#define ForceAbsolutCurrent  // If defined, all measured current values will be forced to be positive (e.g.:-4.5A => +4.5A)
//Here are some example values for standard ACS712 types of sensors
// Sensor Type    Min    Max     
// -5A  .. +5A   -13510  13510 
// -20A .. +20A  -25000	 25000
// -30A .. +30A  -37879	 37879
```

The pin to connect the signal line from the sensor module can be configured by changing this line in the config section:
```
#define PIN_CurrentSensor   2  // the Analog pin the optional current Sensor is connected to 
```
the "2" is the number of the Analog input pin to be used.

## calculating the min/max values for other sensor types ##
![https://openxvario.googlecode.com/svn/wiki/images/CurrentSensorCalculation.png](https://openxvario.googlecode.com/svn/wiki/images/CurrentSensorCalculation.png)

i prepared a little spreadsheet you can use to calculate the min/max values for other sensor types.
you can download the spreadsheet here: https://code.google.com/p/openxvario/source/browse/wiki/Other/openXvario%20Current%20Sensors.xlsx

## Capacity Measuring ##
as the current implementation of the current metering & mAh calculation in openTx only works with a resolution of 100mAh, i have implemented a openXvario internal capacity calculation with a higher precision. This can be used to calculate capacities down to a mAh scale.
The count of capacity will be started with 0mAh each time the oXv gets powered up.
The calculated value can be transmitted in the DIST field to openTX by
uncommenting the following define:
```
#define SEND_mAhAsDist
```

This enables the use of real capacity monitoring in models using very small batteries like DLGs or micro planes.

## Adding a filter capacitor ##
note: this is optional and not required for the sensor to work... it just gives better results...
One tip for the chinese ACS-712 modules:
The modules i bought from various chinese ebay sellers all came without a filter capacitor installed. The datasheet documents the possibility to add a filter capacitor to the circuit. I manually soldered a small 47nF SMD capacitor directly on the 2 pins GND and Filter of the ACS712 on my 5A board. This greatly reduces noise and therefore increases the precision of the sensor. So my recommendations is to install this capacitor!

Heres a pic showing where to install it:

![https://openxvario.googlecode.com/svn/wiki/images/acs712filter.png](https://openxvario.googlecode.com/svn/wiki/images/acs712filter.png)

And here is a picture taken by flaps showing how to mount it:

https://openxvario.googlecode.com/svn-history/r183/wiki/images/ACS712WithCapacitor.JPG

Some of the coating on the ground plane was removed to fit the capacitor and allow easy soldering.

Rainer.