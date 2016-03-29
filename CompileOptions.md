# Introduction #

The code of openxvario can be customized to suit your projects needs.
at the beginning of the code file there are quite a lot of "#define xxxxx" statements. if the line starts with "#define" that option is active. if the line starts with "// #define" that option is currently deactivated. Prior to compiling / uploading the programm to the arduino board, you can change these defines in order to adjust the programm to your whishes.

# Details #

## Pin Assignments ##
some of the pin assignments can be changed here. Not all pins are possible for each function, under normal circumstances do not change these.
the PIN_VoltageCell1-6 will define the pins used for reading up to 6 voltages between 0 and 5V. Only if the PINS are defined here, the actual trasmission of the data will take place.
```
#define PIN_SerialTX 10       // the pin to transmit the serial data to the frsky telemetry enabled receiver
// Define a voltagepin if you want to transmit the value to open9x:
//#define PIN_VoltageCell1 0    //  Pin for measuring Voltage of cell 1 ( Analog In Pin! )
//#define PIN_VoltageCell2 1    //  Pin for measuring Voltage of cell 2 ( Analog In Pin! )
//#define PIN_VoltageCell3 2    //  Pin for measuring Voltage of cell 3 ( Analog In Pin! )
//#define PIN_VoltageCell4 3    //  Pin for measuring Voltage of cell 4 ( Analog In Pin! )
//#define PIN_VoltageCell5 6    //  Pin for measuring Voltage of cell 5 ( Analog In Pin! )
//#define PIN_VoltageCell6 7    //  Pin for measuring Voltage of cell 6 ( Analog In Pin! )
```
## Arduino LED PIN/Mode ##
the onboard LED of the Arduino can be used in one of two ways. only one of the 2 options can be defined
```
#define PIN_ClimbLed 13       // the led used to indicate lift for debugging purposes
// Choose how what the led will be used for (only 1 should be defined):
#define LED_BufferBlink       // Blink every time the averaging buffer complets one cycle
//#define LED_ClimbBlink        // Blink when climbRate > 0.15cm
```
## Absolute or relative Altitude display ##
i personally prefer to start with the abolute altitude being displayed in open9x. But open9x allways takes the first received altitude and uses it as an offset. this results in the starting altitude to be displayed as 0 meters.
If you define FORCE\_ABSOLUTE\_ALT, openxvario will overwrite that offset after starting (or reset). This activates the display of the absoplute calculated height in open9x. before you start your plane you can still press ![MENU](MENU.md) on the telemetry dipslay screens to use the current altitude as an offset again.
```
// #define FORCE_ABSOLUTE_ALT // If defined, the height offset in open9x will be resetted upon startup, which results in an absolute height diplay.
                           // If not defined, open9x will use the first transmitted altitude as an internal offset, which results in an initial height of "0m"
```
## MS5611 Sensor I2C address ##
the normal I2C addresses are 0x76 or 0x77 depending on the used modul.
```
const int I2CAdd=0x77;                 // The I2C Address of the MS5611 breakout board ( normally 0x76 or 0x77 configured on the MS5611 module via a solder pin or fixed ...)
```
## Size of the circular buffer ##
The size of the circular buffers can be changed by this constant.
Bigger Values: More stable behaviour, but also a little slower in reaction time
Smaller Values: Faster reaction to altitude changes, but also more noise._

  * 12 is very fast reacting but with more jitter;
  * 25 is a little slow, but quite stable;
  * 100 is dead slow, but you could almost use it for height measurements in cm ;-)

The altitude and the ClimbRate will normally be transmitted once every 200ms. By changing the LED Mode to LED_BufferBlink, you can visually see every time the circular buffer completed one fill round. ideally it should take as well around 200ms to complete one full circle._

```
const int AverageValueCount=15;        // the number of values that will be used to calculate a new verage value
```
## Analog ClimbRate Mode ##
see AnalogClimbRate for details
```
//#define ANALOG_CLIMB_RATE   // If defined, the climb rate will be written as PWM Signal to the defined port( Only use if you have to use a receiver missing the serial connection)
#define OutputClimbRateMin = -3; 
#define OutputClimbRateMax = 3;
#define PIN_AnalogClimbRate 9 // the pin used to write the data to the frsky a1 or a2 pin (could be 3,5,6,9,10,11)
```
## absolute Altitude / air pressure in additional Fields ##
All transmitted data can be activate/deactivated. choose via the following deines which data you want to transmitt to which field:
```
#define SEND_Alt        // Send alt in the altitude field
#define SEND_VERT_SPEED // Send vertical speed (climbrate) as id 0x38
#define SEND_VREF       // Voltage Reference as cell0
#define SEND_VFAS_NEW   // Voltage as VFAS untested! supposed to work in the next release of open9x
#define SEND_TEMP_T1    // MS5611 temperature as Temp1
//#define SEND_TEMP_T2    // MS5611 temperature as Temp2
//#define SEND_AltAsRPM   // Altitude in RPM ;-)
#define SEND_AltAsDIST  // Altitude in DIST
//#define SEND_PressureAsDIST // pressure in DIST field
#define SEND_PressureAsRPM  // pressure in RPM Field
```