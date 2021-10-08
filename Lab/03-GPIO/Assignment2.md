# Lab 3: UNAX LASA

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/unaxlasa/Digital-electronics-2](https://github.com/unaxlasa/Digital-electronics-2)

### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 | -128, ..., 127 | 8-bit integrer |
| `uint16_t` | 16 | 0,1, ..., 65535 | Unsigned 16-bit integrer |
| `int16_t`  | 16 | −32 768, ..., +32 767 | 16-bit integrer |
| `float`    | 32 | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     | 0 | No range | - |


### GPIO library

1. In your words, describe the difference between the declaration and the definition of the function in C.
   * Function declaration
   * Function definition

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
/* Defines -----------------------------------------------------------*/
#define LED_GREEN   PB5     // AVR pin where green LED is connected
#define LED_BLUE PB6	    // AVR pin where blue LED is connected
#define BUTTON PB7	    // AVR pin where the button is connected
#define BLINK_DELAY 500
#ifndef F_CPU
# define F_CPU 16000000     // CPU frequency in Hz required for delay, 16MHz
#endif

/* Includes ----------------------------------------------------------*/
#include <util/delay.h>     // Functions for busy-wait delay loops
#include <avr/io.h>         // AVR device-specific IO definitions
#include "gpio.h"           // GPIO library for AVR-GCC

/* Function definitions ----------------------------------------------*/
/**********************************************************************
 * Function: Main function where the program execution begins
 * Purpose:  Toggle two LEDs when a push button is pressed. Functions 
 *           from user-defined GPIO library is used.
 * Returns:  none
 **********************************************************************/
//Function declaration
void GPIO_config_output(volatile uint8_t *reg_name, uint8_t pin_num);
void GPIO_config_input_pullup(volatile uint8_t *reg_name, uint8_t pin_num);
void GPIO_write_low(volatile uint8_t *reg_name, uint8_t pin_num);
void GPIO_write_high(volatile uint8_t *reg_name, uint8_t pin_num);
void GPIO_toggle(volatile uint8_t *reg_name, uint8_t pin_num);
uint8_t GPIO_read(volatile uint8_t *reg_name, uint8_t pin_num);

int main(void)
{
    // Green LED at port B
    	GPIO_config_output(&DDRB, LED_GREEN);
    	GPIO_write_low(&PORTB, LED_GREEN);

    // Configure the second LED at port C
	GPIO_config_output(&DDRC, LED_BLUE);
	GPIO_write_high(&PORTC, LED_BLUE);
    // Configure Push button at port D and enable internal pull-up resistor
	GPIO_config_input_pullup(&DDRD, BUTTON);

    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        _delay_ms(BLINK_DELAY);
		while(GPIO_read(&PORTD,BUTTON)) //WHile the button is pushed, the LEDs will change their condition
		{
			GPIO_toggle(&PORTB, LED_GREEN); //Change the LEDs situation
			GPIO_toggle(&PORTB, LED_BLUE);	//Change the LEDs situation
			_delay_ms(BLINK_DELAY);		//Short delay
		}
    }

    // Will never reach this
    return 0;
}

```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure](https://github.com/unaxlasa/Digital-electronics-2/blob/main/Lab/03-GPIO/Assignment2Drawing.jpg)
