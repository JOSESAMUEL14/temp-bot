# 🤖 MINI TBB

### SENSE · DECIDE · MOVE

**MINI TBB** is a compact autonomous two-wheel-drive robot powered by an **ESP32-WROOM-32** and programmed using the **Arduino IDE**.

The robot is designed to automatically detect obstacles using an **HC-SR04 ultrasonic sensor**. During normal operation, MINI TBB moves forward continuously. When an obstacle is detected, the robot automatically moves backward while activating a buzzer and blinking an indicator LED. It continues moving backward until the obstacle is cleared, after which it resumes forward movement.

---

## 🤖 About

**MINI TBB** is an autonomous robotics project that combines embedded programming, motor control, ultrasonic sensing, power electronics, and a custom robot control PCB into a compact mobile platform.

The robot uses an **ESP32-WROOM-32** as its main controller. An **HC-SR04 ultrasonic sensor** is mounted at the front of the robot to detect obstacles.

When the robot is powered on, it automatically begins moving forward. If an obstacle is detected, the ESP32 changes the robot's movement to reverse mode. During reverse movement, the buzzer provides an audible indication and an LED blinks to indicate the obstacle condition.

Once the obstacle is no longer detected, the robot automatically returns to forward movement.

> A compact autonomous robot built around sensing, decision-making, and movement.

---

## ⭐ Key Highlights

| Feature                 | Description                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| 🤖 Autonomous Operation | MINI TBB starts moving automatically when powered on              |
| 🚗 2-Wheel Drive        | Uses two geared DC motors and two wheels                          |
| 📡 Obstacle Detection   | HC-SR04 ultrasonic sensor detects obstacles in front of the robot |
| 🔄 Automatic Reverse    | Robot moves backward when an obstacle is detected                 |
| 🔁 Automatic Recovery   | Robot continues reversing until the obstacle is cleared           |
| ▶️ Forward Resume       | Robot automatically moves forward again after the path is clear   |
| 🔊 Audible Alert        | Buzzer operates during obstacle detection and reverse movement    |
| 💡 Visual Indicator     | LED blinks when an obstacle is detected and the robot reverses    |
| 🧠 ESP32 Control        | ESP32-WROOM-32 controls the robot's sensing and movement          |
| 🔌 Custom PCB           | Custom control PCB integrates the robot's electronics             |
| 🔋 Rechargeable Power   | Powered by a rechargeable 18650 Li-ion cell                       |
| 💻 Arduino Programming  | Developed and programmed using Arduino IDE                        |

---

## 📦 What's in the Box

### ⚡ Electronics & Control

* ✅ ESP32-WROOM-32 development board
* ✅ Custom MINI TBB control PCB
* ✅ Motor driver module
* ✅ DC-DC power conversion module
* ✅ USB-C charging module
* ✅ ON/OFF power switch

### 🚗 Motion Components

* ✅ 2 × Geared DC Motors
* ✅ 2 × Wheels
* ✅ Custom robot chassis

### 📡 Sensors

* ✅ 1 × HC-SR04 Ultrasonic Sensor

### 🔊 Indicators

* ✅ Buzzer
* ✅ PCB power/status LED
* ✅ Obstacle/reverse indicator LED

### 🔋 Power

* ✅ 1 × ICR-18650 Li-ion cell
* **Voltage:** 3.7 V
* **Capacity:** 2200 mAh
* **Energy:** 8.14 Wh

---

## 🔧 Specifications

| Specification        | Details                                  |
| -------------------- | ---------------------------------------- |
| Project Name         | MINI TBB                                 |
| Robot Type           | Autonomous Obstacle-Avoidance Robot      |
| Drive System         | 2-Wheel Drive (2WD)                      |
| Drive Motors         | 2 × Geared DC Motors                     |
| Wheels               | 2                                        |
| Microcontroller      | ESP32-WROOM-32                           |
| Sensor               | HC-SR04 Ultrasonic Sensor                |
| Sensor Quantity      | 1                                        |
| Programming          | Arduino IDE                              |
| Programming Language | Arduino C/C++                            |
| Control Mode         | Autonomous                               |
| Battery Type         | ICR-18650 Li-ion                         |
| Battery Voltage      | 3.7 V                                    |
| Battery Capacity     | 2200 mAh                                 |
| Battery Energy       | 8.14 Wh                                  |
| Charging Interface   | USB-C                                    |
| Motor Driver         | Motor Driver Module                      |
| Power Conversion     | DC-DC Converter                          |
| Chassis              | Custom / 3D-printed                      |
| Obstacle Response    | Reverse until obstacle is cleared        |
| Buzzer               | Active during reverse movement           |
| Obstacle LED         | Blinks during obstacle detection/reverse |
| PCB LED              | Indicates PCB/power status               |

---

## 🔌 Pin Connections

### 📡 HC-SR04 → ESP32

The HC-SR04 ultrasonic sensor is connected to the ESP32 as follows:

