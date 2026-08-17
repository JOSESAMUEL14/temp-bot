# 🤖 MINI TBB

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" alt="MINI TBB Robot" width="750">
</p>

<p align="center">
  <h1 align="center">MINI TBB</h1>
</p>

<p align="center">
  <strong>Autonomous 2WD Obstacle-Avoidance Robot</strong>
</p>

<p align="center">
  <em>Sense • Decide • Move</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/ESP32-WROOM--32-blue?style=for-the-badge&logo=espressif">
  <img src="https://img.shields.io/badge/Arduino-IDE-00979D?style=for-the-badge&logo=arduino">
  <img src="https://img.shields.io/badge/Drive-2WD-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/Sensor-HC--SR04-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Power-18650-yellow?style=for-the-badge">
</p>

---

# 🛰️ PROJECT OVERVIEW

**MINI TBB** is a compact autonomous robot designed to demonstrate the fundamental principles of mobile robotics:

> **Sense the environment → Make a decision → Control movement**

The robot is built around an **ESP32-WROOM-32** and uses an **HC-SR04 ultrasonic sensor** to detect obstacles in its path.

When powered on, MINI TBB automatically moves forward.

When an obstacle appears:

```text id="e0sp5t"
                 🚧 OBSTACLE
                      │
                      ▼
              ┌───────────────┐
              │   HC-SR04     │
              │   DETECTION   │
              └───────┬───────┘
                      │
                      ▼
               🧠 ESP32 DECISION
                      │
                      ▼
                🔄 REVERSE
                  ╱     ╲
                 ╱       ╲
              🔊 BEEP   💡 BLINK
                 ╲       ╱
                  ╲     ╱
                      │
                      ▼
                 PATH CLEAR
                      │
                      ▼
                  🚗 FORWARD
```

The robot continues reversing until the obstacle is no longer detected, then automatically resumes forward movement.

---

# 🎯 PROJECT AT A GLANCE

<table align="center">
<tr>
<td align="center">

### 🧠

**CONTROLLER**

ESP32-WROOM-32

</td>

<td align="center">

### 📡

**SENSOR**

HC-SR04

</td>

<td align="center">

### ⚙️

**DRIVE**

2WD

</td>

<td align="center">

### 🔋

**POWER**

18650 Li-ion

</td>
</tr>
</table>

<br>

<table align="center">
<tr>
<td align="center">

🤖
**AUTONOMOUS**

</td>

<td align="center">

🔄
**AUTO REVERSE**

</td>

<td align="center">

🔊
**BUZZER ALERT**

</td>

<td align="center">

💡
**LED STATUS**

</td>
</tr>
</table>

---

# ✨ CORE FEATURES

### 🤖 Autonomous Operation

MINI TBB starts moving automatically as soon as it is powered on.

### 📡 Obstacle Detection

The HC-SR04 continuously checks the path in front of the robot.

### 🔄 Automatic Reverse

When an obstacle is detected, the robot immediately changes to reverse movement.

### 🔁 Persistent Response

The robot continues reversing as long as the obstacle remains detected.

### 🚗 Automatic Recovery

Once the obstacle is cleared, the robot automatically resumes forward movement.

### 🔊 Audible Feedback

The buzzer operates while the robot is reversing.

### 💡 Visual Feedback

The obstacle indicator LED blinks during reverse movement.

### 🔌 Custom Electronics

A custom PCB integrates the robot's electronic connections.

---

# 🧠 THE MINI TBB PHILOSOPHY

```text id="x8m5vy"
          ┌───────────────┐
          │               │
          │   📡 SENSE    │
          │               │
          └───────┬───────┘
                  │
                  ▼
          ┌───────────────┐
          │               │
          │  🧠 DECIDE    │
          │               │
          └───────┬───────┘
                  │
                  ▼
          ┌───────────────┐
          │               │
          │   ⚙️ MOVE     │
          │               │
          └───────┬───────┘
                  │
                  ▼
          ┌───────────────┐
          │               │
          │   🔁 REPEAT   │
          │               │
          └───────┬───────┘
                  │
                  └───────────────► 📡
```

---

# 🧩 HARDWARE

## 🧠 ESP32-WROOM-32

The ESP32-WROOM-32 acts as the central controller of MINI TBB.

It connects the sensing, movement, and feedback systems.

```text id="1zxx4q"
                     ESP32
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
     📡 SENSOR      ⚙️ MOTORS      🔊 / 💡
     HC-SR04       MOTOR DRIVER     FEEDBACK
```

---

## 📡 HC-SR04

A single **HC-SR04 ultrasonic sensor** is mounted at the front of the robot.

It provides distance information used to detect obstacles.

### Pin Mapping

| Sensor | Connection |
| ------ | ---------- |
| VCC    | 5V         |
| TRIG   | GPIO 21    |
| ECHO   | GPIO 22    |
| GND    | GND        |

