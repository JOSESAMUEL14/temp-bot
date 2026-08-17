# 🤖 MINI TBB

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" alt="MINI TBB Autonomous Robot" width="700">
</p>

<p align="center">
  <strong>Autonomous 2WD Obstacle-Avoidance Robot</strong>
</p>

<p align="center">
  <code>ESP32-WROOM-32</code> · <code>HC-SR04</code> · <code>Arduino IDE</code> · <code>Custom PCB</code>
</p>

---

## 📖 Overview

**MINI TBB** is a compact autonomous mobile robot based on an **ESP32-WROOM-32** microcontroller.

The robot uses a front-mounted **HC-SR04 ultrasonic sensor** to detect obstacles. When powered on, it automatically moves forward. If an obstacle is detected, the robot switches to reverse movement and continues reversing until the obstacle is no longer detected.

During reverse operation:

* 🔊 The buzzer provides audible feedback.
* 💡 The obstacle indicator LED blinks.

After the path becomes clear, the robot automatically resumes forward movement.

The system therefore follows a simple autonomous control cycle:

```text id="eqm2ua"
        SENSE
          ↓
        DECIDE
          ↓
        MOVE
          ↓
        REPEAT
```

---

# 🧩 System Overview

```text id="qu5t1a"
                         ┌──────────────────┐
                         │  ICR-18650 Cell  │
                         │   3.7V / 2200mAh │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Power / Charging │
                         │     Circuit      │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │   DC-DC Module   │
                         └────────┬─────────┘
                                  │
                                  ▼
              ┌────────────────────────────────────┐
              │            MINI TBB PCB            │
              │                                    │
              │       ┌────────────────────┐       │
              │       │  ESP32-WROOM-32    │       │
              │       └─────────┬──────────┘       │
              │                 │                  │
              │          ┌──────┴──────┐           │
              │          │ Motor Driver│           │
              │          └──────┬──────┘           │
              └─────────────────┼──────────────────┘
                                │
                       ┌────────┴────────┐
                       │                 │
                       ▼                 ▼
                    Motor 1           Motor 2
                       │                 │
                       ▼                 ▼
                     Wheel             Wheel


              HC-SR04 ───────────► ESP32
              GPIO21 ────────────► TRIG
              GPIO22 ◄──────────── ECHO

              ESP32 ─────────────► Buzzer
              ESP32 ─────────────► Obstacle LED
              PCB ───────────────► Power LED
```

---

# ⚙️ Functional Architecture

MINI TBB can be divided into five primary subsystems.

```text id="2f7dbr"
┌──────────────────────────────────────────────────┐
│                    MINI TBB                      │
├──────────────────────────────────────────────────┤
│                                                  │
│  1. POWER                                        │
│     Battery → Switch → Power Conversion         │
│                                                  │
│  2. CONTROL                                      │
│     ESP32-WROOM-32                               │
│                                                  │
│  3. SENSING                                      │
│     HC-SR04 Ultrasonic Sensor                    │
│                                                  │
│  4. ACTUATION                                    │
│     Motor Driver → 2 DC Motors → 2 Wheels       │
│                                                  │
│  5. FEEDBACK                                     │
│     Buzzer + Obstacle LED + PCB LED              │
│                                                  │
└──────────────────────────────────────────────────┘
```

---

# 🧠 Controller

## ESP32-WROOM-32

The ESP32-WROOM-32 acts as the primary controller.

It receives distance information from the HC-SR04 and controls the robot's response.

### Controller Responsibilities

```text id="v7y0kq"
HC-SR04
   │
   │ Distance
   ▼
ESP32-WROOM-32
   │
   ├────────► Motor Driver
   │              │
   │              ├──► Motor 1
   │              └──► Motor 2
   │
   ├────────► Buzzer
   │
   └────────► Obstacle LED
```

---

# 📡 Distance Sensing

## HC-SR04 Ultrasonic Sensor

MINI TBB uses one **HC-SR04 ultrasonic sensor** positioned at the front of the robot.

The sensor provides the distance information required for obstacle detection.

### Interface

| HC-SR04 Signal | Connection    |
| -------------- | ------------- |
| VCC            | 5V            |
| TRIG           | ESP32 GPIO 21 |
| ECHO           | ESP32 GPIO 22 |
| GND            | GND           |

### Electrical Interface

```text id="qk7g2s"
             +----------------+
             |    HC-SR04     |
             |                |
5V ──────────┤ VCC            |
GPIO 21 ─────┤ TRIG           |
GPIO 22 ─────┤ ECHO           |
GND ─────────┤ GND            |
             +----------------+
```

---

# ⚙️ Drive Subsystem

MINI TBB uses a **two-wheel-drive configuration**.

### Components

* 2 × geared DC motors
* 2 × wheels
* Motor driver module

### Drive Layout

