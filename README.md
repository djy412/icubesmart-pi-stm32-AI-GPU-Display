# iCubeSmart Pi–STM32 UART Bridge

This project connects a Raspberry Pi Zero W 2 to an STM32-based 16×16×16 LED cube
from icubesmart over UART. The Pi transmits GPU utilization as ASCII commands, and the
STM32 renders dynamic LED patterns accordingly.

## Features
- Raspberry Pi UART transmission
- Interrupt-driven STM32 UART reception
- Robust line-based ASCII protocol
- Fully non-blocking LED refresh
- 3.3 V UART (no level shifting required)

## Hardware
- Raspberry Pi (tested on Pi 4 / Pi 5)
- STM32 / GD32F103-based LED cube controller
- UART @ 9600 or 115200 baud
- Common ground required

## Repository Structure
- `stm32/` – STM32 firmware (CubeMX + HAL)
- `raspberry_pi/` – GPU-to-UART Python transmitter
- `docs/` – Wiring, protocol, troubleshooting

## Quick Start
1. Flash STM32 firmware
2. Enable UART on Raspberry Pi
3. Run `gpu_to_uart.py`
4. Observe LED cube response

Detailed instructions are in the `docs/` folder.
