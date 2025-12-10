# Tomato Soil Monitor 🍅💧

An automated plant care system designed specifically for tomato plants. This device monitors soil moisture levels and automatically waters the plant when necessary, while also tracking the water reservoir level to protect the pump.

## 📖 Project Overview
Tomatoes are sensitive to inconsistent watering. This project solves that problem by creating a closed-loop system that:
1.  **Monitors** soil moisture in real-time.
2.  **Visualizes** data on an LCD screen.
3.  **Automates** watering via a relay and pump.
4.  **Protects** the hardware by sensing low water levels in the reservoir.

## 🧰 Hardware Components
* **Microcontroller:** Arduino Uno
* * **Sensors:**
    *Capacitive Soil Moisture Sensor
    *Water Level Sensor
* **Actuators:**
  *5V Relay Module
  *Submersible Water Pump
* **Display:** LCD1602 RGB Module (I2C)
* **Power:**
    * 9V/USB for Arduino Logic
    * External Battery Pack for Pump
  * **Enclosure:** Repurposed plastic tool caddy (chosen for water resistance and portability) 

## ⚡ Circuit Wiring
The system uses a split power supply: the Arduino powers the sensors and screen (5V), while the battery pack powers the pump via the relay.

| Component | Pin | Arduino/Connection | Function |
| :--- | :--- | :--- | :--- |
| **Soil Sensor** | AOUT | A0  | Sends moisture readings |
| **Water Level** | Signal | A1  | Sends tank level readings |
| **LCD Screen** | SDA | A4 (or SDA) | I2C Data |
| **LCD Screen** | SCL |A5 (or SCL) | I2C Clock |
| **Relay** | IN | Digital Pin 7  | Triggers Pump |
| **Pump (+)** | Red | Battery (+) | Direct Power |
| **Pump (-)** | Black | Relay COM  | Switched Ground |

## ⚙️ Configuration & Calibration
The system logic is based on calibrated analog readings mapped to a 0-100% scale. These values can be adjusted in the code based on your specific soil type.

**Current Thresholds:**
* **Dry Soil (Trigger):** `< 20%` (Activates Pump) 
* **Overwatered Warning:** `> 70%`
* **Low Water Tank:** `< 20%` (Prevents Pump activation) 

**Calibration Values:**
```cpp
// Sensor Calibration (Analog 0-1023)
const int SOIL_RAW_DRY = 900;   // Reading in air
const int SOIL_RAW_WET = 300;   // Reading in water
const int WATER_RAW_EMPTY = 0;  // Empty tank 
const int WATER_RAW_FULL = 650; // Full tank 
