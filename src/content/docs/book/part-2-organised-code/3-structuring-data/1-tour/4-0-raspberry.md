---
title: Structuring Code with Functions
banner: 
  content: This is an optional tour - use it to extend your understanding.
---


**Title:** Using Structs to Represent LED and Button States

**Objective:**  
- Learn to organize data using structs to represent the state of multiple components like LEDs and buttons.

---

**Concepts You Will Explore:**  
- **Structs**: Structs allow you to group related data together, making your code easier to manage and extend.  
- **Enums**: Using enums to represent different types or states, such as the status of a button (PRESSED or NOT_PRESSED).  
- **Data Organization**: Organizing component information into a single, easy-to-manage structure.

---

**Why Structs Matter**:  
In embedded systems, you often work with multiple inputs and outputs, such as buttons and LEDs. Grouping their states and behaviors into a structured data format helps you manage them effectively. Structs allow you to create a blueprint for each device (e.g., an LED or button) and store all related data (like state and pin number) in one place.

---

**C++ Code Example Using SplashKit: Structs for LEDs and Buttons**

```cpp
#include "splashkit.h"

// Define an enum to represent button states
enum button_state
{
    NOT_PRESSED,
    PRESSED
};

// Define a struct to represent an LED
struct led
{
    pins pin;
    bool state;
};

// Define a struct to represent a Button
struct button
{
    pins pin;
    button_state state;
};

// Function to initialize an LED
led init_led(pins pin)
{
    led result;
    result.pin = pin;
    result.state = false;
    raspi_set_mode(result.pin, GPIO_OUTPUT);
    return result;
}

// Function to initialize a Button
button init_button(pins pin)
{
    button result;
    result.pin = pin;
    result.state = NOT_PRESSED;
    raspi_set_mode(result.pin, GPIO_INPUT);
    return result;
}

// Function to read the state of the button and update struct
void update_button(button &btn)
{
    if (raspi_read(btn.pin) == GPIO_HIGH)
    {
        btn.state = PRESSED;
    }
    else
    {
        btn.state = NOT_PRESSED;
    }
}

// Function to toggle LED based on button state
void toggle_led(led &light, button &btn)
{
    if (btn.state == PRESSED)
    {
        light.state = !light.state;
        raspi_write(light.pin, light.state ? GPIO_HIGH : GPIO_LOW);
    }
}

int main()
{
    raspi_init();
    
    led led1 = init_led(PIN_11);        // Initialize LED on PIN 11
    button button1 = init_button(PIN_12); // Initialize Button on PIN 12
    
    open_window("Structuring Data Example", 1, 1);
    
    while (!any_key_pressed())
    {
        process_events();
        
        update_button(button1);   // Check button state
        toggle_led(led1, button1); // Toggle LED based on button press
        
        delay(300);               // Debounce delay
    }
    
    close_all_windows();
    raspi_cleanup();
    return 0;
}
```

**Explanation of Code**:  
- **Structs**: The `led` struct stores the pin number and current state of the LED, while the `button` struct stores the pin number and its state (PRESSED or NOT_PRESSED).
- **Enums**: An enum is used to represent button states, making the code more readable and less error-prone.
- **update_button()**: This function checks the button's pin and updates its state in the struct.
- **toggle_led()**: This function toggles the LED state based on the button’s state.

---

**Additional Information**:  
- **Why Use Structs**: Grouping related data (such as the pin number and state) into a struct simplifies managing multiple components and allows for easier scaling in the future.
- **Warning**: If the library does not respond, ensure you run `sudo pigpiod` to start the GPIO daemon.

---
