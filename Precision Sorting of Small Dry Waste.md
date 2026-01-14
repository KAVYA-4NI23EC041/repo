# Precision Sorting of Small Dry Waste 🌱♻️

### Innovation Design Thinking & Experiential Learning Project
**Department of Electronics and Communication Engineering**
**The National Institute of Engineering (NIE), Mysuru**

---

## 👥 Team Members

This project was a collaborative effort by the following members of the **Department of Electronics & Communication, NIE Mysore**:

* **Kavya G** 
* **Hemashree G N**
* **Disha N Bhushan**
* **Pooja K N**
* **Sapthami B P**
* **Nishkala**
---

## 📖 Abstract
This project presents the design and implementation of a prototype dry waste sorting machine specifically engineered to handle small particles. Traditional waste sorting methods struggle with fine materials, leading to inefficiency. Our prototype features a two-stage sorting process: waste is initially fed through a funnel onto a conveyor belt. Based on data from a sensor array (Metal Detector, IR Sensor, Moisture Sensor), a servomotor mechanism automatically pushes the waste into the correct bin (Plastic, Metal, Glass/Paper).

## 🎯 Objectives
The primary goal of this project is to automate the separation of dry waste to improve recycling efficiency.

* **♻️ Separate Recyclable Material:** Efficiently segregate plastics, paper, glass, and metals using sensor fusion.
* **📉 Prevent Co-Mingling:** Reduce cross-contamination in recycling streams to ensure higher material purity.
* **🗑️ Reduce Landfill Space:** Minimize total waste volume by diverting recyclable materials away from landfills.
* **🤖 Automation:** Eliminate the need for hazardous manual sorting of small, sharp, or dangerous waste particles.

---

## 🛠️ Hardware Components

| Component | Image | Qty | Purpose |
| :--- | :---: | :---: | :--- |
| **Arduino Uno** | <img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Arduino_Uno_-_R3.jpg" width="100"> | 1 | Main Microcontroller (The Brain) |
| **Inductive Sensor**<br>*(LJ12A3-4-Z/BX)* | <img width="284" height="177" alt="Image" src="https://github.com/user-attachments/assets/13613b57-59bf-414e-a73d-ca62abc1bd5a" /> | 1 | **Metal Detection:** Detects metallic waste (aluminum/iron) without physical contact. |
| **IR Sensor Module** | <img width="225" height="225" alt="Image" src="https://github.com/user-attachments/assets/11e2d4d5-2eaf-4e58-9fa3-7f65a9634a99" /> | 3 | **Object/Plastic Detection:** Detects obstacles and differentiates non-metals based on reflection. |
| **L298N Motor Driver** | <img width="218" height="232" alt="Image" src="https://github.com/user-attachments/assets/b29da22f-cf37-4372-87b2-3eb89d5e313b" /> | 1 | **Power Management:** Controls high-power DC motors using low-power Arduino signals. |
| **Soil Moisture Sensor** | <img width="242" height="208" alt="Image" src="https://github.com/user-attachments/assets/1e7c764f-b5a7-428b-ad53-3f92e65d8a1d" /> | 1 | **Wet Waste Detection:** Identifies if waste is wet/organic based on conductivity. |
| **Servo Motors**<br>*(SG90 / MG995)* | <img width="225" height="225" alt="Image" src="https://github.com/user-attachments/assets/e9f2ed3a-9e62-4b49-b53d-c63b80cf18e8" /> <img width="225" height="225" alt="Image" src="https://github.com/user-attachments/assets/5b15ad99-201a-45d5-903b-db852ad075d8" /> | 2 | **Sorting Arms:** Physically pushes the waste into the correct bin (Left/Right). |
| **DC Motors** | <img width="246" height="205" alt="image" src="https://github.com/user-attachments/assets/35afcf26-5761-4147-956a-e2793e936741" /> | 2 | **Conveyor System:** Drives the belt to move waste forward. |
| **Power Supply** | <img width="250" height="202" alt="Image" src="https://github.com/user-attachments/assets/3f89da73-0b3f-41a7-91bc-38d2f101e746" /> | 1 | Powers the L298N driver and motors. |


---

## 🔌 Circuit Connections

The system is centered around the **Arduino Uno**, acting as the central processing unit. The connections are divided into Sensor Inputs and Actuator Outputs.



[Image of Arduino Uno pinout diagram]


### Pin Configuration Table

