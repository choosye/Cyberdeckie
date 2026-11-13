# Cyberdeckie
Half Life Hack Club Week 5 - Cyberdeckie

<img width="1200" height="1360" alt="cyberdeckie_mockup" src="https://github.com/user-attachments/assets/aaae39b8-8bc9-4540-aa0e-8ee3f4b06cdd" />


## What it is 
A clamshell handheld Linux terminal built around a Raspberry Pi Zero 2 W, with a 3.5" screen, a 40-key keyboard and its own rechargeable battery. Made for Hack Club Half Life, Week 5. 

## Features
- Raspberry Pi Zero 2 W running Linux, mounted like a HAT on a 2×20 socket
- 3.5" ST7796 IPS display (480×320) over SPI, connected by a 14-pin FPC cable
- 40-key (4×10) matrix keyboard with a diode on every key
- USB-C charging with power-path (it can run while charging)
- 1S LiPo battery boosted to a steady 5 V
- Power slide switch + safe-shutdown button
- 3 status LEDs (charging, USB connected, power)
- Serial debug header for when the screen/keyboard aren't working yet

## PCB
<img width="741" height="536" alt="Screenshot 2026-11-14 at 12 39 57 AM" src="https://github.com/user-attachments/assets/d3b179cd-85ac-4ebe-9d6a-483ef232a0d9" />

## How it works

Power: USB-C (5.1k CC resistors) → BQ24074 charger/power-path → VSYS → TPS61023 boost → +5 V for the Pi and display. The slide switch controls the boost converter's EN pin.

Display: SPI0 (MOSI, SCLK, CE0) plus DC, RST and a backlight PWM pin. The module has its own backlight transistor.

Keyboard: 4 rows × 10 columns on GPIOs, active-low, with 1N4148W diodes (cathode toward the column) so pressing multiple keys doesn't cause ghosting.

Shutdown button: on GPIO3, which can both trigger a safe shutdown and wake the Pi (dtoverlay=gpio-shutdown).

Serial debug (J1): UART TX/RX/GND for a USB-serial adapter.

