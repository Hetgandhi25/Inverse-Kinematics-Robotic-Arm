# 🤖 Inverse Kinematics in a 3-Link Robotic Arm  

This project implements **Inverse Kinematics (IK)** for a **3-link robotic arm** using an **Arduino-compatible setup**. It calculates **joint angles** based on the given **end-effector coordinates** (x, y) and orientation (θ), enabling precise control of the robotic arm’s movement.

---

## 📌 **Project Overview**  
This project aims to:  
✅ Compute joint angles **(θ1, θ2, θ3)** using inverse kinematics formulas.  
✅ Control the **Braccio Robotic Arm** using an **Arduino Uno**.  
✅ Move the robotic arm to a **specified position** based on calculated angles.  

---

## 🔧 **Hardware & Materials Required**  
The following components were used in this project:  
- 🖥 **Arduino Uno** (Microcontroller)  
- 🤖 **Arduino Tinkerkit Braccio Robotic Arm**  
- 🔌 **Arduino Compatible Shield**  
- ⚡ **Power Adapter**  
- 🧩 **USB Cable** for programming  

---

## 📋 **Project Setup & Installation**

### 1️⃣ **Install Arduino IDE**  
Download the Arduino IDE from the official website:  
[Arduino Official Site](https://www.arduino.cc/en/software)

### 2️⃣ **Connect the Components**  
- Plug the **Arduino Uno** into your PC.
- Attach the **Braccio Robotic Arm** to the Arduino using the provided connectors and wires.

### 3️⃣ **Upload the Code**  
- Copy the provided C++ code into the Arduino IDE.
- Click **Upload** to upload the code to the Arduino Uno.

---

## 🔩 **Test Cases**

Tested with various (x, y, θ) coordinates:

| Task No. | (x, y) Coordinates | θ (Orientation) |
|----------|---------------------|-----------------|
| 1️⃣       | (0, 314)             | 90°             |
| 2️⃣       | (157, 271.93)        | 60°             |
| 3️⃣       | (314, 0)             | 0°              |
| 4️⃣       | (271.93, 157)        | 30°             |
| 5️⃣       | (222, 222)           | 45°             |

---

## 🎥 **Demo & Results**

You can view the output demo of the robotic arm moving to different target positions via the following link:  
[Watch the output here](https://www.youtube.com/watch?v=gsnxKZ3Plk0)

### ✅ **Observations:**
- Successfully calculated and executed inverse kinematics.
- The robotic arm moved precisely to different target positions.
- Tested with various (x, y, θ) values, and the results were as expected.

---

## 👥 **Contributors & Acknowledgments**

This project was developed by **Group-8** at **DAIICT** for the course **IE-410 (Introduction to Robotics)**.

- **Het Gandhi** - 202201167  
- **Meet Joshi** - 202201065  
- **Harsh Bosamiya** - 202201243  
- **Dishant Patel** - 202201260  

---

## 📜 **License**

This project is open-source and can be used for educational purposes. Feel free to modify and enhance it!

