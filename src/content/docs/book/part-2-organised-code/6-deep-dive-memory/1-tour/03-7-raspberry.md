---
title: Deep Dive
sidebar:
  label: " - Raspberry Pi"
---

![](https://i.imgur.com/M23Vtk1.png)


---

### Guided Tour: Dynamic Memory with Arrays and Linked Lists

---

**Title:** Managing Dynamic Arrays for LED States

**Objective:**  
- Understand how dynamic memory works by creating and resizing arrays dynamically.  
- Explore linked lists to manage multiple components (buttons, LEDs) and their states efficiently.

---

**Concepts You Will Explore:**  
- **Dynamic Arrays**: Learn how to dynamically allocate and resize arrays as more data is added (in this case, button presses and LED states).  
- **Linked Lists**: Understand how linked lists allow you to add and remove elements without reallocating memory for the entire structure.  
- **Memory Management**: Learn how to properly allocate and free memory in embedded systems.

---

**C++ Code Example Using SplashKit: Dynamic Array for LED States**

```cpp
#include "splashkit.h"

// Function to dynamically allocate a larger array when needed
int* resize_array(int* arr, int &current_size, int new_size)
{
    int* new_arr = new int[new_size];  // Allocate a new array of the new size
    for (int i = 0; i < current_size; i++)
    {
        new_arr[i] = arr[i];  // Copy over the elements from the old array
    }
    delete[] arr;  // Free the old array
    current_size = new_size;  // Update the current size
    return new_arr;
}

// Function to log button presses into a dynamic array
void log_button_press(int* &history, int &count, int &current_size)
{
    if (count == current_size)
    {
        history = resize_array(history, current_size, current_size * 2);  // Double the size of the array when full
    }
    history[count++] = raspi_read(PIN_12);  // Log the button press
}

// Function to display the history of button presses
void display_history(int* history, int count)
{
    for (int i = 0; i < count; i++)
    {
        write_line("Button press at index " + to_string(i) + ": " + (history[i] == GPIO_HIGH ? "PRESSED" : "NOT PRESSED"));
    }
}

int main()
{
    int initial_size = 5;  // Initial size of the dynamic array
    int current_size = initial_size;  // Keep track of the current array size
    int* button_press_history = new int[current_size];  // Allocate the initial array
    int press_count = 0;

    raspi_init();
    raspi_set_mode(PIN_12, GPIO_INPUT);  // Set button pin as input

    open_window("Dynamic Memory Example", 1, 1);

    while (press_count < 20)  // Log a maximum of 20 button presses
    {
        process_events();
        
        if (raspi_read(PIN_12) == GPIO_HIGH)
        {
            log_button_press(button_press_history, press_count, current_size);  // Log the button press
            delay(300);  // Debounce delay
        }
    }

    display_history(button_press_history, press_count);  // Display the history of button presses
    delete[] button_press_history;  // Free the allocated memory

    close_all_windows();
    raspi_cleanup();

    return 0;
}
```

**Explanation of Code**:  
- **Dynamic Arrays**: The `resize_array()` function reallocates memory for the array when the current array is full. This ensures that the program can handle more data without allocating excessive memory initially.
- **Doubling Size**: When the array reaches capacity, its size is doubled to accommodate more button presses. This simulates real-world scenarios where you need to grow dynamic structures like arrays.
- **Memory Management**: After the button presses are logged and displayed, the array is deallocated to prevent memory leaks.

---

