# 32-Servo Expansion Board

This project includes **two expansion boards**, designed for multi-servo control and embedded system integration:

* **STM32C8T6 Expansion Board** – lightweight control + servo driver
* **STM32F103ZET6 Expansion Board** – high IO expansion + power hub (power supply for Raspberry Pi 4B / Orange Pi 3B, etc.)

---

## Project Overview

This design is suitable for the following applications:

* Multi-degree-of-freedom robotic arms
* Servo cluster control (e.g., 6-DOF robot)
* Embedded control systems with external compute units (Raspberry Pi / Orange Pi)

The system supports:

* **6 servos + 0.5A electromagnet**
* Stable multi-rail power supply
* Rich communication interfaces (UART, I2C, SPI)

---

## 1. STM32C8T6 Expansion Board

### Power Circuit

The power system is divided into two main parts:

#### Servo Power Supply

* Uses **NDP1415RB** step-down regulator
* High-current output dedicated for servos
* Supports:
  * Multiple servo channels
  * Adjustable servo voltage
  * External load (e.g., electromagnet)

#### MCU & Peripheral Power Supply

* Uses **NDP2450KC + RT9013-3.3**
* NDP2450KC provides stable 5V output
* RT9013-3.3 provides stable 3.3V for:
  * MCU
  * Sensors and logic modules

---

### Control Circuit

Main features:

* Servo control interfaces (multiple PWM outputs)
* Basic GPIO expansion (buttons, LEDs, free I/O pins)
* UART, I2C for OLED, SPI for LCD

---

## 2. STM32F103ZET6 Expansion Board

### Power Circuit

#### Main Power Input

* Supports battery or DC input
* Includes reverse polarity protection (e.g., SS54 diode)

#### High-Power Step-Down

* Uses **SCT2450S**
* Converts input (e.g., 12V) to 5V
* Supplies:
  * Servo power rail
  * External devices

#### 5V Linear Regulation

* Uses **LM7805**
* Provides clean 5V for:
  * MCU
  * Logic circuits

#### 3.3V Regulation

* Uses **RT9013-3.3**
* Supplies:
  * MCU core
  * Communication modules

#### Raspberry Pi / Orange Pi Power Supply

* Dedicated **5V high-current output** from SCT2450S
* Directly supplied by the step-down circuit

---

### Control Circuit

#### Core MCU

* STM32F103ZET6 (rich IO, high scalability)

#### Communication Interfaces

* UART (multiple channels)
* WiFi (ESP8266-01S)
* I2C (AT24C02 EEPROM, MPU6050)

#### Display & Peripherals

* OLED interface (I2C)
* TFT LCD interface
* Buzzer (transistor-driven)
* LEDs (status indicators)
* Push buttons (user input)

#### Expansion Interfaces

* NRF24L01 wireless module
* General-purpose IO headers
* Servo headers (multiple channels)

---

## Servo & Actuator Support

* Supports **6-DOF servo system**
* Independent servo power rail (VCC_Servo)
* Includes:
  * Signal resistor protection (100Ω)
  * Stable power decoupling

### Electromagnet Control

* Supports 0.5A electromagnet
* Controlled via MOSFET (NDP1415 / NDP2450KC)
* Includes:
  * Flyback protection
  * Switching control via MCU

---

## TODO / Improvements

1. **PCB Trace Optimization**

   * High-current servo traces should be widened
   * Increase copper pour area for power paths

2. **Thermal Design**

   * Add heat dissipation for:
     * SCT2450
     * Linear regulator (LM7805)

3. **Power Optimization**

   * LM7805 has low conversion efficiency; it is recommended to follow up with other domestic power ICs

---

## Notes

* When using high-current servos and external compute devices (Raspberry Pi / Orange Pi), please ensure proper grounding.
