# 🤖 MINI TBB

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" alt="MINI TBB" width="700">
</p>

<h1 align="center">MINI TBB</h1>

<p align="center">
  <strong>Autonomous 2WD Obstacle-Avoidance Robot</strong>
</p>

<p align="center">
  <b>📡 SENSE → 🧠 DECIDE → ⚙️ MOVE → 🔁 REPEAT</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/ESP32-WROOM--32-blue?style=for-the-badge&logo=espressif" alt="ESP32">
  <img src="https://img.shields.io/badge/Arduino-IDE-00979D?style=for-the-badge&logo=arduino" alt="Arduino">
  <img src="https://img.shields.io/badge/Drive-2WD-orange?style=for-the-badge" alt="2WD">
  <img src="https://img.shields.io/badge/Sensor-HC--SR04-green?style=for-the-badge" alt="HC-SR04">
</p>

---

# 🎬 MINI TBB IN ACTION

> Replace the image below with a GIF of your actual robot once you record it.

<p align="center">
  <img src="assets/mini-tbb-demo.gif" alt="MINI TBB Demonstration" width="700">
</p>

### 🤖 Robot Behavior

```text
        🚗 FORWARD
             │
             ▼
        📡 SCAN PATH
             │
             ▼
       ┌─────────────┐
       │  OBSTACLE?  │
       └──────┬──────┘
              │
        ┌─────┴─────┐
        │           │
       NO          YES
        │           │
        ▼           ▼
   🚗 FORWARD   🔄 REVERSE
                    │
              ┌─────┴─────┐
              │           │
           🔊 BEEP     💡 BLINK
              │           │
              └─────┬─────┘
                    │
                    ▼
             PATH CLEAR?
                    │
                    ▼
               🚗 FORWARD
```

---

# 🧠 WHAT IS MINI TBB?

**MINI TBB** is an autonomous two-wheel-drive robot built around an **ESP32-WROOM-32**.

Its primary task is simple:

> **Move forward until an obstacle is detected, reverse while the obstacle remains, and automatically continue forward once the path is clear.**

The robot combines:

* 🧠 ESP32-WROOM-32
* 📡 HC-SR04 ultrasonic sensing
* ⚙️ Two geared DC motors
* 🛞 Two-wheel drive
* 🔌 Custom control PCB
* 🔋 Rechargeable Li-ion battery
* 🔊 Buzzer feedback
* 💡 LED indication
* 💻 Arduino IDE

---

# ⚡ THE MINI TBB LOOP

```text
                 ┌───────────────┐
                 │    POWER ON   │
                 └───────┬───────┘
                         │
                         ▼
                 ┌───────────────┐
                 │ 🚗 FORWARD    │
                 └───────┬───────┘
                         │
                         ▼
                 ┌───────────────┐
                 │ 📡 HC-SR04    │
                 │ DISTANCE READ │
                 └───────┬───────┘
                         │
                         ▼
                    ┌─────────┐
                    │ CLEAR ? │
                    └────┬────┘
                         │
                ┌────────┴────────┐
                │                 │
               YES               NO
                │                 │
                │                 ▼
                │          ┌─────────────┐
                │          │ 🔄 REVERSE  │
                │          └──────┬──────┘
                │                 │
                │          ┌──────┴──────┐
                │          │             │
                │       🔊 BEEP       💡 BLINK
                │          │             │
                │          └──────┬──────┘
                │                 │
                │                 ▼
                │          OBSTACLE GONE?
                │                 │
                │            ┌────┴────┐
                │           YES       NO
                │            │         │
                │            │         └──────┐
                │            │                │
                └────────────┴────────────────┘
                             │
                             ▼
                       🚗 FORWARD
```

---

# ✨ KEY FEATURES

<table>
<tr>
<td align="center">🤖<br><b>Autonomous</b><br>Starts automatically</td>
<td align="center">📡<br><b>Ultrasonic</b><br>HC-SR04 sensing</td>
<td align="center">🚗<br><b>2WD</b><br>Two motors</td>
</tr>
<tr>
<td align="center">🔄<br><b>Reverse</b><br>Obstacle response</td>
<td align="center">🔊<br><b>Buzzer</b><br>Audible feedback</td>
<td align="center">💡<br><b>LED</b><br>Visual feedback</td>
</tr>
<tr>
<td align="center">🧠<br><b>ESP32</b><br>Main controller</td>
<td align="center">🔌<br><b>Custom PCB</b><br>Integrated electronics</td>
<td align="center">🔋<br><b>Li-ion</b><br>Rechargeable power</td>
</tr>
</table>