| Type | Component | Arduino Pin | Description |
| :--- | :--- | :--- | :--- |
| **INPUT** | **Moisture Sensor** | `A0` (Analog) | Reads analog voltage to determine wetness. |
| **INPUT** | **Capacitive Sensor** | `D2` (Digital) | Logic HIGH/LOW for non-metallic detection. |
| **INPUT** | **Inductive Sensor** | `D3` (Digital) | Logic HIGH/LOW for metal detection. |
| **INPUT** | **IR Sensor** | `D4` (Digital) | Logic HIGH/LOW for object/glass presence. |
| | | | |
| **OUTPUT** | **Servo Motor 1** | `D5` (PWM) | Controls the "Plastic/Paper" sorting arm. |
| **OUTPUT** | **Servo Motor 2** | `D6` (PWM) | Controls the "Metal" sorting arm. |
| **OUTPUT** | **L298N (IN1)** | `D8` | DC Motor Direction Control A. |
| **OUTPUT** | **L298N (IN2)** | `D9` | DC Motor Direction Control B. |
| **OUTPUT** | **L298N (EN1)** | `D10` (PWM) | DC Motor Speed Control. |


---
<br>
<img width="695" height="546" alt="Image" src="https://github.com/user-attachments/assets/302eec77-b2ef-4656-bc40-9db49b332c91" />
<br>

## ⚙️ Methodology & Working

The system operates on a continuous feedback loop. The waste segregation process is divided into three distinct stages:

### Step 1: Input & Feed Mechanism 📥
* **Singulation:** Waste is fed into a funnel/hopper structure. This ensures that particles drop onto the conveyor belt **one by one**, preventing overlap that could confuse the sensors.
* **Transport:** A conveyor belt, driven by DC motors, transports the waste towards the sensor array at a constant speed.

### Step 2: Multi-Sensor Detection 📡
As the waste moves along the belt, it passes through a series of sensors:
1.  **Moisture Sensor:** Immediately checks for wet/organic waste to prevent contamination of dry recyclables.
2.  **Inductive Proximity Sensor:** Generates an electromagnetic field to detect **Ferrous/Non-Ferrous Metals**.
3.  **Capacitive/IR Sensor:** Distinguishes between non-metallic solids (Plastics) and other debris based on dielectric properties and light reflection.

### Step 3: Actuation & Sorting 🦾
The **Arduino Uno** processes the signals in real-time and controls the Servo Motors:

| Condition Detected | Active Sensor | Action Taken | Target Bin |
| :--- | :--- | :--- | :--- |
| **Metal** | Inductive Sensor (HIGH) | **Servo 2** rotates 90° | **Bin A (Metal)** |
| **Plastic/Paper** | Capacitive Sensor (HIGH) | **Servo 1** rotates 90° | **Bin B (Plastic)** |
| **Glass/Others** | No Sensor Trigger | No Action (Belt continues) | **Bin C (Default)** |
| **Wet Waste** | Moisture Sensor (HIGH) | *System Alert / Stop* | *Manual Removal* |

---

## 📊 Cost Estimation

The total estimated cost for the prototype was approximately **₹3,300**.

| Item | Cost (₹) |
| :--- | :--- |
| Arduino | 350 |
| Sensors (IR, Inductive, etc.) | ~550 |
| Motors (DC + Servo) | 700 |
| Power Supply & Driver | ~750 |
| Mechanical (Belt, Body) | ~950 |

---

## 🚀 Future Scope
* **AI Integration:** Using cameras and Image Processing for higher accuracy.
* **IoT:** Remote monitoring of bin levels.
* **Solar Power:** Making the system self-sustainable.

---

### 2. System Architecture (Wiring Logic)

**Flowchart:**
This diagram illustrates the data flow from the sensors to the microcontroller and finally to the actuators.

```mermaid
graph TD
    subgraph SENSORS [INPUTS]
    A[Moisture Sensor] -->|Analog Signal| A0(Arduino A0)
    B[Capacitive Sensor] -->|Digital Signal| D2(Arduino D2)
    C[Inductive Sensor] -->|Digital Signal| D3(Arduino D3)
    D[IR Sensor] -->|Digital Signal| D4(Arduino D4)
    end

    subgraph CONTROLLER [PROCESSING]
    UNO[Arduino Uno]
    A0 --> UNO
    D2 --> UNO
    D3 --> UNO
    D4 --> UNO
    end

    subgraph ACTUATORS [OUTPUTS]
    UNO -->|PWM| S1[Servo 1: Plastic]
    UNO -->|PWM| S2[Servo 2: Metal]
    UNO -->|Control Signal| MD[L298N Driver]
    MD -->|Power| BELT[Conveyor Belt]
    end




