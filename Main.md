# Introduction #
If you found this page, you are probably as well infected by the "build your own Variometer" virus.
The openXvario is my contribution to the 9X community.
It is designed to work together with the open source firmware open9x for the turnigy 9x transmitter. but with little modifications it should work with any Fr-Sky telemetry enabled system.

Discussion about this project: http://9xforums.com/forum/viewforum.php?f=86

## Arduino Variometer / Altimeter over FR-Sky telemetry for open9x ##
High sensitive variometer/altimeter with a resolution better than +/-10cm.
The sensitivity can be adjusted via your trasnimtter.

The following data can be transmitted via the frsky telemetry protocoll for display in e.g. open9x:

  * absolute altitude (ID 0x10 and 0x21)
  * vertical speed
  * supply voltage as VFAS Voltage ( id 0x39)
  * temperature (from MS5611) as T1 ID 0x02
  * absolute air pressure
  * 6 single voltage values connected to the pins as configured as cell 1-6 in id 0x06
  * various other field for diagnostic purposes (e.g. internal kalman filter parameters)

## Building your own ##
visit the BuildInstructions page to learn how to make an openXvario yourself.

## Current Sensor Module support ##
It is now possible to connect a current sensor module to your openXvario as well. visit the Wiki Page CurrentSensorModules for details

## Configuring open9x ##
visit the ConfigureVarioSettingsInOpen9x to learnm how to set the configuration in open9x
## Remote control your openXvario ##
Control the sensitivity of the vario from your transmitter.
see the RemoteControlYouVario page for details


## Credits ##
I got the idea and a lot of code for this project from this thread: http://www.rcgroups.com/forums/showthread.php?t=1749208

The code to write the frsky packages is based on the work in this thread: http://fpv-community.de/showthread.php?18566-FrSky-Telemetrie-Protokoll

The voltage calibration code ist from here: http://provideyourown.com/2012/secret-arduino-voltmeter-measure-battery-voltage/

The kalman filter is based on the information from this site: http://interactive-matter.eu/blog/2009/12/18/filtering-sensor-data-with-a-kalman-filter/

and many thanks to bertrand for the changes to open 9x!

### Sensor data send to open9x ###
here´s an example how it might look in open9x:
![https://openxvario.googlecode.com/svn/wiki/images/open9xTelemetryScreen.jpg](https://openxvario.googlecode.com/svn/wiki/images/open9xTelemetryScreen.jpg)

  * ALT => the relative altitude
  * VSpd => the vertical speed
  * Dist => 279.22 the absolute height as calculated form air pressure+temp
  * Cels => the input voltage of the arduino
  * RPM => 1056 mbar = the current air pressure (not the best resolution in this field...)
  * T1 => 25C the temperature measured by the ms5611
the dist and RPM fields are being "misused" a bit here :D

You can configure this to your liking by just uncommenting some lines in the code. e.g. you can choose what you want in the dist or RPM field: nothing, Altitude,Air pressure..
![https://openxvario.googlecode.com/svn/wiki/images/Prototype2.jpg](https://openxvario.googlecode.com/svn/wiki/images/Prototype2.jpg)

![https://openxvario.googlecode.com/svn/wiki/images/Prototype2Back.jpg](https://openxvario.googlecode.com/svn/wiki/images/Prototype2Back.jpg)

Hint: this prototype is not using the ppm signal from the receiver. new pictures will follow..
### Other useful information ###
  * Macca55 found out that the sensor is quite sensitive to direct sunlight. read here: http://openrcforums.com/forum/viewtopic.php?f=86&t=2629&sid=98c8fe9a88ae3303e047b59c4a3fb69a&start=240#p48371