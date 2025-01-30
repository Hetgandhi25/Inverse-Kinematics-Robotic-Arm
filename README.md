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

## 📜 **Implementation & Working**  

1️⃣ **Understanding Inverse Kinematics (IK)**  
- IK is used to calculate the joint angles **(θ1, θ2, θ3)** from a given **end-effector position** **(x, y, θ)**.  
- The Braccio robotic arm consists of **three main links**:  
  - **L1** → Shoulder to Elbow  
  - **L2** → Elbow to Wrist  
  - **L3** → Wrist to End-Effector  

2️⃣ **Mathematical Formulas Used**  
Given an end-effector position (x, y) and orientation (θ), we calculate joint angles using:  

- **Position of Joint J3**  
  \[
  a = x - L3 \cdot \cos(θ)
  \]
  \[
  b = y - L3 \cdot \sin(θ)
  \]

- **Link Distance Calculation**  
  \[
  C = \sqrt{a^2 + b^2}
  \]

- **Finding Angles using Cosine Law**  
  \[
  α = \cos^{-1} \left( \frac{L1^2 + C^2 - L2^2}{2 \cdot L1 \cdot C} \right)
  \]
  \[
  β = \cos^{-1} \left( \frac{L1^2 + L2^2 - C^2}{2 \cdot L1 \cdot L2} \right)
  \]

- **Final Angle Computation**  
  \[
  θ1 = \tan^{-1} \left(\frac{b}{a}\right) - α
  \]
  \[
  θ2 = 180° - β
  \]
  \[
  θ3 = θ - θ1 - θ2
  \]

---

## 💻 **Code Implementation**  
The following C++ code is written for **Arduino IDE** using the **Braccio.h** and **Servo.h** libraries.

```cpp
#include <Braccio.h>
#include <Servo.h>

Servo base, shoulder, elbow, wrist_rot, wrist_ver, gripper;

// Lengths of robotic arm links (in mm)
const float L1 = 125; // Shoulder to Elbow
const float L2 = 125; // Elbow to Wrist
const float L3 = 71.5; // Wrist to End-Effector

void setup() {
    Serial.begin(9600); // Initialize Serial Monitor
    Braccio.begin(); // Initialize Braccio Arm Position
}

void loop() {
    float x = 0, y = 314, theta = 90; // Change these values to move the arm
    inverseKinematics(x, y, theta);
    delay(1000); // Wait 1 second
}

void inverseKinematics(float x, float y, float theta) {
    float a = x - (L3 * cos(radians(theta)));
    float b = y - (L3 * sin(radians(theta)));
    float C = sqrt(pow(a, 2) + pow(b, 2));

    float alpha = degrees(acos((pow(L1, 2) + pow(C, 2) - pow(L2, 2)) / (2 * L1 * C)));
    float Beta = degrees(acos((pow(L1, 2) + pow(L2, 2) - pow(C, 2)) / (2 * L1 * L2)));

    float theta1 = degrees(atan2(b, a)) - alpha;
    float theta2 = 180 - Beta;
    float theta3 = theta - theta1 - theta2;

    // Move the robotic arm
    Braccio.ServoMovement(20, 0, int(theta1), 90 + int(theta2), 90 + int(theta3), 0, 73);

    // Print calculated angles
    Serial.print("Theta 1: "); Serial.println(theta1);
    Serial.print("Theta 2: "); Serial.println(theta2);
    Serial.print("Theta 3: "); Serial.println(theta3);
}
