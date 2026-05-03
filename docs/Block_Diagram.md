---
title: Block Diagram
---

##Block Diagram: Bidirectional Internet Communication

This chart shows the general layout and functionality that is required to operate the internet communication subsystem. It includes components for debugging as well as pin call outs for each connection. 

![Block Diagram](assets/Block Diagram/Volin Block Diagram.png)

The block diagram was designed to include upstream and downstream headers for shared power and UART communication through multiple systems. USB OTG is used to program this board and send information from the board to a PC. Debugging LEDs were included to show when lines of code are reached, such as when a message is received from another system or when an error occurs. This board uses the ESP32 to communicate wirelessly to the MQTT server through WiFi. 
