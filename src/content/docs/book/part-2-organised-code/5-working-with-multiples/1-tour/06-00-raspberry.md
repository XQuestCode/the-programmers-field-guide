---
title: raspberry pi
banner: 
  content: Managing Multiple Components Using Arrays and Sensors

---

![](https://i.imgur.com/M23Vtk1.png)


### Guided Tour: Managing Multiple LEDs and Sensors

---

**Title:** Interactive Alarm System with Multiple Sensors and LEDs

**Objective:**  
- Learn how to manage multiple components (like LEDs, buttons, and sensors) using arrays and loops.  
- Build a multi-zone alarm system using PIR sensors and LEDs.

---

**Concepts You Will Explore:**  
- **Arrays**: Use arrays to manage multiple LEDs and sensors, allowing the system to monitor several zones simultaneously.
- **Loops**: Use loops to efficiently iterate over multiple components and perform actions (such as turning LEDs on or off) based on sensor inputs.
- **System Design**: Build an interactive multi-zone system that simulates an alarm system, where each zone is controlled by its own sensor.

---

**Why Arrays and Loops Matter**:  
In embedded systems, it’s common to work with multiple components like sensors and LEDs. Arrays allow you to store and manage multiple devices, while loops help process each device efficiently. This allows you to scale systems to monitor and control multiple zones or areas.

---

**C++ Code Example Using SplashKit: Multi-Zone Alarm System**

```cpp
#include "splashkit.h"

// Define a struct to represent a Zone (a sensor and an LED)
struct zone
{
    pins led_pin;
    pins pir_sensor_pin;
    bool triggered;
};

// Function to initialize a zone
void init_zone(zone &z, pins led_pin, pins pir_sensor_pin)
{
    z.led_pin = led_pin;
    z.pir_sensor_pin = pir_sensor_pin;
    z.triggered = false;
    raspi_set_mode(z.led_pin, GPIO_OUTPUT);
    raspi_set_mode(z.pir_sensor_pin, GPIO_INPUT);
}

// Function to check for motion in a zone and update its state
void check_motion(zone &z)
{
    if (raspi_read(z.pir_sensor_pin) == GPIO_HIGH)
    {
        z.triggered = true;
        raspi_write(z.led_pin, GPIO_HIGH);  // Turn LED on if motion is detected
    }
    else
    {
        z.triggered = false;
        raspi_write(z.led_pin, GPIO_LOW);   // Turn LED off if no motion
    }
}

int main()
{
    const int NUM_ZONES = 3;               // Define number of zones
    zone zones[NUM_ZONES];                 // Create an array to store multiple zones

    // Initialize each zone with different GPIO pins for LEDs and sensors
    init_zone(zones[0], PIN_11, PIN_12);
    init_zone(zones[1], PIN_13, PIN_14);
    init_zone(zones[2], PIN_15, PIN_16);

    open_window("Multi-Zone Alarm System", 1, 1);

    while (!any_key_pressed())
    {
        process_events();

        // Check motion for each zone
        for (int i = 0; i < NUM_ZONES; i++)
        {
            check_motion(zones[i]);
        }

        delay(100);  // Add a small delay for stability
    }

    close_all_windows();
    raspi_cleanup();
    return 0;
}
```

**Explanation of Code**:  
- **Zone Struct**: A `zone` struct is used to group together the LED and PIR sensor for each zone, along with a `triggered` state.
- **Array of Zones**: The system manages multiple zones (each with its own LED and sensor) using an array.
- **Loops**: The program iterates over each zone in a loop, checking if motion is detected and updating the LED accordingly.
- **Efficiency**: Using arrays and loops allows the system to scale easily, handling multiple zones with minimal additional code.

---

**Additional Information**:  
- **PIR Sensors**: Each zone uses a PIR sensor to detect motion, and its corresponding LED turns on if motion is detected.
- **Warning**: If the library does not respond, ensure you run `sudo pigpiod` to start the GPIO daemon.
- **Expandability**: You can add more zones by simply increasing the size of the `zones` array and adding more LEDs and PIR sensors to the circuit.

---
