# Raspberry Pi GPU → UART Bridge

This directory contains the Python code that runs on the Raspberry Pi and streams GPU utilization data to the LED cube over UART.

---

## Responsibilities

- Poll GPU utilization via SSH (`nvidia-smi`)
- Convert utilization to 0–99 range
- Transmit ASCII values over UART
- Run automatically at boot via systemd

---

## Requirements

- Raspberry Pi Zero 2 W (or equivalent)
- Python 3.9+
- pyserial
- Passwordless SSH access to Windows host

---

## Files

- `gpu_to_uart.py` – main telemetry script
- `systemd/gpu_to_uart.service` – autostart service

---

## UART Configuration

- Device: `/dev/ttyAMA0`
- Baud Rate: must match STM32
- Format: 8-N-1
- Output: ASCII number + newline

Example output:
25\n
0\n
73\n

---

## Running Manually

```bash
python3 gpu_to_uart.py

sudo cp systemd/gpu_to_uart.service /etc/systemd/system/
sudo systemctl daemon-reexec
sudo systemctl enable gpu_to_uart
sudo systemctl start gpu_to_uart
