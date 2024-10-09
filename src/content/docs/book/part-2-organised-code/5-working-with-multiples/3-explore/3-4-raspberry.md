---
title: Button-Controlled LED using Pointers
sidebar:
    label: " - Raspberry Pi"
---

![](https://i.imgur.com/M23Vtk1.png)

### Task: Multi-Zone Motion Detection System

---

**Title:** Multi-Zone Alarm System with Multiple Sensors and LEDs

**Objective:**  
- Build an alarm system with multiple zones, where each zone consists of a PIR sensor and an LED.  
- Each zone monitors for motion, and if motion is detected, the LED in that zone turns on.

---

**Hardware Required:**  
- Raspberry Pi  
- 3 PIR sensors  
- 3 LEDs  
- 3 220Ω Resistors  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect each PIR sensor and LED to the appropriate GPIO pins on the Raspberry Pi.  
   - Ensure that each LED has a 220Ω resistor to prevent overloading.

2. **Program Objective**:  
   - Write a program that monitors multiple zones (each with its own sensor and LED).  
   - When motion is detected in a zone, the LED for that zone turns on.

3. **Hints**:  
   - Use arrays to store and manage multiple zones.  
   - Each zone should have its own PIR sensor and LED, controlled by the system.

4. **Important Notes**:  
   - Make sure to initialize all the zones correctly and check each one in the main loop.
   - If the library does not respond, try running `sudo pigpiod` to start the GPIO daemon.

---

**Safety Reminder**: Double-check your connections before powering on your Raspberry Pi to avoid any short circuits or damage to the components.

---
