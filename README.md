# ESP32 Menu-Driven Sensor Dashboard

A menu-based embedded system built on ESP32 that lets you monitor environmental sensors and control a relay — all through a structured OLED interface navigated via your keyboard over serial.

No physical buttons. No clutter. Just clean interaction.


## What It Does

- Displays a navigable menu on a 0.96" OLED screen
- Navigate options using keyboard keys over serial (`W`, `S`, `E`, `B`)
- Read real-time sensor data:
  - Temperature (DHT11)
  - Humidity (DHT11)
  - Light level (LDR)
- Control a relay (ON/OFF) directly from the menu


## Why This Is Different From a Basic Sensor Project

Most beginner ESP32 projects just print sensor values to serial monitor. This one builds a full interaction layer on top:

- Structured menu system with navigation
- User-driven control, not just passive monitoring
- OLED as a real UI, not just a display
- Serial keyboard replaces physical buttons entirely


## Hardware Used

| Component | Purpose |
|-----------|---------|
| ESP32 | Main microcontroller |
| 0.96" OLED (I2C) | Display and UI |
| DHT11 | Temperature & Humidity |
| LDR | Light level sensing |
| Relay Module | Switchable output control |


## Navigation Keys

| Key | Action |
|-----|--------|
| `W` | Move up in menu |
| `S` | Move down in menu |
| `E` | Select / Enter |
| `B` | Back |


## System Flow

```
Keyboard input (Serial)
        ↓
ESP32 reads key
        ↓
Menu index updates
        ↓
OLED refreshes display
        ↓
Selected function runs (sensor read / relay toggle)
```


## Setup Instructions

### 1. Install Libraries

In Arduino IDE, install the following:

- `Adafruit SSD1306` — OLED driver
- `Adafruit GFX` — Graphics library
- `DHT sensor library` — for DHT11

### 2. Wire the Hardware

| Component | ESP32 Pin |
|-----------|-----------|
| OLED SDA | GPIO 21 |
| OLED SCL | GPIO 22 |
| DHT11 Data | GPIO 4 |
| LDR (analog) | GPIO 34 |
| Relay IN | GPIO 26 |

> Note: If OLED doesn't turn on, run an I2C scanner sketch first to confirm the address (usually `0x3C` or `0x3D`).

### 3. Upload the Code

- Open `src/main.ino` in Arduino IDE
- Select your ESP32 board and correct COM port
- Upload

### 4. Open Serial Monitor

- Set baud rate to `115200`
- Use keyboard to navigate the menu


## Debugging Notes

During development, the OLED failed to initialize. The fix process:

1. Ran I2C scanner to detect actual device address
2. Verified SDA/SCL wiring
3. Tested with isolated OLED test sketch
4. Updated address in code


## What I Learned

- Designing a menu-driven UI for embedded systems
- Integrating multiple sensors on one microcontroller
- Replacing hardware input (buttons) with software input (serial)
- Real hardware debugging — I2C address scanning, wiring checks, isolation testing
