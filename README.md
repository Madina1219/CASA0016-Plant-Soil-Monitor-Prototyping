# Tomato Soil Monitor 🍅💧

An automated plant care system designed specifically for tomato plants. This device monitors soil moisture levels and automatically waters the plant when necessary, while also tracking the water reservoir level to protect the pump.

## 📖 Project Overview
Tomatoes are sensitive to inconsistent watering. This project solves that problem by creating a closed-loop system that:
1.  **Monitors** soil moisture in real-time.
2.  **Visualizes** data on an LCD screen.
3.  **Automates** watering via a relay and pump.
4.  **Protects** the hardware by sensing low water levels in the reservoir.

## 🧰 Hardware Components
* [cite_start]**Microcontroller:** Arduino Uno [cite: 16]
* **Sensors:**
    * [cite_start]Capacitive Soil Moisture Sensor [cite: 23]
    * [cite_start]Water Level Sensor [cite: 70]
* **Actuators:**
    * [cite_start]5V Relay Module [cite: 46]
    * [cite_start]Submersible Water Pump [cite: 56]
* [cite_start]**Display:** LCD1602 RGB Module (I2C) [cite: 33]
* **Power:**
    * 9V/USB for Arduino Logic
    * [cite_start]External Battery Pack for Pump [cite: 63]
* [cite_start]**Enclosure:** Repurposed plastic tool caddy (chosen for water resistance and portability) 

## ⚡ Circuit Wiring
The system uses a split power supply: the Arduino powers the sensors and screen (5V), while the battery pack powers the pump via the relay.

| Component | Pin | Arduino/Connection | Function |
| :--- | :--- | :--- | :--- |
| **Soil Sensor** | AOUT | [cite_start]A0 [cite: 31] | Sends moisture readings |
| **Water Level** | Signal | [cite_start]A1 [cite: 78] | Sends tank level readings |
| **LCD Screen** | SDA | [cite_start]A4 (or SDA) [cite: 41] | I2C Data |
| **LCD Screen** | SCL | [cite_start]A5 (or SCL) [cite: 44] | I2C Clock |
| **Relay** | IN | [cite_start]Digital Pin 7 [cite: 54] | Triggers Pump |
| **Pump (+)** | Red | [cite_start]Battery (+) [cite: 58] | Direct Power |
| **Pump (-)** | Black | [cite_start]Relay COM [cite: 61] | Switched Ground |

## ⚙️ Configuration & Calibration
The system logic is based on calibrated analog readings mapped to a 0-100% scale. These values can be adjusted in the code based on your specific soil type.

**Current Thresholds:**
* [cite_start]**Dry Soil (Trigger):** `< 20%` (Activates Pump) [cite: 88]
* [cite_start]**Overwatered Warning:** `> 70%` [cite: 89]
* [cite_start]**Low Water Tank:** `< 20%` (Prevents Pump activation) [cite: 90]

**Calibration Values:**
```cpp
// Sensor Calibration (Analog 0-1023)
const int SOIL_RAW_DRY = 900;   // Reading in air [cite: 83]
const int SOIL_RAW_WET = 300;   // Reading in water [cite: 84]
const int WATER_RAW_EMPTY = 0;  // Empty tank [cite: 85]
const int WATER_RAW_FULL = 650; // Full tank [cite: 86]