```text id="jy0h3a"
                    FRONT
                      ▲
                      │
                ┌───────────┐
                │  HC-SR04  │
                └───────────┘

                  O       O
                  │       │
                  │       │
               Motor 1  Motor 2
                  │       │
                  └───┬───┘
                      │
                     2WD
```

### Movement States

| State             | Movement |
| ----------------- | -------- |
| Startup           | Forward  |
| Clear path        | Forward  |
| Obstacle detected | Reverse  |
| Obstacle remains  | Reverse  |
| Obstacle cleared  | Forward  |

---

# 🔊 Feedback Subsystem

MINI TBB provides both audible and visual feedback.

## Buzzer

The buzzer operates when the robot detects an obstacle and enters reverse movement.

```text id="8bgbff"
Obstacle
   │
   ▼
Reverse
   │
   ▼
Buzzer ON
```

## LEDs

### PCB LED

The red PCB LED indicates the power/operating state of the PCB.

### Obstacle LED

The separate obstacle indicator LED blinks during obstacle detection and reverse movement.

```text id="k58kj4"
Obstacle Detected
       │
       ├────► 🔊 Buzzer
       │
       └────► 💡 LED Blink
```

---

# 🔋 Power Subsystem

MINI TBB uses a single rechargeable **ICR-18650 Li-ion cell**.

### Battery Specification

| Parameter       | Value     |
| --------------- | --------- |
| Chemistry       | Li-ion    |
| Cell            | ICR-18650 |
| Nominal Voltage | 3.7 V     |
| Capacity        | 2200 mAh  |
| Energy          | 8.14 Wh   |

### Power Components

* ICR-18650 battery
* USB-C charging module
* ON/OFF switch
* DC-DC conversion module
* Custom PCB

### Power Architecture

```text id="l5eg3f"
            USB-C
               │
               ▼
       ┌───────────────┐
       │ Charging      │
       │ Module        │
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │ 18650 Battery │
       │ 3.7V / 2200mAh│
       └───────┬───────┘
               │
               ▼
          ON / OFF
            Switch
               │
               ▼
       ┌───────────────┐
       │ DC-DC Power   │
       │ Conversion    │
       └───────┬───────┘
               │
               ▼
          MINI TBB PCB
```

---

# 🔌 Custom PCB

The MINI TBB electronics are integrated through a custom control PCB.

The PCB provides the main interconnection between the controller, power system, motor system, sensor, and indicators.

### PCB Functions

```text id="t8s7l9"
                    CUSTOM PCB
                         │
       ┌─────────────────┼──────────────────┐
       │                 │                  │
       ▼                 ▼                  ▼
    ESP32            Motor Driver       Power
       │                 │                  │
       │           ┌─────┴─────┐            │
       │           ▼           ▼            │
       │        Motor 1      Motor 2         │
       │                                     │
       ├────────► HC-SR04                    │
       ├────────► Buzzer                     │
       └────────► Obstacle LED               │
```

---

# 🔌 Interface Connections

### HC-SR04

```text id="q1s8n0"
VCC   → 5V
TRIG  → GPIO21
ECHO  → GPIO22
GND   → GND
```

### Main Functional Interfaces

| Interface    | Function                    |
| ------------ | --------------------------- |
| ESP32        | Main controller             |
| HC-SR04      | Obstacle sensing            |
| Motor Driver | DC motor control            |
| Motor 1      | Drive                       |
| Motor 2      | Drive                       |
| Buzzer       | Audible feedback            |
| Obstacle LED | Reverse/obstacle indication |
| PCB LED      | PCB/power indication        |
| USB-C        | Battery charging            |
| Power Switch | Robot power control         |

---

# 🧠 Control Algorithm

The robot's autonomous behavior follows this sequence:

```text id="n4obg1"
START
  │
  ▼
INITIALIZE
  │
  ├── ESP32
  ├── HC-SR04
  ├── Motors
  ├── Buzzer
  └── LED
  │
  ▼
MOVE FORWARD
  │
  ▼
READ ULTRASONIC SENSOR
  │
  ▼
CHECK FOR OBSTACLE
  │
  ├────────────── CLEAR ──────────────┐
  │                                   │
  │                                   ▼
  │                             MOVE FORWARD
  │                                   │
  │                                   │
  └──────────── OBSTACLE ─────────────┘
                    │
                    ▼
              MOVE BACKWARD
                    │
             ┌──────┴──────┐
             │             │
             ▼             ▼
        BUZZER ON      LED BLINK
             │             │
             └──────┬──────┘
                    │
                    ▼
           CHECK OBSTACLE
                    │
             ┌──────┴──────┐
             │             │
          PRESENT        CLEARED
             │             │
             │             ▼
             │       MOVE FORWARD
             │             │
             └─────────────┘
```

---

# 🔄 State Machine

MINI TBB can be represented using three primary operating states.

```text id="t7kg5v"
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

### State Actions

| State   | Motor    | Buzzer | LED   |
| ------- | -------- | ------ | ----- |
| FORWARD | Forward  | OFF    | OFF   |
| REVERSE | Backward | ON     | Blink |

---

# 💻 Software

MINI TBB is programmed using the **Arduino IDE**.

### Software Platform

```text id="1x8vl4"
Arduino IDE
     │
     ▼
