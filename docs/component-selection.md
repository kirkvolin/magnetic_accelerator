---
title: Component Selection
---

## Team Role

My role in the team is the bidirection internet communication subsystem using MQTT protocol. For this subsystem, I will be using an ESP32-S3-WROOM-1-N4 surface mounted on a custom PCB. This subsystem will include UART to communicate with the sensor, actuator and human interface subsystems. The UART connection for human interface will be included for debugging and redundancy, as we are planning implementation of a wireless interface device which would communicate over the MQTT protocol. With this implementation, my device would be responsible for receiving and sending data over MQTT with the human interface device, and sending and receiving data from the senor and actuator subsystems. The communications will be used to control the speed and direction of a metal marble on a track through the use of copper coils to demonstrate magnetism, and sensor data received will provide position and velocity information to the interface device.


## Component Selection - Bidirectional Internet Communication

### Power Regulator

| Solution 1  | Pros                                                                                        | Cons                                      |
|:-----------:|:-------------------------------------------------------------------------------------------:|:-----------------------------------------:|
|LM2576HVS-3.3| 3.3V Fixed Output                                                                           |   Most Expensive                          |
|![LM2576HVS-3.3](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2575HVS-3.3.png)             | Large footprint makes hand soldering easier                                                 |   Unfamiliar Manufacturer                 |
|[Digikey](https://www.digikey.com/en/products/detail/umw/LM2576HVS-3-3/16705917)             | Requires minimal external components                                                        |   Somewhat confusing component datasheet    |
|             | High current output allows more components to operate from this regulator if needed.        |                                           |

| Solution 2 | Pros                                                                                          |Cons                                      |
|:----------:|:---------------------------------------------------------------------------------------------:|:----------------------------------------:|
|LM2574M-3.3 | 3.3V Fixed Output | Not a lot of extra current available for expanding the system|
|![LM2574M-3.3](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2674M-3.3.png)| Pins have good spacing for hand soldering | Smallest component that could likely be hand soldered|
|[Digikey](https://www.digikey.com/en/products/detail/texas-instruments/LM2674M-3-3-NOPB/287129)|Small footprint can be good for board design|  |
|         | Cheapest option               | |
|        |  Easy to follow datasheet

|Solution 3 | Pros                                                                                          |Cons                                      |
|:----------:|:--------------------------------------------------------------------------------------------:|:----------------------------------------:|
|LM2676S-3.3 | Clear datasheet  | Single sided pins are close together, making hand soldering more difficult |
|![LM2676S-3.3](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2676S-3.3.png)| Large footprint make it easy to handle | More expensive than another option |
|[Digikey](https://www.digikey.com/en/products/detail/texas-instruments/LM2676S-3-3-NOPB/363809) |Plenty of excess amperage available if needed| Larger footprint takes up more space on PCB|

|Solution 4 | Pros                                                                                          |Cons                                      |
|:----------:|:--------------------------------------------------------------------------------------------:|:----------------------------------------:|
|LM2595S-3.3 | Clear datasheet  | Single sided pins are close together, potentially making hand soldering more difficult |
|![LM2676S-3.3](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2595S-3.3.png)| Large footprint make it easy to handle | More expensive than another option |
|[Digikey](https://www.digikey.com/en/products/detail/texas-instruments/LM2595S-3-3-NOPB/363698) |Exceeds amperage requirement peak of 500mA for ESP32, but not as excessively as other options available| Larger footprint takes up more space on PCB|

#### Selection

For a power regulator, the LM2595S seems to be the optimal solution. It offers a good combination of price, usability, and versatility.
Because of it's lower minimum input voltage of 4.5V, it enables the use of USB as a source of power compared to the LM2675M and LM2676S which wouldn't be able to accomplish this due to their minimum requirements of 6.5V and 8V respectively. The regulator's size of the TO263CA standard will also be much easier to manipulate and place for surface mount hand soldering.

#### Application
![Typical Application](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2595S%20Typical%20Application.png)
![Buck Regulator](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2595S%20Buck%20Regulator.png)
#### Footprint
![Footprint](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/LM2595S%20Package.png)

### Power Input

|Solution 1 | Pros                                                                                          |Cons                                      |
|:----------:|:--------------------------------------------------------------------------------------------:|:----------------------------------------:|
|Barrel jack |Consistent power | Need access to power outlets| 
|![Barrel Plug](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/Barrel%20Plug.png)| Easy to implement | Separate cable required|
|[Digikey](https://www.digikey.com/en/products/detail/tensility-international-corp/54-00165/10459297)|||

|Solution 2 | Pros                                                                                          |Cons                                      |
|:----------:|:--------------------------------------------------------------------------------------------:|:----------------------------------------:|
|USB |Consistent power | Need access to power outlet or PC|
|![USB B](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/Micro%20USB%20B.png)| Relatively easy to implement | Separate cable required|
|[Digikey](https://www.digikey.com/en/products/detail/amphenol-cs-fci/10118193-0001LF/2785388)|USB B/C are extremely common| Soldering can be tricky, esp. USB C |
||Can provide both power and data||

|Solution 2 | Pros                                                                                          |Cons                                      |
|:----------:|:--------------------------------------------------------------------------------------------:|:----------------------------------------:|
|Onboard Battery |Portability | Need backup batteries/charger|
|![Battery](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Component%20Selection/18650%20Battery.png)| Relatively easy to implement | Would increase board size significantly or require separate board for power|
|[Digikey](https://www.digikey.com/en/products/detail/sparkfun-electronics/PRT-12895/5271298)|| Much more expensive to implement |
||||

#### Selection

For powering this subsystem, I feel that versatility is important. Because USB is already required to program the ESP32 chip, I will design the circuit board so that it can be powered from either the USB connector or a separate 5.5x2.5mm barrel jack which is a common standard that my teammates and I already have cables for through the Robotics 1 and 2 courses through the Robotics 1 and 2 courses.

### ESP 32 

| ESP Info                                      | Answer |
| --------------------------------------------- | ------ |
| Model                                         | ESP32-S3-WROOM-1-N4      |
| Product Page URL                              | [Product Page](https://www.espressif.com/en/products/socs/esp32-s3)|
| ESP32-S3-WROOM-1-N4 Datasheet URL             | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)|
| Reference Manual                              | [Reference Manual](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf)|
| Vendor link                                   | [Digikey](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1-N4/16162639)      |
| Code Examples                                 | [Code Examples](https://github.com/espressif/esp-idf/tree/master/examples)      |
| External Resources URL(s)                     | [External Resources](https://esp32io.com/tutorials/esp32-code-structure)      |
| Unit cost                                     | $2.95      |
| Absolute Maximum Current for entire IC        | 500mA      |
| Supply Voltage Range                          | 3.0-3.6V      |
| Maximum GPIO current (per pin)                | 40mA      |
| Supports External Interrupts?                 | Yes      |
| Required Programming Hardware, Cost, URL      | None needed, ESP32-S3 is programmable through USB OTG|

#### Pin Requirements

| Module         | # Available | Needed | Associated Pins (or * for any) |
| -------------- | ----------- | ------ | ------------------------------ |
| Power          | 2           | 2      | 3V3, EN                        |
| Ground         | 2           | 2      | GND, GND                       |
| UART           | 3           | 2      |GPIO43 ~ GPIO44, GPIO17 ~ GPIO18|
| External SPI   | 4           | 0      | N/A                            |
| I2C            | 2           | 0      | N/A                            |
| GPIO           | 45          | 3      | *                              |
| ADC            | 2           | 0      | N/A                            |
| LED PWM        | 5           | 5      | *                              |
| Motor PWM      | 0           | 0      | N/A                            |
| USB Programmer | 1           | 1      | GPIO19 ~ GPIO20                |

#### Pinout
![Pinout](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/ESP32%20Pinout.png)
![Pin Table 1](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/ESP32%20Pin%20Definitions%201.png)
![Pin Table 2](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/ESP32%20Pin%20Definitions%202.png)

#### Footprint
![Footprint](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/ESP32%20Pin%20Dimensions.png)

#### USB OTG

![USB OTG](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/ESP32%20USB%20OTG.png)

#### UART

![UART](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/UART%201.png)
![UART2](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/UART%202.png)

#### LED PWM

![LED](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/LED%201.png)
![LED2](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/ESP32/LED%202.png)


### General Components

All surface mount components such as resistors, capacitors, etc. are planned to use 0805 standard for ease of handling and soldering.

### Power Budget
![Power Budget 1](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Power%20Budget/Power%20Budget%201.png)
![Power Budget 2](https://raw.githubusercontent.com/kirkvolin/magnetic_accelerator/main/assets/Power%20Budget/Power%20Budget%202.png)


With this subsystem, the primary power draw is the ESP32-S3. I allowed an extra 50% current capacity minimum when selecting my voltage regulator to ensure that my subsystem was capable of powering the ESP32 and any additional components that might be added through design and integration.

