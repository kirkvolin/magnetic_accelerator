# EGR314 Individual Report — Magnetic Accelerator

Kirk Volin · ASU Polytechnic · Robotics Engineering · Spring 2025

This site documents my individual subsystem contribution to the EGR314 team project: a **magnetic accelerator** that propels a metal marble along a track using timed electromagnetic coils. My subsystem handles **bidirectional internet communication** via MQTT protocol using an ESP32-S3-WROOM-1-N4 on a custom PCB.

## Site Contents

| Page | Description |
|------|-------------|
| [Block Diagram](docs/block-diagram.md) | Subsystem layout, pin callouts, and communication overview |
| [Component Selection](docs/component-selection.md) | Power regulator, power input, and ESP32 selection with trade-off analysis |
| [Schematic Design](docs/schematic-design.md) | Altium schematic, PCB renders, and design notes |
| [BOM and Hardware Order](docs/hardware-order.md) | Bill of materials and purchase order |
| [API](docs/api.md) | UART/MQTT message format, team byte definitions, and flow diagrams |
| [Resources](docs/resources.md) | ESP32 firmware source code download |

## Subsystem Overview

- **Microcontroller:** ESP32-S3-WROOM-1-N4
- **Communication:** MQTT over WiFi (upstream); UART (downstream to sensor, actuator, HMI subsystems)
- **Power:** LM2595S-3.3 buck regulator; accepts USB, barrel jack (5.5×2.5 mm), or ribbon cable input
- **PCB:** Custom surface-mount board designed in Altium Designer; 0805 passives throughout

## Built With

- [Altium Designer](https://www.altium.com/) — schematic and PCB design
- [ESP-IDF](https://github.com/espressif/esp-idf) — ESP32 firmware framework
- Fusion 360
- 3D Printing
## Team

[Team 310's Website](https://asu-egr314-2025-s-310.github.io/)
