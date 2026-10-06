# GPIO Reference — IRX

This table summarizes all hardware GPIO assignments used in the official IRX firmware release.

---

## 1. GPIO Pinout Table

| GPIO Pin | Pad Type | Direction | Connected Device | Function / Engineering Notes |
|:---:|:---:|:---:|:---|:---|
| **GPIO 14** | RTC / IO | Input | TSOP1838 OUT | Active-low IR pulse input. High-speed interrupt capable. Avoids boot strapping pins. |
| **GPIO 4** | RTC / IO | Output | 2N2222 Base | Transistor driver input via 1 kΩ. Driven by ESP32 hardware RMT carrier channel. |
| **GPIO 2** | Strapping | Output | Status LED | Built-in DevKit LED / External status indicator. |
| **GPIO 32** | RTC / IO | Input | Learn Switch | Pushbutton to GND with software internal pullup (`INPUT_PULLUP`). |
| **GPIO 27** | Digital IO | Input | Reset Switch | Pushbutton to GND with software internal pullup (`INPUT_PULLUP`). |
| **GPIO 33** | RTC / IO | Input | Send Switch | Optional hardware test trigger pushbutton (`INPUT_PULLUP`). |
| **GPIO 21** | Digital IO | I/O | SSD1306 SDA | Hardware I2C data bus for optional OLED. |
| **GPIO 22** | Digital IO | Output | SSD1306 SCL | Hardware I2C clock bus for optional OLED. |

---

## 2. Protected & Avoided GPIOs

To maintain reliability, the following pins are **strictly unused** in the IRX firmware:

- **GPIO 6, 7, 8, 9, 10, 11**: Dedicated to internal SPI flash memory. Using these causes instantaneous processor crash.
- **GPIO 0, 12, 15**: Strapping pins governing boot mode, ROM UART download, and SPI flash voltage. Connecting loads could prevent booting.
- **GPIO 34, 35, 36, 39**: Input-only pins lacking internal pull-up/pull-down resistors.
