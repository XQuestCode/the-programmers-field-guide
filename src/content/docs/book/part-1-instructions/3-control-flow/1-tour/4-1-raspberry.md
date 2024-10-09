---
title: Control Flow and Decision Making
sidebar:
  label: " - Raspberry Pi"
---

![](https://i.imgur.com/M23Vtk1.png)

**Title:** LED Control with Button Count and Conditional Logic

**Objective:**  
- Learn how to use control flow (`if-else` statements and loops) to make decisions based on user input.  
- Implement a button press counter that changes the behavior of an LED, demonstrating conditional logic.

---

**Concepts You Will Explore:**  
- **Control Flow**: Using `if-else` conditions to make decisions based on button presses.
- **Looping**: Implement a loop that continues until a condition is met.
- **LED Behavior**: Use control flow to control how the LED behaves based on the number of button presses.

---

**Understanding Control Flow**:  
In this example, we will create a simple program that tracks how many times a button is pressed. Based on the count, the program will use `if-else` conditions to change the behavior of an LED. For instance:
- If the button has been pressed fewer than 3 times, the LED will blink slowly.
- If the button has been pressed between 3 and 5 times, the LED will blink faster.
- If the button has been pressed more than 5 times, the LED will stay on permanently.

---

**C++ Code Example Using SplashKit**:

```cpp
#include "splashkit.h"

int main()
{
    // Initialize GPIO
    raspi_init();
    pins button_pin = PIN_12;
    pins led_pin = PIN_11;

    // Set pin modes
    raspi_set_mode(button_pin, GPIO_INPUT);
    raspi_set_mode(led_pin, GPIO_OUTPUT);

    int press_count = 0;  // Track button presses

    open_window("Control Flow Example", 1, 1);

    while (!any_key_pressed())
    {
        process_events();

        // Check if the button is pressed
        if (raspi_read(button_pin) == GPIO_HIGH)
        {
            press_count++;  // Increment button press count

            // Conditional logic for LED behavior
            if (press_count < 3)
            {
                raspi_write(led_pin, GPIO_HIGH);  // Slow blink
                delay(1000);
                raspi_write(led_pin, GPIO_LOW);
                delay(1000);
            }
            else if (press_count >= 3 && press_count <= 5)
            {
                raspi_write(led_pin, GPIO_HIGH);  // Fast blink
                delay(300);
                raspi_write(led_pin, GPIO_LOW);
                delay(300);
            }
            else
            {
                raspi_write(led_pin, GPIO_HIGH);  // LED stays ON
            }

            // Debouncing delay
            delay(300);
        }
    }

    close_all_windows();
    raspi_cleanup();
    return 0;
}
```

---

**Explanation of Code**:  
- **Control Flow with `if-else`**: The program uses `if-else` to change how the LED behaves based on how many times the button is pressed.
  - **press_count < 3**: The LED blinks slowly.
  - **press_count between 3 and 5**: The LED blinks faster.
  - **press_count > 5**: The LED stays on permanently.
- **Debouncing**: A small delay after a button press ensures the program doesn’t count multiple presses from a single click.

---

**Additional Information**:  
- Control flow and conditional logic are essential when designing embedded systems where components need to react based on different input conditions.
- **Note**: If the GPIO library doesn’t respond, try running `sudo pigpiod` to start the GPIO daemon.

---
