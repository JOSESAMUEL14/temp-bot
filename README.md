# 🤖 MINI TBB

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" alt="MINI TBB Robot" width="700">
</p>

<h1 align="center">MINI TBB</h1>

<p align="center">
  <strong>Autonomous 2WD Obstacle-Avoidance Robot</strong>
</p>

<p align="center">
  <em>SENSE • DECIDE • MOVE</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Controller-ESP32--WROOM--32-blue" alt="ESP32">
  <img src="https://img.shields.io/badge/Programming-Arduino%20IDE-00979D" alt="Arduino IDE">
  <img src="https://img.shields.io/badge/Drive-2WD-orange" alt="2WD">
  <img src="https://img.shields.io/badge/Sensor-HC--SR04-green" alt="HC-SR04">
  <img src="https://img.shields.io/badge/Power-18650%20Li--ion-yellow" alt="Battery">
</p>

---

## 🧭 Overview

**MINI TBB** is a compact autonomous mobile robot built around an **ESP32-WROOM-32**.

The robot uses an **HC-SR04 ultrasonic sensor** to continuously monitor the path ahead.

When powered on, MINI TBB automatically moves forward.

When an obstacle is detected:

```text
Obstacle Detected
       ↓
   Move Backward
       ↓
 🔊 Buzzer Active
 💡 LED Blinking
       ↓
Obstacle Still Present?
       ↓
      YES
       ↓
Continue Backward
       ↓
Obstacle Cleared
       ↓
  Move Forward
```

No manual controller is required during normal operation.

---

## ✨ What Makes MINI TBB?

MINI TBB combines a number of fundamental robotics concepts into one compact platform:

```text
             ┌───────────────────┐
             │     MINI TBB      │
             └─────────┬─────────┘
                       │
       ┌───────────────┼───────────────┐
       │               │               │
       ▼               ▼               ▼
    SENSING         CONTROL         MOTION
       │               │               │
    HC-SR04          ESP32        2 DC Motors
       │               │               │
       └───────────────┼───────────────┘
                       │
                       ▼
                 AUTONOMOUS
                   ROBOT
```

---

## 🚦 Robot Status Flow

```text
┌────────────────┐
│   🟢 POWER ON  │
└───────┬────────┘
        ↓
┌────────────────┐
│ 🚗 FORWARD     │
└───────┬────────┘
        ↓
┌────────────────┐
│ 📡 HC-SR04     │
│ CHECK DISTANCE │
└───────┬────────┘
        ↓
    ┌───────┐
    │ Clear │
    └───┬───┘
        │
        └──────────────► 🚗 FORWARD


    ┌───────────┐
    │ OBSTACLE  │
    └─────┬─────┘
          ↓
    ┌──────────────┐
    │ 🔄 REVERSE   │
    │ 🔊 BUZZER    │
    │ 💡 LED BLINK │
    └──────┬───────┘
           ↓
     Obstacle Clear?
           │
           └──────────► 🚗 FORWARD
```

---

## ⭐ Core Features

### 🤖 Autonomous Navigation

MINI TBB begins moving forward automatically when powered on.

### 📡 Ultrasonic Obstacle Detection

An **HC-SR04** sensor monitors the area in front of the robot.

### 🔄 Automatic Reverse

When an obstacle is detected, the robot automatically reverses.

### 🔁 Continuous Obstacle Response

The robot continues reversing while the obstacle remains in front of it.

### 🔊 Audible Feedback

The buzzer operates during reverse movement.

### 💡 Visual Feedback

A separate LED blinks during obstacle detection and reverse movement.

### 🧠 ESP32-Based Control

The ESP32-WROOM-32 acts as the main controller for sensing and motion.

### 🔌 Custom Electronics

A custom PCB integrates the robot's electronics and connections.

---

# 🧩 Hardware

## 🧠 Main Controller

### ESP32-WROOM-32

The ESP32-WROOM-32 serves as the main processing and control unit.

It is responsible for:

* Reading the ultrasonic sensor
* Processing obstacle conditions
* Controlling the motor system
* Operating the buzzer
* Controlling the obstacle indicator LED

---

## 📡 Ultrasonic Sensor

### HC-SR04

The HC-SR04 is mounted at the front of MINI TBB.

| Pin  | Connection |
| ---- | ---------- |
| VCC  | 5V         |
| TRIG | GPIO 21    |
| ECHO | GPIO 22    |
| GND  | GND        |

### Connection

