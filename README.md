# Air-Quality-Monitoring-System
 This project uses arduino online simulator (Tinkercad) with thingspeak to monitor the air quality and provide a statistical report
  
 This project can also be done without online simulation
 
 #Components Required (ignore if are doing it online)
 
 Arduino Uno
 16x2 Character LCD
 ESP8266 Wi-Fi Module
 MQ135 gas sensor
 
 As the device is powered, the Arduino board loads the required libraries, flashes some initial messages on the LCD screen and start sensing data from the MQ-135 sensor. The sensor can be calibrated so that its analog output voltage is proportional to the concentration of polluting gases in PPM. The analog voltage sensed at the pin A0 of the Arduino is converted to a digital value by using the in-built ADC channel of the Arduino. The Arduino board has 10-bit ADC channels, so the digitized value ranges from 0 to 1023. The digitized value can be assumed proportional to the concentration of gases in PPM. The read value is first displayed on LCD screen and passed to the ESP8266 module wrapped in proper string through virtual serial function. The Wi-Fi module is configured to connect with the ThingSpeak IOT platform. ThingSpeak is an IOT analytics platform service that allows to aggregate, visualize and analyze live data streams in the cloud. ThingSpeak provides instant visualizations of data posted by the IOT devices to ThingSpeak server.

The Wi-Fi module can be connected with the ThingSpeak server by sending AT commands from the module. The module first test the AT startup by sending the AT command. Then, command is passed by the controller to the Wi-Fi module using software serial function. In response to the command 'AT', the platform must respond with 'OK' if the cloud service is running.
Then, the AT command to view the version information is passed.
AT + GMR 
In response to this command, the IOT platform must respond by sending back the version information, SDK version and the time bin is compiled.
1. ESP-01 output : it will be 00160901.
2. ESP-12 output : it will be 00180000902-AI03.
Next, the AT command to set the connection to Wi-Fi mode is send.
 AT + CWMODE = 3
By setting the parameter in CWMODE to 3, the Wi-Fi connection is configured to SoftAP as well as station mode. This AT command can take three parameters
1 - set Wi-Fi connection to station mode
2 - set Wi-Fi connection to SoftAP mode
3 - set Wi-Fi connection to SoftAP + station mode
In response to this command, the IOT platform must send back the string indication the Wi-Fi connection mode set.
Next, the AT command to reset the module is send.
AT + RST
In response to this command, the Wi-Fi module must restart and send back a response of 'OK'. After resetting the module.
Next, command to setup multiple connections is AT+ CIPMUX.
 AT + CIPMUX=1  
This AT command can take two parameters - 0 for setting single connection and 1 for setting multiple connections.
Next, the command to connect with the Access Point (AP) is passed which takes two parameters where first parameter is the SSID and the other parameter is the password.
AT+CWJAP=\"SSID\",\"Password\"
Next, the AT command to get local IP address is passed.
 AT + CIFSR
In response to this command, the local IP address of the Wi-Fi connection is sent back by the module. Now, the module is ready to establish TCP IP connection with the ThingSpeak server. The controller reads the sensor data and store it in a string variable.
The TCP IP connection is established by sending the following AT command
 AT + CIPSTART = 4, "TCP", "184.106.153.149", 80 
The AT + CIPSTART command can be used to establish a TCP connection, register an UDP port or establish an SSL connection. Above command is used to establish a TCP IP connection. For establishing a TCP-IP connection, the command takes four parameters where first parameter is link ID which can be a number between 0 to 4, second parameter is connection type which can be TCP or UDP, third parameter is remote IP address or IP address of the cloud service to connect with and last parameter is detection time interval for checking if the connection is live. If the last parameter is set to 0, the TCP keep-alive feature is disabled otherwise a time interval in seconds range from 1 to 7200 can be passed as parameter. In response to this command, the server must respond with 'OK' if connection is successfully established otherwise it should respond with message 'ERROR'.
When the connection with the server is successfully established and the controller has read the sensor value, it can send the data to the cloud usingAT+CIPSEND command.
AT + CIPSEND = 4  
This command takes four parameters, where first parameter is the link ID which can be a number between 0 to 4, second parameter is data length which can be maximum 2048 bytes long, third parameter is remote IP in case of an UDP connection and remote port number in case of UDP connection. The third and fourth parameter are optional and used only in case of UDP connection with the server. Since, the TCP IP connection is established, these parameters are not used. The command is followed by a string containing the URL having the field names and values passed through the HTTP GET method.
In this project, a string containing the URL having API Key and the sensor value as the field and value is passed. The passed field and its value are logged on the cloud server. It is important to pass the API key in this URL as one of the field value in order to connect with the registered cloud service. The Air quality measured by sensor can now be monitored and recorded through the ThingSpeak IOT platform.

 
