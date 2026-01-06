# iCubeSmart Pi–STM32 UART Bridge

This project connects a Raspberry Pi Zero W 2 to an STM32-based 16×16×16 LED cube
from icubesmart over UART. The Pi transmits GPU utilization as ASCII commands, and the
STM32 renders dynamic LED patterns accordingly.

---

Windows Local LLM Server (GPU)
│
│ SSH (nvidia-smi)
▼
Raspberry Pi Zero 2 W
│
│ UART (ASCII 0–99\n)
▼
STM32 / GD32F103
│
▼
16×16×16 LED Cube

---

## Features

- Real-time GPU utilization visualization
- Robust interrupt-driven UART protocol
- Works with 3.3 V logic (no level shifters required)
- Drop-in STM32 firmware
- Headless Raspberry Pi operation (systemd service)
- Simple ASCII protocol (`"0\n"` – `"99\n"`)

---

## Repository Structure

├── stm32/ # STM32 firmware (CubeMX + HAL)
├── raspberry_pi/ # Raspberry Pi UART + SSH polling code
├── docs/ # Wiring, protocol, setup documentation
└── tools/ # Optional utilities and helpers

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
1. Flash STM32 firmware (`stm32/`)
2. Wire Pi UART to cube controller
3. Install Pi Python dependencies
4. Enable systemd service
5. Observe GPU activity in 3D

Detailed instructions are in the `docs/` folder
