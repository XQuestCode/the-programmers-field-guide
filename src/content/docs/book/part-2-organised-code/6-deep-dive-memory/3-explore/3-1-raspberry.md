---
title: Deep Dive Memory
sidebar:
  label: " - Raspberry Pi"
---

![](https://i.imgur.com/M23Vtk1.png)

### Task: Dynamic Array Button Press Logger

---

**Title:** Managing Dynamic Arrays for Button Press History

**Objective:**  
- Create a program that dynamically logs and manages button press states using a dynamically resizing array.  
- The program should resize the array when needed and handle up to 20 button presses efficiently.

---

**Hardware Required:**  
- Raspberry Pi  
- 1 Button  
- Breadboard and jumper wires

---

**Instructions:**

1. **Connect the Hardware**:  
   - Connect the button to **Pin 12** on your Raspberry Pi.

2. **Program Objective**:  
   - Write a program that logs button presses dynamically into an array.  
   - When the array is full, the program should double the size of the array to accommodate more presses.

3. **Hints**:  
   - Use dynamic memory allocation (`new`) and resize the array using `resize_array()` when it becomes full.
   - Use the `raspi_read()` function to check the button state and store it in the dynamic array.

4. **Important Notes**:  
   - Remember to deallocate memory (`delete[]`) after the program finishes using the array to prevent memory leaks.  
   - If the library does not respond, try running `sudo pigpiod` to start the GPIO daemon.

---

**Safety Reminder**: Always verify your wiring connections before running the program to avoid damaging your Raspberry Pi or components.

---

**Linked Lists** (Optional Advanced Section)

---

If you want to take it further, you can replace the dynamic array with a **linked list** to store the button press history. This will allow you to add and remove button presses without resizing arrays, giving you more flexibility in managing memory. You can create a struct for each node in the list, and link them dynamically as new button presses occur.