Arduino C/C++
     │
     ▼
ESP32-WROOM-32
     │
     ├── HC-SR04
     ├── Motor Driver
     ├── Buzzer
     └── LED
```

### Software Responsibilities

The firmware handles:

* ESP32 initialization
* Ultrasonic distance measurement
* Obstacle detection
* Forward motor control
* Reverse motor control
* Buzzer control
* Obstacle LED control

---

# 📋 Technical Specifications

| Parameter                   | Specification           |
| --------------------------- | ----------------------- |
| **Project Name**            | MINI TBB                |
| **Robot Type**              | Autonomous Mobile Robot |
| **Navigation**              | Obstacle Avoidance      |
| **Drive Configuration**     | 2WD                     |
| **Drive Motors**            | 2 × Geared DC Motors    |
| **Wheels**                  | 2                       |
| **Controller**              | ESP32-WROOM-32          |
| **Sensor**                  | HC-SR04                 |
| **Sensor Quantity**         | 1                       |
| **Programming Environment** | Arduino IDE             |
| **Programming Language**    | Arduino C/C++           |
| **Operating Mode**          | Autonomous              |
| **Battery Chemistry**       | Li-ion                  |
| **Battery Cell**            | ICR-18650               |
| **Battery Voltage**         | 3.7 V                   |
| **Battery Capacity**        | 2200 mAh                |
| **Battery Energy**          | 8.14 Wh                 |
| **Charging Interface**      | USB-C                   |
| **Power Conversion**        | DC-DC                   |
| **PCB**                     | Custom                  |
| **Chassis**                 | Custom / 3D-printed     |
| **Obstacle Response**       | Reverse                 |
| **Audible Feedback**        | Buzzer                  |
| **Visual Feedback**         | LED                     |

---

# 🚀 Getting Started

## Hardware

Prepare the MINI TBB hardware:

```text id="q7d2hs"
ESP32-WROOM-32
       │
       ├── HC-SR04
       ├── Motor Driver
       ├── Buzzer
       └── Obstacle LED

Motor Driver
       │
       ├── Motor 1
       └── Motor 2

Battery
       │
       └── Power System
```

## Assembly

1. Assemble the robot chassis.
2. Mount both geared DC motors.
3. Attach both wheels.
4. Mount the HC-SR04 at the front.
5. Install the ESP32 on the custom PCB.
6. Connect the motor driver.
7. Connect both motors.
8. Connect the buzzer.
9. Connect the obstacle LED.
10. Install the battery.
11. Verify all power connections.

## Programming

1. Install Arduino IDE.
2. Configure ESP32 board support.
3. Connect the ESP32 using USB.
4. Select the correct ESP32 board.
5. Open the MINI TBB firmware.
6. Compile the program.
7. Upload the firmware.
8. Disconnect USB.
9. Power ON the robot.

---

# 🧪 Validation & Testing

### Test 1 — Startup

**Input:** Power ON.

**Expected:**

```text id="sv5p0v"
ESP32 starts
    ↓
Robot begins moving
    ↓
FORWARD
```

### Test 2 — Obstacle

**Input:** Place an obstacle in front of the robot.

**Expected:**

```text id="qzv2cr"
HC-SR04
   ↓
Obstacle detected
   ↓
Reverse
   ├── Buzzer
   └── LED Blink
```

### Test 3 — Obstacle Persistence

**Input:** Keep the obstacle in front of the robot.

**Expected:**

```text id="pl4w3u"
Obstacle remains
      ↓
Continue reversing
```

### Test 4 — Obstacle Removal

**Input:** Remove the obstacle.

**Expected:**

```text id="z6qgqp"
Obstacle cleared
      ↓
Forward movement resumes
```

---

# 📸 MINI TBB

<p align="center">
  <img src="assets/images/mini-tbb-front.jpg" width="600" alt="MINI TBB">
</p>

<p align="center">
  <i>MINI TBB — Autonomous 2WD Obstacle-Avoidance Robot</i>
</p>

---

# 📁 Repository Structure

```text id="c0a6x1"
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

# 📜 License

This project is released under the **MIT License**.

See the `LICENSE` file for the complete license terms.

---

# 🤖 MINI TBB

```text id="4p7t7m"
       ┌─────────────┐
       │ 📡  SENSE   │
       └──────┬──────┘
              │
              ▼
       ┌─────────────┐
       │ 🧠 DECIDE   │
       └──────┬──────┘
              │
              ▼
       ┌─────────────┐
       │ ⚙️  MOVE    │
       └──────┬──────┘
              │
              ▼
       ┌─────────────┐
       │ 🔁  REPEAT  │
       └─────────────┘
```

### **MINI TBB**

**Autonomous Robotics • Embedded Control • Obstacle Avoidance**
