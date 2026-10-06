# Project Overview — IRX

| Attribute | Specification |
|:---|:---|
| **Project Name** | **IRX** (Universal IR Learning, Storage & Transmission Appliance) |
| **Hardware Core** | ESP32-WROOM-32 / DevKit V1 (Xtensa Dual-Core 240 MHz) |
| **Operating System** | Embedded FreeRTOS / ESP-IDF Arduino Runtime |
| **Current Release** | v1.0.0 |
| **Tagline** | *"Learn. Store. Control."* |

---

## 1. What is IRX?

**IRX** is an embedded hardware controller designed to bridge legacy infrared (IR) consumer electronics with modern wireless control interfaces. It functions as an autonomous, self-contained infrared transceiver capable of learning original remote control waveforms with microsecond-level fidelity, decoding standard industry protocols, persisting signals in non-volatile flash memory, and re-transmitting them on demand via high-power infrared LEDs.

IRX acts as a universal remote hub for:
- Televisions (Smart TVs, LCD/LED panels, CRT displays)
- Air Conditioners (Split ACs, multi-byte state frames)
- Set-Top Boxes, Cable & Satellite Receivers
- Audio Receivers, Soundbars & Amplifiers
- Projectors & Home Theater Screens
- Domestic Fans & Air Purifiers

---

## 2. Key Architecture Principles

1. **Zero Cloud Dependency**: Operates entirely within the local Wi-Fi environment without external internet, telemetry, or third-party servers.
2. **Hybrid Protocol & RAW Fallback**: Recognizes industry standards (NEC, Samsung, Sony, LG, RC5/6, Panasonic), while guaranteeing pulse-for-pulse RAW reproduction for proprietary or unclassified protocols.
3. **Safe Optical Driving**: Employs an external 2N2222 NPN switching transistor and ESP32 hardware Remote Control (RMT) peripherals to produce high-current modulated carrier pulses ($70\text{–}100\,\text{mA}$ peak) without loading microcontroller GPIO pins.
4. **Persistent On-Device Storage**: Saves appliance profiles and commands into non-volatile SPI flash (LittleFS and NVS Preferences) across reboots and power cuts.

---

## 3. Explicit Boundaries & Safety

IRX is designed strictly for domestic and workplace consumer electronic devices.

### Supported:
- Consumer televisions, climate control systems, media players, audio receivers, and projectors.

### Strictly Out of Scope:
- Automotive access control (car keys, keyfobs, immobilizer bypass).
- Rolling-code / hopping-code replay systems.
- Commercial security access, barriers, or gate transmitters.
