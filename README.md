# Inverse Kinematics in a 3-Link Robotic Arm  

This project implements inverse kinematics for a 3-link robotic arm using an Arduino-compatible setup. It calculates joint angles based on the given end-effector coordinates (x, y) and orientation (θ), enabling precise control of the robotic arm’s movements.  

## 📌 **Project Overview**  
- Uses **Arduino Uno** and **Braccio Robotic Arm**.  
- Computes joint angles using inverse kinematics formulas.  
- Moves the arm to a specified position based on calculated angles.  

## 🔧 **Hardware & Materials**  
- Arduino Uno with USB cable  
- Arduino Tinkerkit Braccio Robotic Arm  
- Arduino Compatible Shield  
- Power Adapter  

## 📜 **Implementation**  
- Computes joint angles (θ1, θ2, θ3) using trigonometric methods.  
- Uses **Braccio.h** and **Servo.h** libraries for motor control.  
- Executes movements via `Braccio.ServoMovement()`.  

## 🎥 **Demo**  
🔗 [YouTube Video](https://youtu.be/gsnxKZ3Plk0?si=-Y-jB_4tQrPGEVx4)  

## 📂 **Code Example**  
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
