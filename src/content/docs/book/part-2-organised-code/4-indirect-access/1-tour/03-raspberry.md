---
title: Raspberry Pi
banner: 
  content: Indirect Access with Pointers
---

![](https://i.imgur.com/M23Vtk1.png)



### Guided Tour: Indirect Access with Pointers

---

**Title:** Building a Simple Security System with LEDs, Buttons, and PIR Sensors

**Objective:**  
- Learn how to use pointers and pass-by-reference to control multiple components in a dynamic system.
- Build a small security system using buttons, LEDs, and PIR sensors that reacts to movement and button presses.

---

**Concepts You Will Explore:**  
- **Pointers and Pass-by-Reference**: Use pointers to pass data between functions, allowing you to manipulate GPIO components like LEDs and PIR sensors.
- **Conditional Logic**: Use `if-else` statements to handle inputs from multiple sensors and buttons.
- **System Interaction**: Design a small, interactive system that uses multiple inputs (PIR sensor and button) to control LEDs.

---

**C++ Code Example Using SplashKit: Simple Security System**

```cpp
#include "splashkit.h"

// Define a struct to represent a Security System
struct security_system
{
    pins led_pin;
    pins button_pin;
    pins pir_sensor_pin;
    bool system_armed;
};

// Function to initialize the security system
void init_security_system(security_system &system, pins led_pin, pins button_pin, pins pir_sensor_pin)
{
    system.led_pin = led_pin;
    system.button_pin = button_pin;
    system.pir_sensor_pin = pir_sensor_pin;
    system.system_armed = false;
    raspi_set_mode(system.led_pin, GPIO_OUTPUT);
    raspi_set_mode(system.button_pin, GPIO_INPUT);
    raspi_set_mode(system.pir_sensor_pin, GPIO_INPUT);
}

// Function to arm/disarm the security system based on button press
void check_button_press(security_system &system)
{
    if (raspi_read(system.button_pin) == GPIO_HIGH)
    {
        system.system_armed = !system.system_armed;
        raspi_write(system.led_pin, system.system_armed ? GPIO_HIGH : GPIO_LOW);  // Turn LED on if armed
        delay(300);  // Debounce delay
    }
}

// Function to detect motion using PIR sensor and trigger the LED
void detect_motion(security_system &system)
{
    if (system.system_armed && raspi_read(system.pir_sensor_pin) == GPIO_HIGH)
    {
        raspi_write(system.led_pin, GPIO_HIGH);  // Turn LED on when motion detected
        delay(1000);  // Keep the LED on for 1 second
        raspi_write(system.led_pin, GPIO_LOW);   // Turn LED off after delay
    }
}

int main()
{
    raspi_init();

    security_system system;
    init_security_system(system, PIN_11, PIN_12, PIN_13);  // Initialize with LED, Button, and PIR Sensor on pins

    open_window("Security System", 1, 1);

    while (!any_key_pressed())
    {
        process_events();
        check_button_press(system);  // Check if the system should be armed/disarmed
        detect_motion(system);       // Check if motion is detected when armed
    }

    close_all_windows();
    raspi_cleanup();
    return 0;
}
```

**Explanation of Code**:  
- **Structs**: The `security_system` struct groups together the components of the system (LED, button, PIR sensor) and a state variable (`system_armed`).
- **Pass-by-Reference**: The security system is passed by reference to functions, allowing modifications (like arming/disarming the system) to persist outside the function.
- **Motion Detection**: The `detect_motion()` function checks for motion using the PIR sensor and triggers the LED if the system is armed.

---

**Additional Information**:  
- **PIR Sensors**: PIR sensors detect infrared radiation emitted by objects, commonly used to detect motion.
- **Debouncing**: A small delay is added after reading the button to prevent registering multiple presses due to mechanical noise.
- **Warning**: If the library does not respond, ensure you run `sudo pigpiod` to start the GPIO daemon.

---