| HC-SR04 Pin | ESP32 / Power Connection |
| ----------- | ------------------------ |
| VCC         | 5V                       |
| TRIG        | GPIO 21                  |
| ECHO        | GPIO 22                  |
| GND         | GND                      |

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

MINI TBB follows a simple autonomous obstacle-response cycle.

```text
                    ┌──────────────┐
                    │   POWER ON   │
                    └──────┬───────┘
                           │
                           ▼
                  ┌────────────────┐
                  │ MOVE FORWARD   │
                  └───────┬────────┘
                          │
                          ▼
                  ┌────────────────┐
                  │   HC-SR04      │
                  │ CHECK DISTANCE  │
                  └───────┬────────┘
                          │
                     Obstacle?
                       /     \
                     NO       YES
                     │         │
                     │         ▼
                     │  ┌───────────────┐
                     │  │ MOVE BACKWARD │
                     │  │               │
                     │  │ 🔊 Buzzer     │
                     │  │ 💡 LED BLINK  │
                     │  └───────┬───────┘
                     │          │
                     │          ▼
                     │   Obstacle still
                     │      present?
                     │       /     \
                     │     YES      NO
                     │      │        │
                     │      │        ▼
                     │      │   MOVE FORWARD
                     │      │
                     └──────┘
```

### Operating Sequence

1. Turn the robot ON.
2. The ESP32 starts the programmed operation.
3. MINI TBB begins moving forward.
4. The HC-SR04 continuously checks for obstacles.
5. If no obstacle is detected, the robot continues moving forward.
6. When an obstacle is detected, the robot moves backward.
7. The buzzer operates during reverse movement.
8. The obstacle indicator LED blinks.
9. The robot continues reversing while the obstacle remains detected.
10. Once the obstacle is cleared, the robot moves forward again.
11. The process repeats continuously.

---

## 🔋 Power System

MINI TBB is powered by a single rechargeable **ICR-18650 Li-ion cell**.

### Battery Specifications

```text
Battery Type : Li-ion
Cell         : ICR-18650
Voltage      : 3.7 V
Capacity     : 2200 mAh
Energy       : 8.14 Wh
```

The battery supplies power to the robot through its custom PCB and power-management circuitry.

The robot includes:

* USB-C charging module
* DC-DC power conversion module
* ON/OFF power switch
* Custom PCB power distribution

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
        Custom PCB
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

MINI TBB uses a compact **2WD drivetrain**.

The robot contains:

* **2 × geared DC motors**
* **2 × wheels**

The motors provide both forward and backward movement.

### Movement Behavior

| Condition         | Robot Movement    |
| ----------------- | ----------------- |
| Robot powered ON  | Forward           |
| No obstacle       | Continue forward  |
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

                  ROBOT

             O           O
             │           │
          Motor 1     Motor 2
             │           │
             └─────┬─────┘
                   │
                2WD DRIVE
```

---

## 📡 Obstacle Detection

MINI TBB uses an **HC-SR04 ultrasonic sensor** mounted at the front of the robot.

The sensor measures the distance between the robot and objects in front of it.

The ESP32 receives the sensor information and uses it to control the robot's movement.

```text
             ┌─────────────┐
             │   HC-SR04   │
             └──────┬──────┘
                    │
             Distance Data
                    │
                    ▼
             ┌─────────────┐
             │    ESP32    │
             └──────┬──────┘
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
                      ┌─────┴─────┐
                      │           │
                   Buzzer      LED Blink
```

---

## 🔊 Buzzer & LED Indicators

### 🔊 Buzzer

The buzzer provides an audible indication when an obstacle is detected.

It operates while the robot is moving backward in response to the detected obstacle.

### 🔴 PCB Power LED

The custom PCB includes a red LED that indicates whether the PCB is powered/operating.

### 💡 Obstacle Indicator LED

A separate LED blinks when:

* An obstacle is detected.
* The robot enters reverse movement.

### Indicator Summary

| Indicator       | Function                                     |
| --------------- | -------------------------------------------- |
| 🔴 PCB Red LED  | Indicates PCB/power status                   |
| 💡 Obstacle LED | Blinks during obstacle detection and reverse |
| 🔊 Buzzer       | Beeps during obstacle detection and reverse  |

---

## 💻 Software

MINI TBB is programmed using the **Arduino IDE** and an ESP32 development environment.

### Development Platform

* **Arduino IDE**
* **ESP32-WROOM-32**
* **Arduino C/C++**

### Main Software Functions

The robot firmware controls:

* ESP32 initialization
* HC-SR04 distance sensing
* Obstacle detection
* Forward movement
* Reverse movement
* Motor control
* Buzzer activation
* Obstacle LED control

### Control Logic

```text
START
  │
  ▼
Initialize ESP32
  │
  ▼
Initialize HC-SR04
  │
  ▼
Initialize Motors
  │
  ▼
Move Forward
  │
  ▼
