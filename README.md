# 🤖 Inverse Kinematics in a 3-Link Robotic Arm  

This project implements **inverse kinematics** for a **3-link robotic arm** using an **Arduino-compatible setup**. The algorithm calculates joint angles based on a given **end-effector position** \((x, y, \theta)\) and precisely moves the robotic arm to the desired location.

---

## 📌 **Project Overview**  
- Implements **inverse kinematics** for a 3-link robotic arm.  
- Uses **Arduino Uno** and **Braccio Robotic Arm**.  
- Computes joint angles \((\theta_1, \theta_2, \theta_3)\) using trigonometric formulas.  
- Moves the robotic arm to the specified position based on calculated angles.  

---

## 🔧 **Hardware & Materials**  
- **Arduino Uno** with USB cable  
- **Arduino Tinkerkit Braccio Robotic Arm**  
- **Arduino-Compatible Shield**  
- **Power Adapter**  

---

## 📜 **Implementation & Working**  

### 🔢 **Mathematical Formulas Used**  
Given an **end-effector position** \((x, y)\) and orientation \(\theta\), we calculate joint angles using:  

#### 📍 **Position of Joint J3**  
\[
a = x - L3 \cdot \cos(\theta)
\]
\[
b = y - L3 \cdot \sin(\theta)
\]

#### 📏 **Link Distance Calculation**  
\[
C = \sqrt{a^2 + b^2}
\]

#### 📐 **Finding Angles using Cosine Law**  
\[
\alpha = \cos^{-1} \left( \frac{L1^2 + C^2 - L2^2}{2 \cdot L1 \cdot C} \right)
\]
\[
\beta = \cos^{-1} \left( \frac{L1^2 + L2^2 - C^2}{2 \cdot L1 \cdot L2} \right)
\]

#### 🔄 **Final Angle Computation**  
\[
\theta_1 = \tan^{-1} \left(\frac{b}{a}\right) - \alpha
\]
\[
\theta_2 = 180^\circ - \beta
\]
\[
\theta_3 = \theta - \theta_1 - \theta_2
\]

---

## 📂 **Code Implementation**  
Below is a snippet of the inverse kinematics function in **Arduino C++**:

```cpp
void inverseKinematics(float x, float y, float theta) {
    float a = x - (L3 * cos(radians(theta)));
    float b = y - (L3 * sin(radians(theta)));
    float C = sqrt(pow(a, 2) + pow(b, 2));

    float alpha = degrees(acos((pow(L1, 2) + pow(C, 2) - pow(L2, 2)) / (2 * L1 * C)));
    float Beta = degrees(acos((pow(L1, 2) + pow(L2, 2) - pow(C, 2)) / (2 * L1 * L2)));

    float theta1 = degrees(atan2(b, a)) - alpha;
    float theta2 = 180 - Beta;
    float theta3 = theta - theta1 - theta2;

    Braccio.ServoMovement(20, 0, int(theta1), 90 + int(theta2), 90 + int(theta3), 0, 73);
}
