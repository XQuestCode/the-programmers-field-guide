---
title: LED Blink on Raspberry Pi
---

Here’s a guide for creating an LED blink program using Raspberry Pi and C/C++ with SplashKit, similar to the format you requested:

---

## Blinking LED with SplashKit

In this guide, you'll create a simple program to blink an LED using your Raspberry Pi. You'll write C++ code and compile it using SplashKit. Let's get started by setting up the project and writing the code.

![Raspberry Pi LED blinking](https://i.imgur.com/vH5k9Qb.gif)

### Setting Up

Before we dive into the code, ensure that SplashKit is installed and set up correctly. We’ll start by creating a folder for our project.

## Creating the Project

Let’s create a new folder where we can store our LED blink program.

```bash
cd ~/Documents/Code
mkdir LEDBlink
cd LEDBlink
touch BlinkLED.cpp
code .
```

This will create an empty `BlinkLED.cpp` file inside your `LEDBlink` folder and open the folder in VS Code for you to start coding.

---

### Writing the Code

Now, let’s write the code to blink an LED. We will use the Raspberry Pi's GPIO pins to control the LED, and SplashKit to interact with the GPIO.

```cpp
#include "splashkit.h"

int main()
{
    // Initialize Raspberry Pi
    raspi_init();
    
    // Define the LED pin
    pins led_pin = PIN_11; // Pin 11 will control the LED
    
    // Set the pin mode to output (to control the LED)
    raspi_set_mode(led_pin, GPIO_OUTPUT);
    
    // Open a dummy window for event processing (required by SplashKit)
    open_window("LED Blinker", 1, 1);
    
    // Main loop to blink LED
    while(!any_key_pressed()) // Keep running until a key is pressed
    {
        process_events(); // Process system events
        
        raspi_write(led_pin, GPIO_HIGH); // Turn LED on
        delay(500);                      // Wait for 500 milliseconds
        
        raspi_write(led_pin, GPIO_LOW);  // Turn LED off
        delay(500);                      // Wait for 500 milliseconds
    }
    
    // Clean up resources when done
    close_all_windows();
    raspi_cleanup();
    
    return 0;
}
```

### Understanding the Code

1. **Initialize Raspberry Pi:**
   The function `raspi_init()` initializes the Raspberry Pi to begin using the GPIO pins.
   
2. **Set GPIO Pin Mode:**
   We set the `led_pin` to **GPIO_OUTPUT** mode using `raspi_set_mode()`. This means the pin will be used to send signals (turn the LED on and off).

3. **Main Loop:**
   The program runs an infinite loop, where it continuously turns the LED on and off with delays in between (500 milliseconds or half a second). The loop ends when a key is pressed, which is detected by the `any_key_pressed()` function.

4. **GPIO Control:**
   - `raspi_write(led_pin, GPIO_HIGH)` turns the LED on.
   - `raspi_write(led_pin, GPIO_LOW)` turns the LED off.
   
5. **Process Events:**
   The `process_events()` call ensures the program keeps running smoothly by processing system events, especially since SplashKit uses an event-driven model.

6. **Cleanup:**
   The `raspi_cleanup()` function ensures that the Raspberry Pi’s GPIO pins are properly released when the program finishes.

---

### Compiling and Running the Code

After writing the code, you’ll need to compile and run it. Save the file and run the following commands to compile and execute your program:

```bash
clang++ BlinkLED.cpp -o blink -l SplashKit
./blink
```

The `clang++` command compiles the program and links it with SplashKit. The `-o blink` specifies the output file name, and `-l SplashKit` links the SplashKit library.

:::caution
- **Wiring:** Ensure that the LED is connected properly with a current-limiting resistor. Incorrect wiring can damage the GPIO pins or your Raspberry Pi.
- **Pin Modes:** Be careful when assigning GPIO pin modes. Setting the wrong mode for a pin may lead to errors or even hardware damage.
:::

Once compiled and executed, your LED should blink on and off every half a second. Press any key to stop the program and release the resources.

---

This simple project introduces basic GPIO control using C++ and SplashKit on the Raspberry Pi. Once you have this running, you can start experimenting with different delays or even add more LEDs for complex patterns!