# IRForge V1 - Change Log

All notable changes to the IRForge project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-10-06

### Added
- **Hardware Architecture**:
  - Centralized pin configuration in `src/config/pins.h`.
  - TSOP1838 / VS1838B 38 kHz optical receiver input on GPIO 14 with 0.1 µF bypass filtering.
  - 2N2222 NPN BJT driver stage on GPIO 4 with 1 kΩ base resistor and 100 Ω collector current limiter driving 940 nm IR LEDs.
  - 100 µF bulk capacitor on the 5V rail to prevent ESP32 power dips during pulse bursts.
  - Tactile hardware push buttons for Learn (GPIO 32) and Wi-Fi reset (GPIO 27).
  - Optional SSD1306 0.96" OLED display support with automatic I2C detection and headless fallback.
- **Firmware Engine**:
  - `IRReceiverManager`: Non-blocking 1024-element tick ring buffer, 50 ms gap timeout, multi-protocol decoding, and raw microsecond timing capture.
  - `IRTransmitterManager`: Hardware RMT carrier generation for protocol synthesis and raw mark/space pulse replay.
  - `IRStorage`: LittleFS filesystem persistence (`/devices.json`, `/commands/<id>.json`) and NVS Preferences (`irforge_wifi`).
  - `DeviceManager`: Appliance profile and command management with cascaded deletion.
  - `WiFiManager`: Dual-mode Wi-Fi with default Access Point (`IRForge-XXXX`), Station mode, and automatic disconnection recovery.
  - `WebServerManager`: Embedded asynchronous HTTP REST API server on port 80.
- **Web Interface**:
  - Responsive Single-Page Application (SPA) stored in LittleFS (`index.html`, `style.css`, `app.js`).
  - Appliance management with dedicated remote control keypads.
  - 3-step learning wizard with real-time countdown timer and waveform analysis preview.
  - System diagnostics reporting free heap RAM, flash usage, and IP configuration.
- **Engineering Documentation**:
  - Complete 10-document core engineering suite in `docs/` covering specifications, architecture, hardware design, BOM, firmware, protocols, REST API, storage format, test matrix, and user manual.
