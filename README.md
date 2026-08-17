# 🤖 MINI TBB

### SENSE · DECIDE · MOVE

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" alt="MINI TBB Robot" width="650">
</p>

<p align="center">
  <b>An Autonomous 2WD Obstacle Avoidance Robot</b>
</p>

<p align="center">
  ESP32-WROOM-32 • HC-SR04 • Arduino IDE • Custom PCB
</p>

---

## 📚 Table of Contents

* [About](#-about)
* [Key Highlights](#-key-highlights)
* [Hardware Components](#-hardware-components)
* [Specifications](#-specifications)
* [Pin Connections](#-pin-connections)
* [How It Works](#-how-it-works)
* [Power System](#-power-system)
* [Motor System](#️-motor-system)
* [Obstacle Detection](#-obstacle-detection)
* [Buzzer & LED Indicators](#-buzzer--led-indicators)
* [Software](#-software)
* [Getting Started](#-getting-started)
* [Testing](#-testing)
* [Repository Structure](#-repository-structure)
* [System Architecture](#️-system-architecture)
* [License](#-license)

---

## 🤖 About

**MINI TBB** is a compact autonomous two-wheel-drive robot designed around the **ESP32-WROOM-32** microcontroller.

The robot uses an **HC-SR04 ultrasonic sensor** to detect obstacles in front of it. When powered on, MINI TBB automatically begins moving forward.

When an obstacle is detected, the robot automatically changes direction and moves backward. During reverse movement, a buzzer provides an audible alert and an indicator LED blinks. The robot continues moving backward while the obstacle remains detected.

Once the obstacle is cleared, MINI TBB automatically resumes forward movement.

The project combines:

* 🧠 ESP32 embedded control
* 📡 Ultrasonic distance sensing
* ⚙️ DC motor control
* 🔋 Rechargeable battery power
* 🔌 Custom PCB electronics
* 🔊 Audible feedback
* 💡 Visual status indication
* 💻 Arduino-based programming

> **Sense → Decide → Move → Repeat**

---

## ⭐ Key Highlights

| Feature                 | Description                                            |
| ----------------------- | ------------------------------------------------------ |
| 🤖 Autonomous Operation | Starts moving automatically after power ON             |
| 🚗 2WD Drive            | Uses 2 geared DC motors and 2 wheels                   |
| 📡 Obstacle Detection   | HC-SR04 detects obstacles in front of the robot        |
| 🔄 Automatic Reverse    | Reverses when an obstacle is detected                  |
| 🔁 Continuous Response  | Keeps reversing while the obstacle remains detected    |
| ▶️ Forward Recovery     | Resumes forward movement after the obstacle is cleared |
| 🔊 Buzzer Alert         | Beeps during obstacle detection and reverse movement   |
| 💡 LED Indicator        | Blinks during obstacle detection and reverse movement  |
| 🧠 ESP32 Control        | ESP32-WROOM-32 manages sensing and movement            |
| 🔌 Custom PCB           | Integrates the robot's electronic components           |
| 🔋 Rechargeable Battery | Uses an ICR-18650 Li-ion cell                          |
| 💻 Arduino IDE          | Programmed using Arduino IDE                           |

---

## 📦 Hardware Components

### 🧠 Control & Electronics

* **ESP32-WROOM-32** development board
* Custom MINI TBB control PCB
* Motor driver module
* DC-DC power conversion module
* USB-C charging module
* ON/OFF power switch

### 🚗 Motion System

* **2 × Geared DC Motors**
* **2 × Wheels**
* Custom robot chassis

### 📡 Sensor

* **1 × HC-SR04 Ultrasonic Sensor**

### 🔊 Indicators

* Buzzer
* PCB power/status LED
* Obstacle/reverse indicator LED

### 🔋 Power

* **1 × ICR-18650 Li-ion Cell**
* Nominal voltage: **3.7 V**
* Capacity: **2200 mAh**
* Energy: **8.14 Wh**

---

## 🔧 Specifications

| Specification               | Details                             |
| --------------------------- | ----------------------------------- |
| **Project Name**            | MINI TBB                            |
| **Robot Type**              | Autonomous Obstacle Avoidance Robot |
| **Drive System**            | 2-Wheel Drive (2WD)                 |
| **Drive Motors**            | 2 × Geared DC Motors                |
| **Wheels**                  | 2                                   |
| **Microcontroller**         | ESP32-WROOM-32                      |
| **Ultrasonic Sensor**       | HC-SR04                             |
| **Sensor Quantity**         | 1                                   |
| **Programming Environment** | Arduino IDE                         |
| **Programming Language**    | Arduino C/C++                       |
| **Control Mode**            | Autonomous                          |
| **Battery Type**            | ICR-18650 Li-ion                    |
| **Battery Voltage**         | 3.7 V                               |
| **Battery Capacity**        | 2200 mAh                            |
| **Battery Energy**          | 8.14 Wh                             |
| **Charging Interface**      | USB-C                               |
| **Motor Driver**            | Motor Driver Module                 |
| **Power Conversion**        | DC-DC Converter                     |
| **Chassis**                 | Custom / 3D-printed                 |
| **Obstacle Response**       | Reverse until obstacle is cleared   |
| **Buzzer**                  | Active during reverse               |
| **Obstacle LED**            | Blinks during reverse               |
| **PCB LED**                 | Indicates PCB/power status          |

---

## 🔌 Pin Connections

### 📡 HC-SR04 → ESP32

| HC-SR04 Pin | Connection    |
| ----------- | ------------- |
| **VCC**     | 5V            |
| **TRIG**    | ESP32 GPIO 21 |
| **ECHO**    | ESP32 GPIO 22 |
| **GND**     | GND           |

### Sensor Wiring

```text
                 HC-SR04
              ┌────────────┐
              │            │
      VCC ────┤ VCC        │──── 5V
     TRIG ────┤ TRIG       │──── GPIO 21
     ECHO ────┤ ECHO       │──── GPIO 22
      GND ────┤ GND        │──── GND
              │            │
              └────────────┘
```

---

## 🧠 How It Works

MINI TBB uses a simple autonomous control loop.

```text
                   ┌──────────────┐
                   │   POWER ON   │
                   └──────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ MOVE FORWARD  │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │    HC-SR04    │
                  │ CHECK DISTANCE│
                  └───────┬───────┘
                          │
                     Obstacle?
                       /     \
                     NO       YES
                     │         │
                     │         ▼
                     │  ┌──────────────┐
                     │  │ MOVE BACKWARD│
                     │  │              │
                     │  │ 🔊 Buzzer    │
                     │  │ 💡 LED Blink │
                     │  └──────┬───────┘
                     │         │
                     │         ▼
                     │   Obstacle still
                     │      present?
                     │      /      \
                     │    YES       NO
                     │     │         │
                     │     └────┐    │
                     │          │    ▼
                     │          │ MOVE FORWARD
                     │          │
                     └──────────┘
```

### Operating Sequence

1. Power ON MINI TBB.
2. ESP32 initializes the robot.
3. The robot starts moving forward.
4. HC-SR04 measures the distance ahead.
5. If the path is clear, the robot continues forward.
6. If an obstacle is detected, the robot moves backward.
7. The buzzer operates during reverse movement.
8. The obstacle LED blinks.
9. The robot continues reversing while the obstacle remains detected.
10. When the obstacle is cleared, the robot resumes forward movement.
11. The cycle repeats automatically.

---

## 🔋 Power System

MINI TBB uses a single rechargeable **ICR-18650 Li-ion cell**.

### Battery Specifications

```text
Battery Type : Li-ion
Cell         : ICR-18650
Voltage      : 3.7 V
Capacity     : 2200 mAh
Energy       : 8.14 Wh
```

### Power Components

* ICR-18650 Li-ion battery
* USB-C charging module
* ON/OFF power switch
* DC-DC power conversion module
* Custom PCB

### Power Flow

```text
       ICR-18650 Battery
              │
              ▼
       ON/OFF Switch
              │
              ▼
       Power / Charging
              │
              ▼
       DC-DC Conversion
              │
              ▼
          MINI TBB PCB
              │
       ┌──────┴──────┐
       ▼             ▼
     ESP32       Motor Driver
                     │
               ┌─────┴─────┐
               ▼           ▼
            Motor 1     Motor 2
```

---

## ⚙️ Motor System

MINI TBB uses a **2WD drivetrain** consisting of two geared DC motors and two wheels.

### Movement Behavior

| Condition         | Robot Behavior    |
| ----------------- | ----------------- |
| Power ON          | Move forward      |
| Clear path        | Continue forward  |
| Obstacle detected | Move backward     |
| Obstacle remains  | Continue backward |
| Obstacle cleared  | Move forward      |

### Drive Layout

```text
                    FRONT
                      ▲
                      │
                ┌───────────┐
                │  HC-SR04  │
                └───────────┘

                  O       O
                  │       │
               Motor 1  Motor 2
                  │       │
                  └───┬───┘
                      │
                    2WD
```

---

## 📡 Obstacle Detection

The **HC-SR04 ultrasonic sensor** is mounted at the front of MINI TBB.

It measures the distance to objects ahead of the robot. The ESP32 uses this information to determine whether the robot should continue moving forward or switch to reverse movement.

```text
                 HC-SR04
                    │
                    │ Distance
                    ▼
              ESP32-WROOM-32
                    │
              Decision Logic
                    │
             ┌──────┴──────┐
             │             │
          CLEAR         OBSTACLE
             │             │
             ▼             ▼
        MOVE FORWARD   MOVE BACKWARD
                            │
                       ┌────┴────┐
                       │         │
                    Buzzer    LED Blink
```

---

## 🔊 Buzzer & LED Indicators

### 🔊 Buzzer

The buzzer provides an audible indication when an obstacle is detected.

It operates while MINI TBB is moving backward.

### 🔴 PCB Power LED

The red LED on the custom PCB indicates whether the PCB is powered/operating.

### 💡 Obstacle Indicator LED

A separate LED blinks when an obstacle is detected and the robot enters reverse movement.

| Indicator       | Function                                     |
| --------------- | -------------------------------------------- |
| 🔴 PCB Red LED  | PCB / power status                           |
| 💡 Obstacle LED | Blinks during obstacle detection and reverse |
| 🔊 Buzzer       | Beeps during reverse movement                |

---

## 💻 Software

MINI TBB is programmed using **Arduino IDE**.

### Development Platform

* **Arduino IDE**
* **ESP32-WROOM-32**
* **Arduino C/C++**

### Software Responsibilities

The robot firmware handles:

* ESP32 initialization
* HC-SR04 distance sensing
* Obstacle detection
* Forward movement
* Reverse movement
* Motor control
* Buzzer operation
* Obstacle LED control

---

## 🚀 Getting Started

### 🔧 Hardware Setup

1. Assemble the MINI TBB chassis.
2. Install the two geared DC motors.
3. Install the two wheels.
4. Mount the HC-SR04 at the front.
5. Install the ESP32-WROOM-32 on the custom PCB.
6. Connect the motor driver and motors.
7. Connect the HC-SR04.
8. Connect the buzzer and indicator LED.
9. Install the ICR-18650 battery.
10. Verify the power connections.
11. Turn ON the robot.

### 💻 Software Setup

1. Install **Arduino IDE**.
2. Install ESP32 board support.
3. Connect the ESP32 to your computer using USB.
4. Select the appropriate ESP32 board.
5. Load the MINI TBB firmware.
6. Compile the program.
7. Upload the firmware.
8. Disconnect USB.
9. Power ON MINI TBB.
10. Test the robot in an open area.

---

## 🧪 Testing

### Basic Operation Test

```text
Power ON
   │
   ▼
Robot moves forward
   │
   ▼
Obstacle placed in front
   │
   ▼
HC-SR04 detects obstacle
   │
   ▼
Robot moves backward
   │
   ├── 🔊 Buzzer
   │
   └── 💡 LED Blink
   │
   ▼
Obstacle remains
   │
   ▼
Robot continues backward
   │
   ▼
Obstacle removed
   │
   ▼
Robot resumes forward movement
```

### Expected Behavior

| Test Condition    | Expected Result             |
| ----------------- | --------------------------- |
| Power ON          | Robot starts moving forward |
| Clear path        | Robot continues forward     |
| Obstacle detected | Robot moves backward        |
| Reverse movement  | Buzzer operates             |
| Reverse movement  | Obstacle LED blinks         |
| Obstacle remains  | Robot continues reversing   |
| Obstacle removed  | Robot moves forward         |

---

## 📁 Repository Structure

```text
MINI-TBB/
│
├── assets/
│   ├── images/
│   │   ├── mini-tbb-front.jpg
│   │   ├── mini-tbb-side.jpg
│   │   ├── mini-tbb-top.jpg
│   │   └── pcb.jpg
│   │
│   └── diagrams/
│       ├── system-architecture.png
│       └── wiring-diagram.png
│
├── hardware/
│   ├── pcb/
│   ├── wiring/
│   └── mechanical/
│
├── firmware/
│   └── arduino/
│       └── MINI_TBB/
│
├── docs/
│   ├── assembly/
│   ├── hardware/
│   └── operation/
│
├── LICENSE
└── README.md
```

---

## 🏗️ System Architecture

```text
                         MINI TBB
                            │
             ┌──────────────┴──────────────┐
             │                             │
        Power System                  Sensing System
             │                             │
     ┌───────┴───────┐               ┌────┴────┐
     │               │               │ HC-SR04 │
  18650          DC-DC               │ Sensor  │
  Battery        Converter           └────┬────┘
     │               │                    │
     └───────┬───────┘                    │
             │                            │
             ▼                            ▼
       ┌─────────────────────────────────────┐
       │            CUSTOM PCB               │
       │                                     │
       │         ESP32-WROOM-32              │
       │                │                    │
       │          ┌─────┴─────┐              │
       │          │   Motor   │              │
       │          │   Driver  │              │
       │          └─────┬─────┘              │
       └────────────────┼────────────────────┘
                        │
                ┌───────┴───────┐
                │               │
                ▼               ▼
             Motor 1         Motor 2
                │               │
                ▼               ▼
              Wheel           Wheel

       ESP32 ───────────────► Buzzer
       ESP32 ───────────────► Obstacle LED
       PCB  ────────────────► Power LED
```

---

## 📜 License

This project is released under the **MIT License**.

See the `LICENSE` file for the complete license terms.

---

## 🤖 MINI TBB

**MINI TBB** demonstrates a simple autonomous robotics system using an **ESP32-WROOM-32**, **HC-SR04 ultrasonic sensing**, **2WD motor control**, custom electronics, rechargeable battery power, and Arduino programming.

The robot continuously follows a simple autonomous cycle:

```text
📡 SENSE
   ↓
🧠 DECIDE
   ↓
⚙️ MOVE
   ↓
🔁 REPEAT
```

**MINI TBB — Sense. Decide. Move.**
