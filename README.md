# Openhab-Room-Humidifier
Activates and deactivates a room humidifier based on indoor humidity and outdoor temperature. Uses MQTT and Arduino.

## Hardware:
Digital Temperature and Humidity sensors DHT22/AMC2302 or equivalent  
Raspberry Pi running Openhab (an open source home automation program)  
Arduino Unos or equivalent (I used Arduino Nanos with a Nano IO shield, which included a socket for an NRF24L radio module)  
Arduino Mega 2560  
Power supplies for Arduino and Raspberry Pi  
Relays rated for mains voltage  
NRF24L01 radio modules  

Wire, solder, shrink tubing, misc. electronic parts.  

## Software:
Openhab for Raspberry Pi (www.openhab.org)  
MySensors Arduino library (www.mysensors.org)  
MQTT server running on the Raspberry Pi.  

## Overall design:
Arduino Nanos read individual DHT11 sensors and send the readings by radio (NRF24L01) to the Arduino Mega. The Mega connects by
ethernet cable to a network switch, to which the Raspberry Pi is also connected. The Pi accepts the payload of data from the Mega
through an MQTT protocol. Using this protocol, the Pi makes the data available to other nodes in the network that request it.
The payload data is stored and updated by the Pi whenever it is sent by a node and sent whenever it is requested. 

## Adjusting indoor humidity:
In the winter, experts recommend maintaining about 50% humidity indoors. On very cold days, however, humidity might condense
on interior windows and walls, and the difference in humidity between indoors and outdoors might cause humidity to migrate
through walls. The humidity migrating across the walls would then condense as it approaches the cold outdoor temperature, causing
water (and eventually mold) to collect within the walls. HVAC professionals recommmend homeowners to decrease indoor humiditiy as
the exterior temperature decreases in order to reduce the difference between indoor and outdoor humidity.

Proper ajustment of indoor humidity therefor requires both indoor and outdoor temperature readings. This home automation project
1) takes indoor and outdoor temperature readings from a DHT sensor
2) takes indoor humidity levels from a DHT sensor
3) calculates the recommended interior humidity level
4) turns on a room humidifier if the humidity level is too low
5) turns off the room humidifier when the recommended humidity level is reached.

A complete description of hardware, Openhab, MQTT and MySensors setup is beyond the scope of this ReadMe. 
