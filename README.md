Arduino-Temp-Logger
=================

Arduino temperature logger is a wireless temperature measurement unit which will send measured
temperature values via 433MHz RF link to Arduino gateway. The Arduino gateway will pass the measurement
values to Domoticz via MQTT protocol.

More information about the system can be found from [Domoticz forum](http://www.domoticz.com/forum/viewtopic.php?f=38&t=7389)

More information about Arduino Domoticz Gateway can be found via following link:

[Arduino-Domoticz-Gateway](https://github.com/MikaPetteriLundgren/Arduino-Domoticz-Gateway)

Arduino-Temp-Logger sketch will need following HW and SW libraries to work:

**HW**

* Arduino
* DS18B20 temperature sensor
* DS1307 RTC
* TX433N RF transmitter

**Libraries**

* DallasTemperature for DS18B20 temp sensor
* Wire for I2C communication
* OneWire for communication with DS18B20 sensor
* VirtualWire for RF communication
* RTClib for RTC functionality
* Narcoleptic for sleep functionality

**HW connections**

DS1307 RTC is connected to Arduino via I2C bus.
Temperature readings are read from DS18B20 digital temperature sensor via OneWire bus.
TX433N RF transmitter is connected to the Arduino via single GPIO pin.

This repository includes also breadboard and schematics pictures in PDF and Fritzing formats.

**Functionality of the sketch**

Sketch reads current time from the RTC clock and checks is it time to run temperature measurement function.
After the temperature value is measured, value will be added to the data string with IDX and dtype values.
The data string is then converted to char array and sent to Arduino based gateway via 433MHz RF link  which will then send the 
data to the MQTT server. So this sketch doesn't send temperature and humidity data directly to the MQTT server.

There is also a sleep function in main loop which will decrease overall power consumption.

It's possible to print amount of free RAM memory of Arduino via serial port by uncommenting `#define RAM_DEBUG` line