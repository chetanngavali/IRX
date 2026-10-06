# Firmware Overview — IRX

The IRX firmware is an asynchronous, event-driven embedded application built for the dual-core 240 MHz ESP32 microcontroller.

---

## 1. Firmware Design Highlights

- **Zero-Jitter Hardware Modulation**: Utilizes ESP32 Remote Control (RMT) hardware peripherals to synthesize carrier frequencies (typically 38 kHz), eliminating software timing jitters caused by Wi-Fi interrupts.
- **Universal Protocol & RAW Fallback**: Automatically decodes recognized consumer protocols (NEC, Samsung, Sony, LG, RC5/6, Panasonic, etc.) while always capturing and storing raw microsecond pulse arrays for unrecognized signals.
- **Asynchronous Web & REST Architecture**: Built with `ESPAsyncWebServer`, providing responsive HTTP serving on port 80 without blocking real-time operations.
- **Fail-Safe Storage**: LittleFS filesystem layout ensures atomic command writes, flash wear leveling, and complete persistence across cold reboots.
- **Self-Healing Wi-Fi**: Broadcasts an isolated Access Point (`IRForge-XXXX`) by default, with Station mode support and a 20-second watchdog that restores AP mode if the home router disconnects.

---

## 2. Memory & Flash Footprint (v1.0.0 Release)

| Resource | Used | Total Available | Percentage |
|:---|:---|:---|:---:|
| **RAM (Heap)** | 46.5 KB | 327.6 KB | **14.2%** |
| **Flash Memory** | 997.4 KB | 1.96 MB (App partition) | **50.7%** |
| **LittleFS Filesystem** | 15.3 KB (Assets) | 192.0 KB | **8.0%** |

The system retains over **280 KB of free dynamic heap memory**, providing ample buffer space for concurrent HTTP connections and long infrared waveform buffers.