```text id="5p4x3g"
              HC-SR04

         ┌───────────────┐
         │               │
  5V ────┤ VCC           │
 GPIO21 ─┤ TRIG          │
 GPIO22 ─┤ ECHO          │
  GND ───┤ GND           │
         │               │
         └───────────────┘
```

---

# ⚙️ MOTION SYSTEM

MINI TBB uses **two geared DC motors** and **two wheels**.

```text id="nhb5jq"
                    FRONT
                      ▲
                      │
               ┌─────────────┐
               │   HC-SR04   │
               └─────────────┘

                   ◯     ◯
                   │     │
                 M1       M2
                   │     │
                   └──┬──┘
                      │
                     2WD
```

### Motion States

| Robot State         | Movement         |
| ------------------- | ---------------- |
| 🟢 Normal           | Forward          |
| 🔴 Obstacle         | Reverse          |
| 🔴 Obstacle remains | Continue Reverse |
| 🟢 Path clear       | Forward          |

---

# 🔋 POWER ARCHITECTURE

MINI TBB uses one rechargeable **ICR-18650 Li-ion cell**.

### Battery Specifications

| Parameter | Value     |
| --------- | --------- |
| Cell      | ICR-18650 |
| Chemistry | Li-ion    |
| Voltage   | 3.7 V     |
| Capacity  | 2200 mAh  |
| Energy    | 8.14 Wh   |

### Power System

```text id="bbt2jj"
              🔌 USB-C
                  │
                  ▼
        ┌───────────────────┐
        │ Charging Module   │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ 🔋 ICR-18650      │
        │ 3.7V / 2200mAh    │
        └─────────┬─────────┘
                  │
                  ▼
             🔘 SWITCH
                  │
                  ▼
        ┌───────────────────┐
        │ ⚡ DC-DC Module   │
        └─────────┬─────────┘
                  │
                  ▼
           ┌──────────────┐
           │ MINI TBB PCB │
           └──────┬───────┘
                  │
             ┌────┴────┐
             ▼         ▼
          🧠 ESP32   ⚙️ Motors
```

---

# 🔌 CUSTOM PCB

MINI TBB uses a custom control PCB to connect the major electronic systems.

### PCB Includes Connections For

```text id="4xw8fn"
                    CUSTOM PCB
                         │
       ┌─────────────────┼──────────────────┐
       │                 │                  │
       ▼                 ▼                  ▼
     ESP32           Motor Driver         POWER
       │                 │
       │          ┌──────┴──────┐
       │          ▼             ▼
       │       Motor 1       Motor 2
       │
       ├──────────► HC-SR04
       ├──────────► Buzzer
       └──────────► Obstacle LED
```

---

# 🔊 FEEDBACK SYSTEM

## Buzzer

The buzzer provides an audible signal during obstacle response.

```text id="q9pjh0"
Obstacle Detected
       │
       ▼
    Reverse
       │
       ▼
 🔊 BUZZER ACTIVE
```

## LEDs

### 🔴 PCB LED

Indicates the PCB's power/operating state.

### 💡 Obstacle LED

Blinks while an obstacle is detected and the robot is reversing.

```text id="7m8y0u"
💡 ON
 │
 ▼
💡 OFF
 │
 ▼
💡 ON
 │
 ▼
💡 OFF
 │
 ▼
   ...
```

---

# 🧠 CONTROL SYSTEM

```text id="3m13v9"
                         START
                           │
                           ▼
                    INITIALIZE SYSTEM
                           │
                           ▼
                     MOVE FORWARD
                           │
                           ▼
                    READ HC-SR04
                           │
                           ▼
                     ┌───────────┐
                     │ OBSTACLE? │
                     └─────┬─────┘
                           │
                ┌──────────┴──────────┐
                │                     │
               NO                    YES
                │                     │
                ▼                     ▼
         MOVE FORWARD           MOVE BACKWARD
                                      │
                              ┌───────┴───────┐
                              │               │
                              ▼               ▼
                         🔊 BUZZER       💡 LED BLINK
                              │               │
                              └───────┬───────┘
                                      │
                                      ▼
                              CHECK DISTANCE
                                      │
                              ┌───────┴───────┐
                              │               │
                           PRESENT         CLEARED
                              │               │
                              │               ▼
                              │         MOVE FORWARD
                              │               │
                              └───────────────┘
```

---

# 🔄 STATE MODEL

MINI TBB operates primarily through two movement states.

### FORWARD

```text id="a6l5f7"
🟢 FORWARD

Motors   → Forward
Buzzer   → OFF
LED      → OFF
Sensor   → Monitoring
```

### REVERSE

```text id="e0e5wo"
🔴 REVERSE

Motors   → Backward
Buzzer   → ON
LED      → BLINK
Sensor   → Monitoring
```

### State Transition

```text id="xqv2x9"
        ┌─────────────┐
        │   FORWARD   │
        └──────┬──────┘
               │
        Obstacle detected
               │
               ▼
        ┌─────────────┐
        │   REVERSE   │
        └──────┬──────┘
               │
        Obstacle cleared
               │
               ▼
        ┌─────────────┐
        │   FORWARD   │
        └─────────────┘
```

