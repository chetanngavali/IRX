# IRX — Universal IR Learning & Control System for ESP32

<p align="center">
  <img src="assets/logo/IRX-logo.svg" alt="IRX Logo" width="360" />
</p>

<p align="center">
  <strong>Autonomous ESP32-based universal infrared remote learning, storage, and wireless transmission appliance.</strong><br>
  <em>"Learn. Store. Control."</em>
</p>

<p align="center">
  <a href="#quick-start"><img src="https://img.shields.io/badge/Release-v1.0.0-blue.svg" alt="Release v1.0.0"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License MIT"></a>
  <a href="docs/02-hardware/hardware-overview.md"><img src="https://img.shields.io/badge/Hardware-ESP32%20DevKit%20V1-red.svg" alt="Hardware ESP32"></a>
  <a href="docs/03-firmware/firmware-overview.md"><img src="https://img.shields.io/badge/Flash-LittleFS-orange.svg" alt="LittleFS"></a>
</p>

---

## 🌟 Overview

**IRX** is a hardware and firmware appliance that turns an ESP32 into a standalone universal remote hub. It captures incoming infrared signals from existing physical remotes with microsecond timing accuracy, decodes standard industry protocols, persists signals in non-volatile flash memory, and re-transmits them on demand via high-power infrared LEDs.

Target appliances include **Televisions**, **Air Conditioners**, **Set-Top Boxes**, **Audio Receivers**, **Soundbars**, **Projectors**, and domestic **Fans**.

> 🔒 **Security Notice**: IRX is designed exclusively for domestic and workplace consumer electronics. Automotive access control (car keys, keyfobs, immobilizer bypass) and rolling-code replay systems are strictly out of scope.

---

## 🚀 Key Features

- **Microsecond Signal Capture**: TSOP1838 / VS1838B active-low 38 kHz optical receiver input with 1024-sample raw ring buffer.
- **Hybrid Decoding + RAW Fallback**: Recognizes NEC, Samsung, Sony SIRC, LG, RC5/6, and Panasonic, while always capturing raw pulse trains for unclassified remotes and complex split-AC state frames.
- **Hardware-Generated Carrier (RMT)**: Synthesizes precise 36–56 kHz carrier modulation using ESP32 hardware Remote Control (RMT) channels with zero software jitter.
- **2N2222 Transistor Optical Driver**: Drives 940 nm IR LEDs up to 100 mA peak current pulses safely from the 5V power bus, achieving $>5$ meters transmission range.
- **Non-Volatile Persistence**: Saves appliance profiles and commands into on-chip LittleFS and NVS Preferences. Data persists across reboots and power losses.
- **Zero Cloud Dependencies**: Hosts an embedded, responsive Single-Page Application (SPA) directly from flash memory. Operates as an isolated Wi-Fi Access Point (`IRForge-XXXX`) or joins home Wi-Fi networks in Station mode.
- **Full REST API**: Asynchronous JSON endpoints on port 80 for status diagnostics, appliance management, signal acquisition, and transmission.

---

## 📁 Repository Structure

```text
IRX/
├── docs/
│   ├── 01-overview/             # Specifications, features, system architecture
│   ├── 02-hardware/             # Schematics, wiring guide, GPIO table, BOM
│   ├── 03-firmware/             # Installation, flashing, updates
│   ├── 04-usage/                # User guide, learning signals, transmitting, troubleshooting
│   └── 05-development/          # QA test matrix, release process
│
├── hardware/
│   ├── schematics/              # Schematic diagrams and reference docs
│   ├── pcb/                     # PCB layout and fabrication notes
│   └── bom/                     # IRX-BOM.csv (machine-readable BOM)
│
├── firmware/
│   ├── releases/v1.0.0/         # Pre-compiled binaries & SHA256SUMS.txt
│   └── README.md                # Flashing guide
│
├── assets/
│   └── logo/                    # IRX brand SVG assets
│
├── examples/
│   └── sample-ir-profile.json   # Sample appliance & command JSON dataset
│
├── README.md                    # Project landing page
├── LICENSE                      # MIT Open Source License
├── SECURITY.md                  # Vulnerability reporting policy
├── CHANGELOG.md                 # Version history & release notes
└── .gitignore                   # Ignore rules
```

---

## ⚡ Quick Start: Flashing Pre-Compiled Firmware

You can flash official release binaries directly onto any ESP32 DevKit V1 board in seconds using `esptool.py`:

```bash
# 1. Install esptool if needed:
pip install esptool

# 2. Flash release v1.0.0 (replace COM3 with your serial port):
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash -z \
  0x1000 firmware/releases/v1.0.0/bootloader.bin \
  0x8000 firmware/releases/v1.0.0/partitions.bin \
  0x10000 firmware/releases/v1.0.0/IRX-v1.0.0.bin \
  0x3D0000 firmware/releases/v1.0.0/IRX-v1.0.0-littlefs.bin
```

---

## 🔌 Hardware Wiring Summary

| Signal | ESP32 GPIO | Direction | Connected Peripheral |
|:---|:---:|:---:|:---|
| **`IR_RECEIVE`** | **GPIO 14** | Input | TSOP1838 Data OUT (Active Low) |
| **`IR_TRANSMIT`** | **GPIO 4** | Output | 2N2222 Base via 1 kΩ (Hardware RMT) |
| **`STATUS_LED`** | **GPIO 2** | Output | Built-in DevKit Blue LED |
| **`BUTTON_LEARN`** | **GPIO 32** | Input | Tactile Pushbutton to GND (`INPUT_PULLUP`) |
| **`BUTTON_RESET`** | **GPIO 27** | Input | Tactile Pushbutton to GND (`INPUT_PULLUP`) |
| **`OLED_SDA`** | **GPIO 21** | I/O | Optional SSD1306 OLED (I2C) |
| **`OLED_SCL`** | **GPIO 22** | Output | Optional SSD1306 OLED (I2C) |

*For complete wiring diagrams and transistor calculations, see the [Wiring Guide](docs/02-hardware/wiring-guide.md).*

---

## 📖 Documentation Index

- **System Architecture**: [docs/01-overview/system-architecture.md](docs/01-overview/system-architecture.md)
- **Hardware Overview**: [docs/02-hardware/hardware-overview.md](docs/02-hardware/hardware-overview.md)
- **Wiring Guide**: [docs/02-hardware/wiring-guide.md](docs/02-hardware/wiring-guide.md)
- **Bill of Materials**: [docs/02-hardware/bill-of-materials.md](docs/02-hardware/bill-of-materials.md)
- **Installation Guide**: [docs/03-firmware/installation.md](docs/03-firmware/installation.md)
- **Learning a Command**: [docs/04-usage/learning-a-command.md](docs/04-usage/learning-a-command.md)
- **Transmitting Signals**: [docs/04-usage/transmitting-a-command.md](docs/04-usage/transmitting-a-command.md)
- **Troubleshooting**: [docs/04-usage/troubleshooting.md](docs/04-usage/troubleshooting.md)
- **Testing & QA Matrix**: [docs/05-development/testing.md](docs/05-development/testing.md)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
