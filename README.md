# Embedded "Simon Says" Game

This repository contains the source code for a "Simon Says" memory game implemented on an STM32 Nucleo-64 development board.

**Date:** May 2025

## Project Overview

This project is a hardware implementation of the classic electronic memory game, "Simon Says". The game generates a sequence of colors (Red, Green, Yellow), and the player must replicate the sequence by pressing the corresponding buttons. The game is built around a state machine with interrupt-driven button input and timed feedback logic. It features various user feedback mechanisms, including LEDs and a buzzer, and supports being powered by either USB or an external 5V battery.

## Gameplay

1.  **Start:** When the device is first powered on, it enters an `IDLE` state. Press the `START` button to begin the game.
2.  **Startup Sequence:** The game will perform a quick startup animation, blinking the Red, Green, and Yellow LEDs in order.
3.  **Memorize the Sequence:** The device will then generate and display a random sequence of colors. The game starts with a sequence length of 2, and each color lights up for half a second.
4.  **Player's Turn:** After the sequence is shown, it is the player's turn to repeat it by pressing the colored buttons in the correct order. A brief LED flash provides feedback for each button press.
5.  **Success:** If the player correctly enters the entire sequence, a green indicator LED will blink twice. The game then increases the sequence length by 1 (up to 8) and starts the next round.
6.  **Failure:** If the player makes a mistake, a buzzer will sound and the indicator LED will flash several times. The game resets the sequence length to 2 and restarts with a new sequence.

## Key Technical Features

* **Interrupt-Driven Input:** All button presses (start, red, green, yellow) are handled by hardware interrupts (EXTI), allowing the microcontroller to react instantly without needing to poll the button states continuously.
* **Progressive Difficulty:** Sequence length increases after each successful round, from 2 up to a maximum of 8.
* **User Feedback:** The game provides rich feedback through:
    * Three colored LEDs (Red, Green, Yellow) for sequence display and input confirmation.
    * A piezoelectric buzzer for failure indication.
    * A separate indicator LED for success/failure signals.
* **Dual Power Compatibility:** The hardware is designed to be powered either via the USB-B connector from a computer or by an external 5V battery connected to the board's `VIN` and `GND` pins.

## Hardware Requirements

* STM32 Nucleo-64 Development Board (STM32L073RZ)
* Breadboard
* 4x Push Buttons (3 for colors, 1 for Start)
* 3x Colored LEDs (1x Red, 1x Green, 1x Yellow)
* 1x Indicator LED (1x Yellow)
* 1x Piezoelectric Buzzer
* 4x 220Ω Resistors (for the LEDs)
* Jumper Wires
* Power Source: Micro-USB cable

## Code Structure

The entire application logic is contained within `Core/Src/main.c`.