---

# 💻 SOFTWARE

MINI TBB is programmed using the **Arduino IDE**.

### Technology Stack

| Layer                   | Technology     |
| ----------------------- | -------------- |
| Development Environment | Arduino IDE    |
| Controller              | ESP32-WROOM-32 |
| Programming             | Arduino C/C++  |
| Distance Sensor         | HC-SR04        |
| Motor Control           | Motor Driver   |
| Feedback                | Buzzer + LEDs  |

### Firmware Responsibilities

* Initialize ESP32 peripherals
* Read HC-SR04
* Detect obstacles
* Control motor direction
* Activate buzzer
* Blink obstacle LED
* Resume forward operation after obstacle clearance

---

# 📋 TECHNICAL SPECIFICATIONS

| Specification               | MINI TBB                |
| --------------------------- | ----------------------- |
| **Project Name**            | MINI TBB                |
| **Robot Type**              | Autonomous Mobile Robot |
| **Primary Function**        | Obstacle Avoidance      |
| **Drive Configuration**     | 2WD                     |
| **Motors**                  | 2 × Geared DC Motors    |
| **Wheels**                  | 2                       |
| **Main Controller**         | ESP32-WROOM-32          |
| **Ultrasonic Sensor**       | HC-SR04                 |
| **Sensor Count**            | 1                       |
| **Programming Environment** | Arduino IDE             |
| **Programming Language**    | Arduino C/C++           |
| **Operating Mode**          | Autonomous              |
| **Battery**                 | ICR-18650 Li-ion        |
| **Battery Voltage**         | 3.7 V                   |
| **Battery Capacity**        | 2200 mAh                |
| **Battery Energy**          | 8.14 Wh                 |
| **Charging**                | USB-C                   |
| **Power Conversion**        | DC-DC                   |
| **Main PCB**                | Custom                  |
| **Chassis**                 | Custom / 3D-printed     |
| **Obstacle Response**       | Reverse                 |
| **Audible Feedback**        | Buzzer                  |
| **Visual Feedback**         | LED                     |

---

# 🧪 TESTING

## 🟢 Test 01 — Startup

```text id="9p7u1p"
POWER ON
   │
   ▼
ESP32 START
   │
   ▼
🚗 FORWARD
```

---

## 🔴 Test 02 — Obstacle Detection

```text id="9r5qyp"
🚧 OBSTACLE
     │
     ▼
📡 HC-SR04
     │
     ▼
🧠 ESP32
     │
     ▼
🔄 REVERSE
     │
 ┌───┴───┐
 ▼       ▼
🔊       💡
BEEP    BLINK
```

---

## 🔄 Test 03 — Obstacle Remains

```text id="7axv2p"
Obstacle remains
       │
       ▼
🔄 Continue reversing
       │
       ▼
🔊 Buzzer active
       │
       ▼
💡 LED blinking
```

---

## 🟢 Test 04 — Path Clear

```text id="d6c9q7"
Obstacle removed
       │
       ▼
📡 Path clear
       │
       ▼
🚗 Forward movement
```

---

# 📸 MINI TBB GALLERY

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" width="45%" alt="MINI TBB Front View">
  <img src="assets/images/mini-tbb-side.jpg" width="45%" alt="MINI TBB Side View">
</p>

<p align="center">
  <img src="assets/images/mini-tbb-top.jpg" width="45%" alt="MINI TBB Top View">
  <img src="assets/images/pcb.jpg" width="45%" alt="MINI TBB Custom PCB">
</p>

---

# 📁 REPOSITORY STRUCTURE

```text id="yd5zq3"
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
│       ├── architecture.png
│       └── wiring.png
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
│   ├── hardware/
│   ├── assembly/
│   └── operation/
│
├── LICENSE
└── README.md
```

---

# 🏁 QUICK START

```text id="u8g3c9"
        ┌─────────────────┐
        │  POWER ON MINI  │
        │      TBB        │
        └────────┬────────┘
                 │
                 ▼
            🚗 FORWARD
                 │
                 ▼
            📡 DETECT
                 │
          ┌──────┴──────┐
          │             │
        CLEAR        OBSTACLE
          │             │
          │             ▼
          │         🔄 REVERSE
          │             │
          │        🔊 + 💡
          │             │
          │             ▼
          │       PATH CLEAR
          │             │
          └─────────────┘
                 │
                 ▼
            🚗 FORWARD
```

---

# 📜 LICENSE

This project is released under the **MIT License**.

See the `LICENSE` file for complete license terms.

---

# 🤖 MINI TBB

<p align="center">

### 📡 SENSE

↓

### 🧠 DECIDE

↓

### ⚙️ MOVE

↓

### 🔁 REPEAT

</p>

<p align="center">
  <strong>MINI TBB</strong><br>
  <em>A compact autonomous robotics platform.</em>
</p>
