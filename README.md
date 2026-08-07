# STM32 Servo Motor Control via UART

In this project, I controlled an SG90 servo motor using an STM32 (Nucleo-F303RE) board via UART commands sent from a PC.

## Hardware
* Board: STM32 Nucleo-F303RE
* Servo: SG90 Micro Servo
* Connections: TIM1 Channel 3 (PWM) and USART2 (115200 Baud Rate)

## How It Works
Commands are sent to the board using a serial terminal (Termite, PuTTY, etc.):
* A90 or a90: Moves the servo to 90 degrees (accepts values from 0 to 180).
* S or s: Runs a sweep test (0 -> 180 -> 90 degrees).
* R or r: Prints the current angle of the servo.

## Code Structure
* Incoming UART data is collected byte-by-byte using an interrupt (HAL_UART_RxCpltCallback) and stored in a buffer.
* Once \n or \r is received, the command is parsed, converted to an integer with atoi, and translated into a PWM signal.
