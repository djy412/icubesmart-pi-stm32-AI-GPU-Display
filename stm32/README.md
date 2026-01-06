## STM32 Firmware

- MCU: STM32F103 / GD32F103
- UART: USART1
- Baud: 9600 (default)
- RX: Interrupt-driven

### Build
- STM32CubeIDE
- Open `CubeMX/icube.ioc`
- Build and flash

### Protocol
Receives ASCII digits terminated by `\n`.
