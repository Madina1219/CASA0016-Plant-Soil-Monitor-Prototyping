📖 Introduction

Tomato plants are particularly sensitive to inconsistent watering, which can lead to physiological disorders such as blossom-end rot or root stress. 
For beginner growers, maintaining an optimal and consistent soil moisture level can be challenging when relying solely on visual judgement or habit.

This project presents a low-cost, automated tomato soil monitoring and irrigation system that objectively measures soil conditions and responds in real time. 
The system continuously monitors soil moisture, displays live status feedback, and automatically activates irrigation only when required, while also protecting the pump through independent water-level monitoring.

📸 Prototype image:
[IMG_5063](https://github.com/user-attachments/assets/39c09915-b060-415c-ba5a-b2462c258738)

🎥 Prototype Testing Video

A short demonstration video showing live sensor readings, pump activation, and LCD feedback during testing is available below:

▶ System testing video:https://github.com/Madina1219/CASA0016-Plant-Soil-Monitor-Prototyping/blob/main/Tomato%20Soil%20Monitor%20Prototype%20Images/System%20Testing%20.zip


🎯 Project Objectives

The system was designed to:

- Support consistent irrigation for tomato plants
- Reduce human error in watering decisions
- Demonstrate IoT principles using simple, accessible hardware
- Enable safe, portable, and beginner-friendly deployment

🧠 System Overview

The Tomato Soil Monitor operates as a closed-loop control system that:

- Monitors soil moisture using a capacitive sensor
- Checks reservoir water availability independently
- Displays real-time system status on an RGB LCD
- Triggers a short, controlled irrigation pulse when soil is dry
- Prevents pump operation if the reservoir is empty

🧰 Hardware Components

- Microcontroller: Arduino Uno
- Sensors:
.Capacitive Soil Moisture Sensor
.Water Level Sensor
- Actuators:
.5V Relay Module
.Submersible Water Pump
- Display: LCD1602 RGB (I2C)
- Power Supply:
.USB / 9V for Arduino logic
.External battery pack for pump
- Enclosure:
.Repurposed plastic tool caddy (chosen for splash resistance, portability, and separation of wet/dry components)

⚡ Circuit & Power Design

The system uses a split-power architecture to improve safety and reliability:

-Arduino (5V): Sensors + LCD
-External Battery: Pump (via relay)

Wiring Summary
Component	Connects To
Arduino 5V / GND	Breadboard rails
Soil Moisture Sensor	+, –, A0
LCD1602 RGB	+, –, SDA, SCL
Relay Module	+, –, Pin 7
Pump	Battery +, Relay COM
Battery –	Relay NO
Water Level Sensor	+, –, A1


⚙️ Configuration & Calibration

Sensor readings are mapped from raw analog values (0–1023) to a 0–100% scale, enabling intuitive threshold-based decisions.

Operating Thresholds:
.Dry soil (irrigation trigger): < 20%
.Over-watered warning: > 70%
.Low reservoir protection: < 20% (pump disabled)

Calibration Values (Example)
// Soil sensor calibration
const int SOIL_RAW_DRY = 900;   // Sensor in air
const int SOIL_RAW_WET = 300;   // Sensor in water

// Water level sensor calibration
const int WATER_RAW_EMPTY = 0;  
const int WATER_RAW_FULL  = 650;

These values should be recalibrated based on soil type, sensor variation, and container size.

🧪 Testing & Limitations

During live testing, the system successfully demonstrated:

-Responsive soil moisture detection
-Accurate pump triggering and cut-off
-Clear real-time LCD feedback

However, the project also highlighted common physical-computing challenges:

-Sensor variability requiring careful calibration
-Fragility of jumper-wire connections during movement
-Time pressure during live demonstrations
-These observations informed future design improvements.

🚀 Future Improvements

-Weather-sealed connectors and soldered wiring
-Data logging and MQTT publishing
-Mobile or web-based dashboard
-Predictive watering using historical data
-Solar-powered deployment


👤 Author

Madina Diallo
MSc Connected Environments – UCL
