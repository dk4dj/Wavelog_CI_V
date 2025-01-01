# Wavelog_CI_V
![image of configuration dialog on ESP32-webserver](https://github.com/user-attachments/assets/be6f4759-350b-4999-8a51-d55a53d7c620)

## Introduction
This is a CI-V Connector for Wavelog that can be running on an Wireless Tag WT32-ETH01 ESP32 developer board.

## Needed hardware
* WT32-ETH01 board
* 3,5 mm jack plug
* some wire
* diode
* 1x 4k7 resistor
* 1x 10k resistor

![How a prototype of a pcb with ESP32 can look like](https://github.com/dg9vh/Wavelog_CI_V/assets/13950650/b69d722d-725e-41cc-ac18-d5fdcf4bf325)

On the image above you see a prototype built on a perforated grid circuit board with an ESP32 development board. A prototype with WT32-ETH01 looks similar.

## Wiring schedule
[Schematics.pdf](/Documents/Schematics.pdf)

## Features
This connects via CI-V to your Icom Transceiver (e.g. IC-7300) on the 3,5 mm jack plug port.
From there it reads following measurements:
* Working frequency
* Working mode
* Working rf-power-level

This values are transported to the radio hardware API of Wavelog (Cloudlog also works) and
there this data can be used for logging purpose.

Also this CI-V Connector is presenting a rudimentary XML-RPC service on port 12345 to be used by 
CloudLogOffline by DL9MJ - you will find this at https://github.com/myzinsky/cloudLogOffline

## Prerequisites
To have this working properly, you need to have your transceiver in "transceive = on"-mode for 
CI-V. Also it should be configured for 19200 baud on the serial output (not on USB-port!).

## Starting from Scratch
First time you start this code it will obtain an IP automatically by DHCP. You can see the IP
on serial debug output or in your router. The configuration dialog could be reached by a webbrowser
using the obtained IP.

On this dialog you configure the URL of your wavelog installation (for example http://wavelog.dg9vh.de)
and the API-endpoint (for example /index.php/api/radio). Also the Wavelog API Key is needed beneath
the CI-V address of your transceiver (for example 0x94 for an IC-7300).

Optional but useful is also to give a description text (this will be shown in Wavelog Hardware 
interface dialog) and an mDNS name. This is useful for getting a hostname instead of an IP 
for communicating with the WT32-ETH01.

Save this and be ready to rumble :-)

## How it's working?
From now on every change of one of the parameters mentioned above this would be transported to
your wavelog instance via the API to be available for logging.

## Credits
Some parts of this code (for example fundamentals of the CI-V-communication) where taken from 
Patric (DF7ZZ) and his "Antennenumschalter ESP32"-code. So thank you Patric for your inspirations!
Also a big thank you to Kim (DG9VH) for publishing his code and the corresponding article in the 
CQ DL magazine.
