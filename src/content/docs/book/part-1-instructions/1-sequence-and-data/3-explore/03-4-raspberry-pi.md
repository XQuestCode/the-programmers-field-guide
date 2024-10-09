---
title: Control LED Blink Speed with Button Presses
---

### Task: Control LED Blink Speed with Button Presses

![](https://i.imgur.com/M23Vtk1.png)

**Title:** Button-Controlled LED Blink Speed

**Objective:**  
- Create a program that counts how many times a button is pressed and uses that count to adjust the blink speed of an LED.

---

**Hardware Required:**  
- Raspberry Pi  
- Push button  
- 1 LED  
- 220Ω Resistor  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect the button to **Pin 12** and the LED to **Pin 11** of your Raspberry Pi.  
   - Use a 220Ω resistor in series with the LED to prevent damage.

2. **Program Objective**:  
   - Create a program that increases the blink speed of the LED as the button is pressed more times.

3. **Hints**:  
   - Use an integer variable to count the button presses and a delay function to control the LED's blink speed.
   - Remember to debounce the button by adding a small delay after each press to avoid registering multiple presses.

:::note
   - Ensure your Raspberry Pi is properly connected and the `raspi_set_mode()` is correctly configured for input (button) and output (LED).
   - If the library does not respond, try running `sudo pigpiod` to start the GPIO daemon.


**Safety Reminder**: Always double-check your connections before powering your Raspberry Pi to avoid damaging components or shorting circuits.
:::



---