```text
       HC-SR04
     ┌───────────┐
     │           │
VCC ─┤           ├── 5V
TRIG─┤           ├── GPIO21
ECHO─┤           ├── GPIO22
GND ─┤           ├── GND
     └───────────┘
```

---

## ⚙️ Drive System

MINI TBB uses a **2-wheel-drive configuration**.

```text
             FRONT
               ▲

         ┌───────────┐
         │  HC-SR04  │
         └───────────┘

          ◯         ◯
          │         │
       MOTOR 1   MOTOR 2
          │         │
          └────┬────┘
               │
             2WD
```

### Drive Components

* 2 × Geared DC Motors
* 2 × Wheels
* Motor driver module
* Custom chassis

---

## 🔋 Power System

MINI TBB is powered by a rechargeable **ICR-18650 Li-ion cell**.

### Battery

| Parameter | Value     |
| --------- | --------- |
| Type      | Li-ion    |
| Cell      | ICR-18650 |
| Voltage   | 3.7 V     |
| Capacity  | 2200 mAh  |
| Energy    | 8.14 Wh   |

### Power Components

```text
       🔋 18650
          │
          ▼
    🔘 ON / OFF
          │
          ▼
    ⚡ Power Circuit
          │
          ▼
    🔌 DC-DC Module
          │
          ▼
      MINI TBB PCB
```

The robot also includes a **USB-C charging module**.

---

# 🔌 Electronics

## Custom PCB

MINI TBB uses a custom control PCB that provides connections between the main controller, motors, sensor, indicators, and power system.

The PCB includes connection points for:

* ESP32
* Motor system
* Servo expansion
* HC-SR04
* Buzzer
* LEDs
* Power
* Additional GPIO connections

---

## 🔊 Buzzer

The buzzer provides audible feedback during obstacle detection.

```text
Obstacle
   ↓
ESP32 detects condition
   ↓
Robot reverses
   ↓
🔊 BUZZER ACTIVE
```

---

## 💡 LED Indicators

MINI TBB uses two LED functions.

### 🔴 PCB LED

Indicates the power/operating status of the PCB.

### 💡 Obstacle LED

Blinks when an obstacle is detected and the robot is reversing.

---

# 📋 Specifications

| Category              | Specification           |
| --------------------- | ----------------------- |
| **Project**           | MINI TBB                |
| **Robot Type**        | Autonomous Mobile Robot |
| **Navigation**        | Obstacle Avoidance      |
| **Drive**             | 2WD                     |
| **Motors**            | 2 × Geared DC Motors    |
| **Wheels**            | 2                       |
| **Controller**        | ESP32-WROOM-32          |
| **Sensor**            | HC-SR04                 |
| **Sensor Count**      | 1                       |
| **Programming**       | Arduino IDE             |
| **Language**          | Arduino C/C++           |
| **Operation**         | Autonomous              |
| **Battery**           | ICR-18650 Li-ion        |
| **Battery Voltage**   | 3.7 V                   |
| **Battery Capacity**  | 2200 mAh                |
| **Battery Energy**    | 8.14 Wh                 |
| **Charging**          | USB-C                   |
| **PCB**               | Custom                  |
| **Chassis**           | Custom / 3D-printed     |
| **Obstacle Response** | Reverse                 |
| **Buzzer**            | Reverse/obstacle alert  |
| **Obstacle LED**      | Reverse indicator       |

---

# 🧠 Control Logic

The complete robot behavior can be represented as:

```text
                         START
                           │
                           ▼
                     Initialize
                           │
                           ▼
                    MOVE FORWARD
                           │
                           ▼
                  Read HC-SR04
                           │
                           ▼
                    ┌───────────┐
                    │ Obstacle? │
                    └─────┬─────┘
                          │
                 ┌────────┴────────┐
                 │                 │
                NO                YES
                 │                 │
                 ▼                 ▼
          MOVE FORWARD        MOVE BACKWARD
                 │                 │
                 │          ┌──────┴──────┐
                 │          │             │
                 │       🔊 Buzzer     💡 LED
                 │          │             │
                 │          └──────┬──────┘
                 │                 │
                 │          Check obstacle
                 │                 │
                 │           ┌─────┴─────┐
                 │           │           │
                 │          YES          NO
                 │           │           │
                 │           │           ▼
                 │           │      MOVE FORWARD
                 │           │
                 │           └──────────────┐
                 │                          │
                 └──────────────────────────┘
```

---

# 🔄 Movement States

