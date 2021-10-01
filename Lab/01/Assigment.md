# Lab 1: Unax Lasa

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/unaxlasa/Digital-electronics-2/](https://github.com/unaxlasa/Digital-electronics-2/)

### Blink example

1. What is the meaning of the following binary operators in C?
   * `|` or
   * `&` and
   * `^` exor
   * `~` compliment
   * `<<` left shift
   * `>>` right shift

2. Complete truth table with operators: `|`, `&`, `^`, `~`

| **b** | **a** |**b or a** | **b and a** | **b xor a** | **not b** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 |
| 1 | 0 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 | 0 |


### Morse code

1. Listing of C code with syntax highlighting which repeats one "dot" and one "comma" (BTW, in Morse code it is letter `A`) on a LED:

```c
#define LED_GREEN   PB5 // AVR pin where green LED is connected
#define SHORT_DELAY 500 // Delay in milliseconds
#ifndef F_CPU           // Preprocessor directive allows for conditional
                        // compilation. The #ifndef means "if not defined".
# define F_CPU 16000000 // CPU frequency in Hz required for delay
#endif                  // The #ifndef directive must be closed by #endif

#include <util/delay.h> // Functions for busy-wait delay loops
#include <avr/io.h>     // AVR device-specific IO definitions

int main(void)
{
    // Set pin as output in Data Direction Register
    // DDRB = DDRB or 0010 0000
    DDRB = DDRB | (1<<LED_GREEN);

    // Set pin LOW in Data Register (LED off)
    // PORTB = PORTB and 1101 1111
    PORTB = PORTB & ~(1<<LED_GREEN);

    // Infinite loop
    while (1)
    {
         _delay_ms(SHORT_DELAY);                // Delay of 500ms
         PORTB = PORTB ^ (1<<LED_GREEN);        // LED ON
         _delay_ms(SHORT_DELAY);                // Delay of 500ms
         PORTB = PORTB ^ (1<<LED_GREEN);        // LED OFF
         _delay_ms(SHORT_DELAY);                // Delay of 500ms
         PORTB = PORTB ^ (1<<LED_GREEN);        // LED ON  
         _delay_ms(1000);                       // Longer delay, the line
         PORTB = PORTB ^ (1<<LED_GREEN);        // LED OFF, as it was in the beggining of the loop
    }

    // Will never reach this
    return 0;
}
```


2. Scheme of Morse code application, i.e. connection of AVR device, LED, resistor, and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure](https://github.com/unaxlasa/Digital-electronics-2/blob/main/Lab/01/AssigmentDrawing.png)
