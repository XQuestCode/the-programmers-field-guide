---
title: Raspberry 
sidebar:
    label: " Reaction-Based LED Control with Indirect Access"
---

![](https://i.imgur.com/M23Vtk1.png)


### Task: Interactive Security System with LEDs and PIR Sensors

---

**Title:** Build a Security System with Motion Detection and Control via Button

**Objective:**  
- Build a small security system that uses buttons to arm and disarm it, and a PIR sensor to detect motion and control the LED.

---

**Hardware Required:**  
- Raspberry Pi  
- 1 LED  
- 1 Button  
- 1 PIR sensor  
- 220Ω Resistor  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect the LED to **Pin 11**, the button to **Pin 12**, and the PIR sensor to **Pin 13** on your Raspberry Pi.
   - Use a 220Ω resistor in series with the LED to prevent damage.

2. **Program Objective**:  
   - Build a security system where a button toggles the system’s armed state (on/off).
   - When armed, the LED should blink if the PIR sensor detects motion.

3. **Hints**:  
   - Use a struct to organize the components of the system (LED, button, PIR sensor).
   - Use pointers (pass-by-reference) to modify the system’s state in different functions.

4. **Important Notes**:  
   - Test how the system responds to motion when the system is armed vs. disarmed.
   - If the library does not respond, try running `sudo pigpiod` to start the GPIO daemon.

---

**Safety Reminder**: Always verify connections before running the program to avoid damaging your components or shorting circuits.

---