Read Distance
  │
  ├─────────────── Clear ──────────────┐
  │                                    │
  │                                    ▼
  │                              Move Forward
  │                                    │
  │                                    └─────┐
  │                                          │
  └── Obstacle Detected                     │
             │                               │
             ▼                               │
       Move Backward                        │
             │                               │
             ├── Buzzer ON                  │
             └── LED BLINK                  │
             │                               │
             ▼                               │
       Check Distance                        │
             │                               │
       Obstacle Present?                    │
          /       \                          │
        YES        NO                        │
         │          │                        │
         └──────────┘                        │
                    │                        │
                    ▼                        │
              Move Forward ◄────────────────┘
```

---

## 🚀 Getting Started

### 🔧 Hardware Setup

1. Assemble the MINI TBB chassis.
2. Install the two geared DC motors.
3. Install the two wheels.
4. Mount the HC-SR04 ultrasonic sensor at the front.
5. Install the ESP32-WROOM-32 onto the custom PCB.
6. Connect the motor driver and motors.
7. Connect the HC-SR04 sensor.
8. Connect the buzzer and indicator LED.
9. Install the ICR-18650 battery.
10. Verify the power connections.
11. Turn ON the robot.

### 💻 Software Setup

1. Install **Arduino IDE**.
2. Install ESP32 board support in Arduino IDE.
3. Connect the ESP32 to a computer using USB.
4. Select the appropriate ESP32 board.
5. Load the MINI TBB firmware.
6. Compile the program.
7. Upload the firmware to the ESP32.
8. Disconnect the USB cable.
9. Power ON MINI TBB.
10. Place the robot in a clear test area.

---

## 🧪 Testing

MINI TBB can be tested using the following sequence:

```text
Power ON
   │
   ▼
Robot moves forward
   │
   ▼
Place obstacle in front
   │
   ▼
HC-SR04 detects obstacle
   │
   ▼
Robot moves backward
   │
   ├── Buzzer beeps
   │
   └── LED blinks
   │
   ▼
Keep obstacle present
   │
   ▼
Robot continues backward
   │
   ▼
Remove obstacle
   │
   ▼
Robot detects clear path
   │
   ▼
Robot moves forward
```

### Expected Result

| Test              | Expected Behavior              |
| ----------------- | ------------------------------ |
| Power ON          | Robot starts moving forward    |
| Clear path        | Robot continues forward        |
| Obstacle detected | Robot reverses                 |
| During reverse    | Buzzer operates                |
| During reverse    | Indicator LED blinks           |
| Obstacle remains  | Robot continues reversing      |
| Obstacle removed  | Robot resumes forward movement |

---

## 📁 Repository Structure

A recommended repository structure for MINI TBB is:

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
       Power System                   Sensing System
             │                             │
     ┌───────┴───────┐              ┌──────┴──────┐
     │               │              │             │
  18650          DC-DC            HC-SR04       Front
  Battery        Converter        Ultrasonic     Detection
     │               │              │
     └───────┬───────┘              │
             │                      │
             ▼                      ▼
       ┌─────────────────────────────────┐
       │         CUSTOM PCB              │
       │                                 │
       │        ESP32-WROOM-32           │
       │               │                 │
       └───────────────┼─────────────────┘
                       │
             ┌─────────┼─────────┐
             │         │         │
             ▼         ▼         ▼
         Motor      Buzzer     Obstacle
         Driver                 LED
             │
        ┌────┴────┐
        ▼         ▼
     Motor 1   Motor 2
        │         │
        ▼         ▼
      Wheel     Wheel
```

---

## 🛠️ Hardware Architecture

```text
                 ┌──────────────────┐
                 │ ICR-18650 Li-ion │
                 │   3.7V 2200mAh   │
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
              ┌─────────────────────────┐
              │       MINI TBB PCB      │
              │                         │
              │   ┌─────────────────┐   │
              │   │ ESP32-WROOM-32  │   │
              │   └────────┬────────┘   │
              │            │            │
              │      ┌─────┴─────┐      │
              │      │   Motor   │      │
              │      │   Driver  │      │
              │      └─────┬─────┘      │
              └────────────┼────────────┘
                           │
                    ┌──────┴──────┐
                    │             │
                    ▼             ▼
                 Motor 1       Motor 2
                    │             │
                    ▼             ▼
                  Wheel         Wheel


          HC-SR04 ───────────► ESP32
          TRIG ──────────────► GPIO 21
          ECHO ──────────────► GPIO 22

          ESP32 ─────────────► Buzzer
          ESP32 ─────────────► Obstacle LED
          PCB ───────────────► Power LED
```

---

## 📄 License

This project is licensed under the **MIT License**.

See the `LICENSE` file in this repository for the complete license terms.

---

## 🤖 MINI TBB

MINI TBB demonstrates the fundamentals of autonomous robotics through a simple and practical control system.

Using an **ESP32-WROOM-32**, **HC-SR04 ultrasonic sensor**, **2WD motor system**, custom PCB, rechargeable Li-ion battery, buzzer, and LED indicators, the robot can independently sense obstacles and respond to them without manual control.

### Core Concept

```text
        SENSE
          ↓
       DECIDE
          ↓
        MOVE
          ↓
        REPEAT
```

**MINI TBB — A compact autonomous robot built to sense, decide, and move.**
