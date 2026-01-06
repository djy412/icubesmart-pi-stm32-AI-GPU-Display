# Hardware Wiring Guide

This document describes the electrical connections between the Raspberry Pi and the STM32/GD32 LED cube controller.

---

## Required Connections

| Raspberry Pi | STM32 / GD32 | Description |
|-------------|--------------|-------------|
| UART TX     | UART RX      | Data from Pi to cube |
| GND         | GND          | Common ground |

⚠ **Ground must be shared** or communication will fail.

---

## Raspberry Pi UART Pins

For Raspberry Pi Zero 2 W (40-pin header):

| Function | GPIO | Pin |
|--------|------|-----|
| UART TX | GPIO14 | Pin 8 |
| UART RX | GPIO15 | Pin 10 |
| GND | — | Pin 6 (or any GND) |

> Only **TX** is required for this project.

---

## STM32 / GD32 UART Pins

| Signal | Typical Pin |
|------|-------------|
| USART1_RX | PA10 |
| GND | Any ground |

Refer to your board schematic to confirm pin mapping.

---

## Voltage Levels

- Raspberry Pi UART: **3.3 V**
- STM32 UART pins: **3.3 V tolerant**
- ✔ Direct connection supported
- ❌ Do NOT connect to 5 V UARTs

---

## Tested Configurations

✔ Pi TX → STM32 RX  
✔ Pi TX split to USB-UART RX for monitoring  
✔ Shared ground across all devices  

---

## Common Issues

| Symptom | Likely Cause |
|-------|--------------|
| No response | Missing ground |
| Garbled input | Baud mismatch |
| Intermittent | Polling-based RX |
| Works from PC but not Pi | Weak edges / timing |

---

## Debug Tip

You can observe Pi output using:

```bash
cat /dev/ttyAMA0

Or with a USB-UART adapter in parallel.


---

# 3️⃣ `docs/setup_pi.md`

```markdown
# Raspberry Pi Setup Guide

This guide walks through configuring the Raspberry Pi to stream GPU telemetry to the LED cube.

---

## Enable UART

```bash
sudo raspi-config

Interface Options → Serial

Disable login shell

Enable serial hardware

Reboot
