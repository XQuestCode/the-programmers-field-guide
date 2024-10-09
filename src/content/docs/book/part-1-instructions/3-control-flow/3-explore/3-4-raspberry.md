---
title: Button-Controlled LED Behavior Based on Press Count
sidebar:
  label: " - Raspberry Pi"
---

![](https://i.imgur.com/M23Vtk1.png)

### Task: Button-Controlled LED with Conditional Logic

---

**Title:** Button-Controlled LED Behavior Based on Press Count

**Objective:**  
- Create a program where the LED behavior changes based on how many times the button has been pressed, using conditional logic and control flow.

---

**Hardware Required:**  
- Raspberry Pi  
- 1 Push button  
- 1 LED  
- 220Ω Resistor  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect the button to **Pin 12** and the LED to **Pin 11** on your Raspberry Pi.  
   - Ensure the LED is connected through a 220Ω resistor to avoid damage.

2. **Program Objective**:  
   - Write a program that tracks the number of times the button is pressed and uses conditional logic to change the behavior of the LED.
   - Use `if-else` statements to control whether the LED blinks slowly, quickly, or stays on, based on the number of button presses.

3. **Hints**:  
   - Start by writing the code to increment the button press count and then add conditional logic using `if-else` statements to control the LED.
   - Use `delay()` to adjust the blink speed.

:::note
   - Remember to debounce the button to avoid detecting multiple presses from a single click.
   - Ensure the Raspberry Pi’s GPIO pins are correctly configured as input for the button and output for the LED.
   - **Note**: If the library doesn’t respond, use `sudo pigpiod` to start the GPIO daemon.



**Safety Reminder**: Verify your wiring before running the program to avoid short circuits or component damage.

:::