| Robot State  | Motors  | Buzzer | Obstacle LED |
| ------------ | ------- | ------ | ------------ |
| 🟢 Forward   | Forward | OFF    | OFF          |
| 🔴 Obstacle  | Reverse | ON     | Blink        |
| 🔄 Reversing | Reverse | ON     | Blink        |
| 🟢 Clear     | Forward | OFF    | OFF          |

---

# 💻 Software

MINI TBB is programmed using **Arduino IDE**.

## Development Stack

```text
┌────────────────────────┐
│      Arduino IDE       │
└───────────┬────────────┘
            │
            ▼
┌────────────────────────┐
│     Arduino C/C++      │
└───────────┬────────────┘
            │
            ▼
┌────────────────────────┐
│    ESP32-WROOM-32      │
└───────────┬────────────┘
            │
     ┌──────┼──────┐
     ▼      ▼      ▼
 HC-SR04 Motors  Indicators
```

---

# 🚀 Getting Started

## 1️⃣ Hardware

Assemble the robot with:

* ESP32-WROOM-32
* Custom PCB
* 2 geared DC motors
* 2 wheels
* HC-SR04
* Motor driver
* Battery
* Charging module
* DC-DC module
* Buzzer
* LEDs
* Power switch

---

## 2️⃣ Arduino IDE

Install Arduino IDE and configure ESP32 board support.

Connect the ESP32 to your computer using USB.

Select the appropriate ESP32 board and upload the MINI TBB firmware.

---

## 3️⃣ Power ON

After programming:

```text
USB Connected
     ↓
Upload Firmware
     ↓
Disconnect USB
     ↓
Install Battery
     ↓
Power ON
     ↓
MINI TBB starts moving
```

---

# 🧪 Testing

## Test 01 — Startup

**Action:**

Turn ON MINI TBB.

**Expected:**

```text
🟢 Robot powers ON
       ↓
🚗 Starts moving forward
```

---

## Test 02 — Obstacle

**Action:**

Place an obstacle in front of the robot.

**Expected:**

```text
📡 HC-SR04 detects obstacle
       ↓
🔄 Robot reverses
       ↓
🔊 Buzzer activates
       ↓
💡 LED blinks
```

---

## Test 03 — Obstacle Removal

**Action:**

Remove the obstacle while the robot is reversing.

**Expected:**

```text
📡 Path becomes clear
       ↓
🔊 Buzzer stops
       ↓
💡 LED stops blinking
       ↓
🚗 Robot moves forward
```

---

# 🏗️ System Architecture

```text
                         ┌──────────────┐
                         │ ICR-18650    │
                         │ 3.7V / 2200mAh│
                         └───────┬──────┘
                                 │
                                 ▼
                         ┌──────────────┐
                         │ Power System │
                         └───────┬──────┘
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │      MINI TBB PCB      │
                    │                        │
                    │   ┌────────────────┐   │
                    │   │ ESP32-WROOM-32 │   │
                    │   └───────┬────────┘   │
                    │           │            │
                    └───────────┼────────────┘
                                │
                 ┌──────────────┼──────────────┐
                 │              │              │
                 ▼              ▼              ▼
             HC-SR04       Motor Driver     Buzzer
                 │              │
                 │        ┌─────┴─────┐
                 │        ▼           ▼
                 │     Motor 1     Motor 2
                 │        │           │
                 │        ▼           ▼
                 │      Wheel       Wheel
                 │
                 └──────► ESP32

                         ESP32
                           │
                           ▼
                    Obstacle LED
```

---

# 📸 Robot Gallery

Add your actual robot images to the repository and display them here.

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" width="45%" alt="MINI TBB Front View">
  <img src="assets/images/mini-tbb-side.jpg" width="45%" alt="MINI TBB Side View">
</p>

<p align="center">
  <img src="assets/images/mini-tbb-top.jpg" width="45%" alt="MINI TBB Top View">
  <img src="assets/images/pcb.jpg" width="45%" alt="MINI TBB PCB">
</p>

---

# 📁 Repository Structure

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

# 📜 License

This project is released under the **MIT License**.

See the `LICENSE` file for the complete license terms.

---

# 🤖 MINI TBB

### A compact autonomous robot built around a simple idea:

```text
       📡
      SENSE
        │
        ▼
      🧠
     DECIDE
        │
        ▼
      ⚙️
      MOVE
        │
        ▼
      🔁
     REPEAT
```

**MINI TBB — SENSE • DECIDE • MOVE**
