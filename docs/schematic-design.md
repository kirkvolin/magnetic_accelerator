---
title: Schematic Design
---

## Schematic
![Schematic](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Schematic%20Assets/ESP32%20MQTT%20Schematic.png)

## PCB

![Top](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/simulation_image_top.png)

![Bottom](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/simulation_image_bottom.png)

## ZIP File
[Click here for PDF and ZIP files](https://github.com/kirkvolin/magnetic_accelerator/tree/main/assets/Schematic%20Assets)

## Writeup
This PCB allows input power from 8 pin ribbon cables, USB, or a barrel jack. Any combination of power inputs can be connected together safely through the use of OR diodes. The voltage regulator circuit powers an ESP32-S3, which is the main component of the MQTT subsystem. The ESP32-S3 can be programmed and communicate with a PCB through the use of the ESP32-S3 USB OTG functionality. 

Future iterations of this design would likely include the use of a USB-UART bridge with auto-programming circuitry. This isn't a required feature for functionality, but without it, programming and communicating with the ESP32 can pose some issues based on settings in VSCode. Including the autoprogramming circuitry would allow this board to function similarly to an ESP32 devkit in regards to programming and communication.

I would also use larger breakout headers. The ones that I chose for this iteration are smaller, to minimize board size, but do not function with standard jumper cables and require specialized 24 gauge jumpers. 

This schematic and PCB were created using Altium Designer. 
