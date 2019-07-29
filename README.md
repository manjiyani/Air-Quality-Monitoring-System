# Air-Quality-Monitoring-System
 This project uses arduino online simulator (Tinkercad) with thingspeak to monitor the air quality and provide a statistical report
  
 This project can also be done without online simulation
 
## Components Required (ignore if you are doing it online)

* Arduino Uno

* 16X2 Charater LCD

* ESP8266 Wi-Fi Module

* MQ135 Gas Sensor
 
## Connections

 * LCD RS pin to digital pin 12
 * LCD Enable pin to digital pin 11
 * LCD D4 pin to digital pin 5
 * LCD D5 pin to digital pin 4
 * LCD D6 pin to digital pin 3
 * LCD D7 pin to digital pin 2
 * LCD R/W pin to ground
 * LCD VSS pin to ground
 * LCD VCC pin to 5V
 * 10K resistor:
 * ends to +5V and ground
 * wiper to LCD VO pin (pin 3)
 
## System Architecture
![GitHub Logo](/images/architecture.png)


### For a graphical view of connections please visit https://www.tinkercad.com/things/4bvrgNA91Dt
 
## Air Quality measurement

* Converting air pollutant concentration
1. Converting Micro grams per cubic meter to PPM
ppmv = mg/m^3 x (0.08205 x T) / M 

2. Converting PPM to Micro grams per cubic meter
mg/m^3 = ppmv x M /(0.08205 x T) 

Where,

mg/m^3 = microgram of pollutant per cubic meter of air

ppmv = air pollutant concentration, in parts per million by volume

T = ambient temperature in kelvin

0.08205 = Universal gas constant

M = Molecular weight of air pollutant

## Software and Prerequisites

* Tinkercad.com: 
Go and signup on tinkercad.com(for online arduino simulation) if u want to complete the project online and visit this link for guidance

* Thingspeak.com

Firstly go to thingspeak and signup and login

Then, go to "channels" section and create a new channel

While creating the channel, name it as per your requirements and create only one field named "Air Quality"

Save the channel

After that, go to "API keys" tab under your created channel and save the given API key!

## To understand the code please read the guide.docx file!

## Note: Because of the firewall or an unkown issue i wasn't unable to connect to the thingspeak server but if you are doing it on a hardware it can be easily done! Any further contribution is highly appreciated!

