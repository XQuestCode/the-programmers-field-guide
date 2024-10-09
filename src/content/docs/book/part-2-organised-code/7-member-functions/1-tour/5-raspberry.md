---
title: Raspberry Pi
---

### Guided Tour: Member Functions for Multiple LEDs and Buttons

---

**Title:** Managing LEDs and Buttons Using Object-Oriented Programming

**Objective:**  
- Learn how to use member functions in a class to manage the state and behavior of multiple buttons and LEDs dynamically.
- Understand how object-oriented programming can help in organizing your code for embedded systems.

---

**Concepts You Will Explore:**  
- **Classes and Objects**: Use classes to represent LEDs and buttons, and manage their states and interactions.
- **Member Functions**: Functions inside a class that operate on the data stored in that class, allowing you to manage multiple components in a structured way.
- **Dynamic Arrays**: Use dynamic arrays to manage an unlimited number of LEDs and buttons, allowing the system to scale as needed.

---

**Why Use Classes and Member Functions?**  
Using classes and member functions makes it easier to organize your code and manage multiple components. For instance, in a large embedded system, you might have several LEDs and buttons, each with its own behavior. Member functions let you encapsulate this behavior in reusable objects, simplifying your code.

---

**C++ Code Example Using SplashKit: Object-Oriented LED and Button Control**

```cpp
#include "splashkit.h"

// Define a class for the LED
class LED
{
private:
    pins pin;    // Pin for the LED
    bool state;  // State of the LED (on or off)

public:
    // Constructor to initialize the LED
    LED(pins led_pin)
    {
        pin = led_pin;
        state = false;
        raspi_set_mode(pin, GPIO_OUTPUT);  // Set the pin as output
    }

    // Function to toggle the LED
    void toggle()
    {
        state = !state;
        raspi_write(pin, state ? GPIO_HIGH : GPIO_LOW);  // Set LED state
    }

    // Function to turn off the LED
    void turn_off()
    {
        state = false;
        raspi_write(pin, GPIO_LOW);  // Turn off the LED
    }

    // Function to get the LED state
    bool is_on() const
    {
        return state;
    }
};

// Define a class for the Button
class Button
{
private:
    pins pin;  // Pin for the button

public:
    // Constructor to initialize the button
    Button(pins button_pin)
    {
        pin = button_pin;
        raspi_set_mode(pin, GPIO_INPUT);  // Set the pin as input
    }

    // Function to check if the button is pressed
    bool is_pressed() const
    {
        return raspi_read(pin) == GPIO_HIGH;
    }
};

int main()
{
    raspi_init();

    // Create dynamic arrays of buttons and LEDs
    const int num_components = 3;
    LED* leds = new LED[num_components]{LED(PIN_11), LED(PIN_13), LED(PIN_15)};
    Button* buttons = new Button[num_components]{Button(PIN_12), Button(PIN_14), Button(PIN_16)};

    open_window("Member Functions Example", 1, 1);

    while (!any_key_pressed())
    {
        process_events();

        // Check button states and toggle the corresponding LED
        for (int i = 0; i < num_components; i++)
        {
            if (buttons[i].is_pressed())
            {
                leds[i].toggle();  // Toggle the LED if the button is pressed
                delay(300);        // Debounce delay
            }
        }
    }

    // Free the dynamically allocated memory
    delete[] leds;
    delete[] buttons;

    close_all_windows();
    raspi_cleanup();

    return 0;
}
```

**Explanation of Code**:  
- **LED and Button Classes**: The `LED` and `Button` classes encapsulate the behavior of the LEDs and buttons. Each LED can toggle its state using the `toggle()` member function, and each button can check if it’s pressed using the `is_pressed()` member function.
- **Dynamic Arrays**: The program creates dynamic arrays of `LED` and `Button` objects, allowing for as many LEDs and buttons as needed. This mirrors the idea of an expandable system, like a POS system or music app that can handle an unlimited number of products or songs.
- **Member Functions**: The use of member functions keeps the logic for each component contained within its class, making the code cleaner and more organized.

---

**Additional Information**:  
- **Object-Oriented Design**: Encapsulating components like LEDs and buttons in classes makes the program easier to extend and maintain.
- **Memory Management**: After dynamically allocating the LED and button objects, they are properly deallocated at the end to avoid memory leaks.
- **Warning**: If the library does not respond, ensure you run `sudo pigpiod` to start the GPIO daemon.

---