---

# 🧩 HARDWARE

## 🧠 Controller

### ESP32-WROOM-32

The ESP32-WROOM-32 is the main controller of MINI TBB.

It handles:

```text
HC-SR04
   │
   ▼
ESP32
   │
   ├──► Motor Driver
   │
   ├──► Buzzer
   │
   └──► Obstacle LED
```

---

## 📡 Distance Sensor

### HC-SR04

The front-mounted HC-SR04 provides obstacle-distance information.

### Pin Configuration

| HC-SR04 | MINI TBB |
| ------- | -------- |
| VCC     | 5V       |
| TRIG    | GPIO 21  |
| ECHO    | GPIO 22  |
| GND     | GND      |

```text
       HC-SR04
      ┌─────────┐
      │         │
VCC ──┤         ├── 5V
TRIG──┤         ├── GPIO 21
ECHO──┤         ├── GPIO 22
GND ──┤         ├── GND
      └─────────┘
```

---

# ⚙️ MOTION

MINI TBB uses a **2WD configuration**.

```text
                 FRONT
                   ▲
                   │

             ┌───────────┐
             │  HC-SR04  │
             └───────────┘

               ◯     ◯
               │     │
             M1       M2
               │     │
               └──┬──┘
                  │
                 2WD
```

### Movement States

```text
🟢 CLEAR
   ↓
🚗 FORWARD

🔴 OBSTACLE
   ↓
🔄 REVERSE
   ↓
🔊 BEEP
💡 BLINK
   ↓
🟢 CLEAR
   ↓
🚗 FORWARD
```

---

# 🔋 POWER

MINI TBB uses one rechargeable **ICR-18650 Li-ion cell**.

| Specification | Value     |
| ------------- | --------- |
| Cell          | ICR-18650 |
| Chemistry     | Li-ion    |
| Voltage       | 3.7 V     |
| Capacity      | 2200 mAh  |
| Energy        | 8.14 Wh   |

### Power Components

* 🔋 ICR-18650 battery
* 🔌 USB-C charging module
* 🔘 ON/OFF switch
* ⚡ DC-DC conversion module
* 🟢 Custom PCB

### Power Flow

```text
       🔋 BATTERY
           │
           ▼
      🔘 ON / OFF
           │
           ▼
      ⚡ POWER
           │
           ▼
      🔌 DC-DC
           │
           ▼
      🟢 CUSTOM PCB
           │
      ┌────┴────┐
      ▼         ▼
    🧠 ESP32   ⚙️ MOTORS
```

---

# 🔊 INDICATORS

## Buzzer

The buzzer activates during reverse movement after an obstacle is detected.

```text
Obstacle
   ↓
🔄 Reverse
   ↓
🔊 Buzzer ON
```

## LEDs

### 🔴 PCB LED

Shows the operating/power state of the PCB.

### 💡 Obstacle LED

Blinks when the robot detects an obstacle and starts reversing.

```text
OBSTACLE
   ↓
💡 ON
   ↓
💡 OFF
   ↓
💡 ON
   ↓
💡 OFF
```

---

# 🏗️ CUSTOM PCB

The MINI TBB electronics are integrated around a custom control PCB.

The board provides connections for the robot's:

* ESP32 controller
* Motor system
* Ultrasonic sensor
* Buzzer
* LEDs
* Power system
* Expansion connections

### PCB Concept

```text
                 MINI TBB PCB
        ┌──────────────────────────┐
        │                          │
        │    ┌────────────────┐    │
        │    │ ESP32-WROOM-32 │    │
        │    └───────┬────────┘    │
        │            │             │
        │       ┌────┴────┐        │
        │       │  MOTOR  │        │
        │       │  DRIVER │        │
        │       └────┬────┘        │
        │            │             │
        │   HC-SR04  │  BUZZER     │
        │      │     │     │       │
        │      │     │     │       │
        │      ▼     ▼     ▼       │
        │      📡    ⚙️    🔊      │
        │                          │
        └──────────────────────────┘
```

---

# 📋 SPECIFICATIONS

