# Lab 4: UNAX LASA

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/unaxlasa/Digital-electronics-2](https://github.com/unaxlasa/Digital-electronics-2)


### Overflow times

1. Complete table with overflow times.

| **Module** | **Number of bits** | **1** | **8** | **32** | **64** | **128** | **256** | **1024** |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Timer/Counter0 | 8  | 16us | 128us | -- | 1min| -- | 4ms |16ms |
| Timer/Counter1 | 16 |   4 ms  |  33ms    | -- | 262ms| -- |1sec |42sec |
| Timer/Counter2 | 8  |  16us   |   128us   |   512us | 1ms |  2ms  | 4ms | 16ms|


### Timer library

1. In your words, describe the difference between common C function and interrupt service routine.
   * Functions need to be called when we need them in the program. They have no priority, so information might be lost, because of the timing of the program.
   * However, interrupt service routines have the priority to interrupt the code and execute the routine. 

2. Part of the header file listing with syntax highlighting, which defines settings for Timer/Counter0:

```c
/**
 * @name  Definitions of Timer/Counter0
 * @note  F_CPU = 16 MHz
 */
/** @brief Stop timer, prescaler 000 --> STOP */
#define TIM0_stop()           TCCR1B &= ~((1<<CS02) | (1<<CS01) | (1<<CS00));

/** @brief Set overflow 16ms, prescaler 001 --> 1 */
#define TIM0_overflow_16us()   TCCR1B &= ~((1<<CS02) | (1<<CS01)); TCCR1B |= (1<<CS00);
/** @brief Set overflow 33ms, prescaler 010 --> 8 */
#define TIM0_overflow_128us()  TCCR1B &= ~((1<<CS02) | (1<<CS00)); TCCR1B |= (1<<CS01);
/** @brief Set overflow 262ms, prescaler 011 --> 64 */
#define TIM0_overflow_1ms() TCCR1B &= ~(1<<CS02); TCCR1B |= (1<<CS01) | (1<<CS00);
/** @brief Set overflow 1s, prescaler 100 --> 256 */
#define TIM0_overflow_4ms()    TCCR1B &= ~((1<<CS01) | (1<<CS00)); TCCR1B |= (1<<CS02);
/** @brief Set overflow 4s, prescaler // 101 --> 1024 */
#define TIM0_overflow_16ms()    TCCR1B &= ~(1<<CS01); TCCR1B |= (1<<CS02) | (1<<CS00);
/** @brief Enable overflow interrupt, 1 --> enable */
#define TIM0_overflow_interrupt_enable()  TIMSK0 |= (1<<TOIE0);
/** @brief Disable overflow interrupt, 0 --> disable */
#define TIM0_overflow_interrupt_disable() TIMSK0 &= ~(1<<TOIE0);
```

3. Flowchart figure for function `main()` and interrupt service routine `ISR(TIMER1_OVF_vect)` of application that ensures the flashing of one LED in the timer interruption. When the button is pressed, the blinking is faster, when the button is released, it is slower. Use only a timer overflow and not a delay library.

   ![your figure](https://github.com/unaxlasa/Digital-electronics-2/blob/main/Lab/04-Interrupts/Lab4.png)


### Knight Rider

1. Scheme of Knight Rider application with four LEDs and a push button, connected according to Multi-function shield. Connect AVR device, LEDs, resistors, push button, and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure](https://github.com/unaxlasa/Digital-electronics-2/blob/main/Lab/04-Interrupts/Assignment4Drawing.jpg)
