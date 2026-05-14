# L476-USART4-Multiplication
# STM32 UART Multiplication Learning Game

A simple UART-based multiplication quiz game using STM32L476 and PuTTY terminal.

Users answer multiplication questions through UART serial communication.

---

# Features

- UART TX/RX communication
- Random multiplication questions
- Integer input from terminal
- Answer validation
- Feedback message
- Echo typed characters
- Works with PuTTY / TeraTerm

---

# Hardware

- STM32L476 Nucleo Board
- USB cable
- PC terminal software

---

# Software

- STM32CubeIDE
- STM32 HAL Driver
- PuTTY or TeraTerm

---

# UART Configuration

USART2:

| Setting    | Value |
|------------|-------|
| Baud Rate  | 115200 |
| Data Bits  | 8 |
| Stop Bits  | 1 |
| Parity     | None |

---

Main Functionalities
Read Integer From UART
int ReadInt()
{
    int i, N;
    char Rx[2];

    N = 0;

    while(1)
    {
        HAL_UART_Receive(&huart2, (uint8_t*)Rx, 1, HAL_MAX_DELAY);

        HAL_UART_Transmit(&huart2, (uint8_t*)Rx, 1, HAL_MAX_DELAY);

        if(Rx[0] == '\r')
            break;

        if(Rx[0] >= '0' && Rx[0] <= '9')
        {
            i = Rx[0] - '0';
            N = 10 * N + i;
        }
    }

    return N;
}

Example Output
***** Learning Multiplication ****

23 * 7 = ?161

Well Done

Wrong answer example:

45 * 6 = ?100

Wrong!... Correct answer = 270

How To Run
Open STM32CubeIDE
Build project
Flash board
Open PuTTY
Configure serial port:
COM Port = Your STM32 COM Port
Speed = 115200
Press Reset button on STM32 board
Start answering questions

# Future Improvements
Addition support
Subtraction support
Score system
Timer countdown
OLED display support
FreeRTOS task version
UART interrupt version
DMA UART version
