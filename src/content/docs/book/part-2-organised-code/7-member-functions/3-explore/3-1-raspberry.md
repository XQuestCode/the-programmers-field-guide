---
title: Raspberry Pi
---

![](https://i.imgur.com/M23Vtk1.png)

### Task: Dynamically Managing Multiple LEDs and Buttons

---

**Title:** Unlimited LED and Button Management Using Member Functions

**Objective:**  
- Write a program that allows the user to manage an unlimited number of buttons and LEDs. Each button should toggle the corresponding LED.

---

**Hardware Required:**  
- Raspberry Pi  
- 3 LEDs  
- 3 Buttons  
- 220Ω Resistors  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect three buttons to **Pins 12, 14, and 16**, and three LEDs to **Pins 11, 13, and 15** on your Raspberry Pi.
   - Ensure each LED has a 220Ω resistor to avoid overloading.

2. **Program Objective**:  
   - Use classes to represent each LED and button, and use member functions to manage their states.  
   - Create dynamic arrays to store an unlimited number of LEDs and buttons.

3. **Hints**:  
   - Use object-oriented programming principles to encapsulate the behavior of the LEDs and buttons in classes.
   - Use dynamic arrays (`new[]` and `delete[]`) to handle as many buttons and LEDs as you like.

4. **Important Notes**:  
   - Ensure proper memory management by freeing dynamically allocated memory at the end of the program.
   - If the library does not respond, try running `sudo pigpiod` to start the GPIO daemon.

---

**Safety Reminder**: Always verify wiring connections before running the program to avoid damaging your Raspberry Pi or components.

---
