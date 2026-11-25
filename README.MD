# sOS Nano 256B



Version: 0.6 – Experimental

## Overview

sOS Nano 256B is an experimental miniature operating system designed to fit entirely into 256 bytes of RAM. It is written in native RCA CDP1802 hexadecimal machine code.

The project explores how much functionality can be implemented with extremely limited hardware resources.

## Hardware requirements

sOS Nano 256B is specifically designed for a modified **RCA COSMAC Microtutor II**, featuring:

- RCA CDP1802 COSMAC 8-bit microprocessor
- 256 bytes of RAM
- Two hexadecimal seven-segment displays
- Custom eight-LED binary output display
- Custom hexadecimal input keypad
- RUN, LOAD and memory protection controls
- IN button

Compatibility with unmodified Microtutor II systems or other CDP1802-based computers is not guaranteed.

## Features

- Animated 505 (sOS) boot sequence
- Hexadecimal command shell
- Native 8-bit calculator
- Addition, subtraction, multiplication and division
- Print command
- 15-byte writable RAM storage (sFS)
- LED-based Pong game (sPong)
- Highscore storage
- Visual system status indicators

## Commands

| Input | Function |
|---|---|
| 00 | Start sPong |
| 01 | Display highscore |
| 11 XX | Print byte XX |
| F5 00 | Read stored data |
| F5 01 | Write 15 bytes to RAM storage |
| XX FF YY | Addition |
| XX EE YY | Subtraction |
| XX DD YY | Multiplication |
| XX CC YY | Division |

All input and output values are hexadecimal.

Example: 23 FF 11 should return 34.

## System status codes

| Display | Meaning |
|---|---|
| 50 → 05 | Boot animation |
| FF | Boot successful |
| C1 | User input required |
| 10 | Processing |
| EE | Error |

## sPong

sPong is a minimal reaction game designed for the eight-LED output display.

A single light moves across the LEDs. The player must press the IN button when the final LED lights up.

- Resolution: 8 × 1 pixels
- Color depth: 1 bit
- Target reaction window: 500 ms
- Maximum highscore: 255 points
- Early or late input results in game over

The highscore is stored in RAM.

## sFS

sFS provides 15 bytes of writable, volatile user storage, equivalent to 30 hexadecimal characters.

Stored bytes are intended to be treated as data rather than executable instructions. Data is not encrypted and is lost when RAM contents are lost.

## Memory layout

The intended memory allocation for version 0.6 is:

| Address range | Purpose | Size |
|---|---|---:|
| 00–EE | Operating system | 239 B |
| EF | Highscore | 1 B |
| F0–FE | User storage | 15 B |
| FF | I/O buffer | 1 B |
| Total | | 256 B |

No heap, swap, external storage or dynamic memory allocation is required by design.

## Installation

1. Switch the computer to LOAD mode.
2. Disable memory write protection.
3. Enter the hexadecimal machine code starting at address 0000.
4. Reset the processor without clearing RAM.
5. Switch to RUN mode.

The current implementation assumes I/O port 4, an active-low EF4 input signal and disabled automatic memory switching.

## Development status

Version 0.6 is an experimental prototype. The machine code, memory layout, timing and listed functionality have not yet been fully verified on the original hardware.

## Disclaimer

This software is provided "AS IS", without warranty of any kind, express or implied.

Use this software at your own risk. To the extent permitted by applicable law, the author accepts no liability for hardware damage, data loss, malfunctions or other damages resulting from its use.

Always follow the electrical specifications and operating instructions of your hardware.

## Author

Developed by Yenoyosh, 2026.

---
