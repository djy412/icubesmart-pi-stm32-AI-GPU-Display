# STM32 Firmware (LED Cube Controller)

This directory contains the STM32/GD32 firmware that drives the 16×16×16 LED cube and receives UART commands from the Raspberry Pi.

---

## Target Hardware

- MCU: GD32F103 / STM32F103 class
- Voltage: 3.3 V
- UART: USART1
- Baud Rate: 9600 or 115200 (must match Pi)
- Data Format: 8-N-1

---

## UART Protocol

- ASCII decimal number: `0`–`99`
- Terminated by `\n` or `\r\n`

Examples:
0\n → clear display
25\n → flash 25 LEDs
99\n → flash 99 LEDs


Reception is **interrupt-driven** to ensure reliability even during heavy LED refresh.

---

## Display Behavior

- `0` → display cleared and held off
- `1–99` → that many LEDs randomly flash in the cube
- Any change in value forces a full display reset

---

## Key Files

- `main.c` – application logic and UART handling
- `main.h` – definitions and prototypes
- CubeMX `.ioc` (if present) – hardware configuration

---

## Build Instructions

1. Open project in STM32CubeIDE
2. Verify clock and USART1 settings
3. Build and flash
4. Confirm UART debug output via USB-TTL

---

## Notes

- UART RX is **interrupt-based**
- GPIO timing is critical for LED stability
- Common ground between Pi and STM32 is mandatory