| Category          | MINI TBB                            |
| ----------------- | ----------------------------------- |
| Robot Type        | Autonomous Obstacle-Avoidance Robot |
| Drive             | 2WD                                 |
| Motors            | 2 × Geared DC Motors                |
| Wheels            | 2                                   |
| Controller        | ESP32-WROOM-32                      |
| Sensor            | HC-SR04                             |
| Sensor Quantity   | 1                                   |
| Programming       | Arduino IDE                         |
| Language          | Arduino C/C++                       |
| Operation         | Autonomous                          |
| Battery           | ICR-18650 Li-ion                    |
| Battery Voltage   | 3.7 V                               |
| Battery Capacity  | 2200 mAh                            |
| Battery Energy    | 8.14 Wh                             |
| Charging          | USB-C                               |
| PCB               | Custom                              |
| Chassis           | Custom / 3D-printed                 |
| Obstacle Response | Reverse                             |
| Audible Feedback  | Buzzer                              |
| Visual Feedback   | LED                                 |

---

# 🧠 SOFTWARE

MINI TBB is programmed using **Arduino IDE**.

### Software Stack

```text
┌─────────────────────┐
│     Arduino IDE     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Arduino C/C++    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   ESP32-WROOM-32    │
└──────────┬──────────┘
           │
      ┌────┼────┐
      ▼    ▼    ▼
    📡    ⚙️    🔊
 HC-SR04 Motors Buzzer
```

---

# 🔄 CONTROL STATES

| State       | Movement | Buzzer | LED   |
| ----------- | -------- | ------ | ----- |
| 🟢 FORWARD  | Forward  | OFF    | OFF   |
| 🔴 OBSTACLE | Reverse  | ON     | Blink |
| 🔄 REVERSE  | Reverse  | ON     | Blink |
| 🟢 CLEAR    | Forward  | OFF    | OFF   |

---

# 🚀 GETTING STARTED

## Hardware

1. Assemble the MINI TBB chassis.
2. Mount the two geared DC motors.
3. Install the two wheels.
4. Mount the HC-SR04 at the front.
5. Install the ESP32-WROOM-32 on the custom PCB.
6. Connect the motor driver.
7. Connect the motors.
8. Connect the HC-SR04.
9. Connect the buzzer and LEDs.
10. Install the battery.
11. Check the power connections.

## Software

1. Install Arduino IDE.
2. Install ESP32 board support.
3. Connect ESP32 through USB.
4. Select the appropriate ESP32 board.
5. Load the MINI TBB firmware.
6. Compile the program.
7. Upload the firmware.
8. Disconnect USB.
9. Turn ON the robot.

---

# 🧪 TESTING

### Test 01 — Start

```text
POWER ON
   ↓
🚗 FORWARD
```

### Test 02 — Obstacle

```text
📡 OBSTACLE DETECTED
        ↓
🔄 REVERSE
        ↓
🔊 BUZZER
💡 LED
```

### Test 03 — Clear

```text
🚧 OBSTACLE REMOVED
        ↓
📡 PATH CLEAR
        ↓
🚗 FORWARD
```

---

# 📸 MINI TBB GALLERY

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" width="45%" alt="MINI TBB Front">
  <img src="assets/images/mini-tbb-side.jpg" width="45%" alt="MINI TBB Side">
</p>

<p align="center">
  <img src="assets/images/mini-tbb-top.jpg" width="45%" alt="MINI TBB Top">
  <img src="assets/images/pcb.jpg" width="45%" alt="MINI TBB PCB">
</p>

---

# 🏛️ SYSTEM ARCHITECTURE

```text
                         🔋 POWER
                            │
                            ▼
                    ┌──────────────┐
                    │   DC-DC      │
                    │ CONVERSION    │
                    └──────┬───────┘
                           │
                           ▼
              ┌────────────────────────┐
              │       MINI TBB PCB      │
              │                        │
              │   🧠 ESP32-WROOM-32   │
              └────────────┬───────────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
       📡 HC-SR04       ⚙️ MOTOR        🔊 BUZZER
                           DRIVER
                              │
                       ┌──────┴──────┐
                       ▼             ▼
                    MOTOR 1       MOTOR 2
                       │             │
                       ▼             ▼
                     WHEEL         WHEEL

                   ESP32
                     │
                     ▼
                💡 OBSTACLE LED
```

---

# 📁 REPOSITORY

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

# 📜 LICENSE

This project is released under the **MIT License**.

See the `LICENSE` file for the complete license terms.

---

# 🤖 MINI TBB

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

### **MINI TBB**

### *SENSE • DECIDE • MOVE*
