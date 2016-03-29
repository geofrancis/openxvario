# This project has moved to GitHub: [openXsensor new home](https://github.com/openXsensor/openXsensor) #















![https://openxvario.googlecode.com/svn/wiki/images/openXvario_big_bow800x227.png](https://openxvario.googlecode.com/svn/wiki/images/openXvario_big_bow800x227.png)

An Arduino based vario and (optional current sensor) for openTX/ 9X / FrSky Taranis and more...


If you like this project you might want to consider donating a small amount:

![https://www.paypalobjects.com/de_DE/DE/i/btn/btn_donateCC_LG.gif](https://www.paypalobjects.com/de_DE/DE/i/btn/btn_donateCC_LG.gif)

[Paypal Donate](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4GNGDMV5VP2US)

have a look here for more information: https://code.google.com/p/openxvario/wiki/Main

![https://openxvario.googlecode.com/svn/wiki/images/Prototype2.jpg](https://openxvario.googlecode.com/svn/wiki/images/Prototype2.jpg)
![https://openxvario.googlecode.com/svn/wiki/images/Prototype2Back.jpg](https://openxvario.googlecode.com/svn/wiki/images/Prototype2Back.jpg)
![https://openxvario.googlecode.com/svn/wiki/images/openXvario_D4R-II.jpg](https://openxvario.googlecode.com/svn/wiki/images/openXvario_D4R-II.jpg)

This is a combination of a FRSky D4R-II wit a openXvario directly connected to it.
Doesn't add much size and weight, but quite a bit of funtionality.
![http://openxvario.googlecode.com/svn/wiki/images/open9xTelemetryScreen.jpg](http://openxvario.googlecode.com/svn/wiki/images/open9xTelemetryScreen.jpg)

  * ALT => the relative altitude
  * VSpd => the vertical speed
  * Dist => 279.22 the absolute height as calculated form air pressure+temp
  * Cels => the input voltage of the arduino
  * RPM => 1056 mbar = the current air pressure (not the best resolution in this field...)
  * T1 => 25C the temperature measured by the ms5611

the dist and RPM fields are being "misused" a bit here :D

you can configure this to your liking by just uncommenting some lines in the code.
e.g. you can choose what you want in the dist or RPM field: nothing, Altitude,Air pressure..