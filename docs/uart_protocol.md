# UART Protocol Specification

This document defines the UART communication protocol between the Raspberry Pi and the STM32/GD32 LED cube controller.

---

## Electrical Characteristics

- Logic level: **3.3 V TTL**
- Signaling: **UART (asynchronous)**
- Shared ground required
- No level shifting required

---

## UART Configuration

| Parameter     | Value        |
|---------------|--------------|
| Baud rate     | 9600 or 115200 (must match both sides) |
| Data bits     | 8            |
| Parity        | None         |
| Stop bits     | 1            |
| Flow control  | None         |

---

## Message Format

Messages consist of an ASCII decimal number followed by a line terminator.

<digits><newline>


### Valid Range

- Minimum: `0`
- Maximum: `99`

### Line Terminators

Accepted terminators:
- `\n` (LF)
- `\r\n` (CRLF)

---

## Examples

| Message | Meaning |
|-------|--------|
| `0\n` | Turn display OFF |
| `1\n` | Display 1 LED |
| `25\n` | Display 25 LEDs |
| `99\n` | Display maximum LEDs |

---

## Behavior Rules (STM32 Side)

- Digits are accumulated until a newline is received
- On newline:
  - Value is parsed
  - Clamped to `0–99`
  - Display is **cleared immediately**
  - New LED count is applied
- Invalid characters reset the receive buffer
- Empty lines are ignored

---

## Timing Considerations

- No inter-character delay required
- STM32 uses **interrupt-driven RX**
- Protocol is tolerant of variable frame spacing
- Repeated values are accepted

---

## Error Handling

| Condition | Behavior |
|---------|----------|
| Non-digit input | Reset buffer |
| Value > 99 | Clamped |
| Empty frame | Ignored |
| Partial frame | Wait for newline |

---

## Rationale

This protocol was chosen for:
- Debuggability via terminal
- Human readability
- Immunity to framing errors
- Ease of scripting and testing

