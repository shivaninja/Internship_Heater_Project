
# Arduino Temperature-Controlled Heater System

Using LM75 / TMP36 sensors with finite state machine control

This project implements a smart heater controller using Arduino.
It monitors temperature in real-time and adjusts heater output using a Finite State Machine (FSM).
Two versions are implemented:

### Project 1 — Analog Sensor (TMP36, No Protocols)

### Project 2 — Digital I²C Sensor (LM75 using I²C / Wire.h)

# Project Structure

* Temperature-Heater-Control
  
 ├── Project-1-TMP36-Analog

 ├── Project-2-LM75-I2C
 
 ├── README.md (this file)
 
 └── ...


# Project Variants

## Project 1 — Analog Temperature Sensor (TMP36)

1. No communication protocols
2. Uses Arduino’s internal ADC + analogRead()
3. Acts as base template for the system

Sensor: TMP36
Input Method: Raw ADC reading → Celsius Conversion
Protocol: None

Why TMP36?

Directly outputs a voltage proportional to temperature

Simple wiring

No driver or communication protocol

TMP36 → Analog Pin (A0) → Convert ADC → °C

## Project 2 — I²C Temperature Sensor (LM75)

1. Uses I²C protocol
2. Reads temperature using Wire.h
3. More accurate & digital temperature data

Sensor: LM75
Protocol: I²C
Default Address: 0x48

Why LM75?

Built-in onboard ADC

9-bit digital temperature

No analog noise

Supports high-precision industrial readings

📡 Hardware Requirements
Component	Purpose
Arduino Uno	Microcontroller
Heater Relay / LED	Simulated heater output
200Ω resistor	Current-limiting (recommended)
Wires	Connections
TMP36 Sensor	For Project 1
LM75 Sensor (I²C)	For Project 2
LED (optional)	Overheat indicator
 System Behavior — How It Works

This firmware continuously monitors temperature and controls a heater based on thresholds.

Implemented as a Finite State Machine (FSM)

States:

IDLE – Wait for temperature to drop below threshold

HEATING – Heater ON

STABILIZING – Heater OFF (temperature reached, cool-down window)

TARGET_REACHED – Stable temperature maintained

OVERHEAT – Emergency shutdown + warning LED

## Temperature Logic
Key parameters
const float targetTemp = 40.0;   // Desired temperature (°C)
const float hysteresis = 2.0;    // Buffer to prevent rapid switching
const float overheatTemp = 50.0; // Safety limit (°C)

Example behavior

If temperature < 38°C → Heater ON

If temperature ≥ 40°C → Stabilize state

If temperature ≥ 50°C → Emergency shutdown

Why Two Versions?
Version	Sensor Type	Communication	Stability	Industrial Use
Project 1	TMP36	None (Analog)	Medium	Hobby use
Project 2	LM75	I²C digital	High	Embedded / HVAC
## Pin Connections
## Heater / Relay
D8 → Heater / LED

## Overheat Indicator
D13 → LED

## Sensor Wiring
```

TMP36 (Project 1)
VCC → 5V
GND → GND
OUT → A0

LM75 (Project 2 – I²C)
SDA → A4
SCL → A5
VCC → 3.3V
GND → GND

```

## Requirements

Arduino IDE

Arduino UNO

C++ / Arduino Framework

TMP36 sensor (Analog) OR LM75 (I²C)

## Core Concepts Demonstrated

1. ADC reading

2. I²C communication

3. Sensor data conversion

4. State machine design pattern

5. Heat control logic (PID-like hysteresis)

6. Safety cut-off logic

## Future Improvements

PID controller instead of hysteresis

OLED temperature display (SSD1306)

Logging via UART/MQTT

SPI sensor integration

EEPROM calibration storage

## Author

Developed by: Shiva Panjugula
Low-level programming, Embedded Systems & IoT
