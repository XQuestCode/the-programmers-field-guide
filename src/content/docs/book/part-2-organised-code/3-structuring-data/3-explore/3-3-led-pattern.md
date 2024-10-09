---
title: LED State Control with Structs and Enums
---

![](https://i.imgur.com/M23Vtk1.png)
---

**Title:** Structuring Data to Manage Multiple LEDs and Buttons

**Objective:**  
- Use structs and enums to manage multiple LEDs and buttons. Each button should toggle its corresponding LED.

---

**Hardware Required:**  
- Raspberry Pi  
- 2 LEDs  
- 2 Push buttons  
- 220Ω Resistors  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect two buttons to **Pin 12** and **Pin 13**, and two LEDs to **Pin 11** and **Pin 10** on your Raspberry Pi.
   - Make sure each LED has a 220Ω resistor to prevent damage.

2. **Program Objective**:  
   - Create structs for each button and LED, and use these structs to manage the state of each component.
   - Each button should toggle its corresponding LED.

3. **Hints**:  
   - Create an array or list of buttons and LEDs, and use loops to manage their states.
   - Use the `raspi_read()` function to read button states and `raspi_write()` to control LED output.

4. **Important Notes**:  
   - Use structs to encapsulate all relevant data for the LEDs and buttons. This will help in organizing and managing multiple components more easily.
   - If the library does not respond, try running `sudo pigpiod` to start the GPIO daemon.

---

**Safety Reminder**: Always ensure your connections are correct and resistors are properly used to prevent overloading your GPIO pins.

---
