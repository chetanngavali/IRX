# Installation Guide — IRX

This guide describes how to flash official pre-compiled IRX firmware binaries onto an ESP32 board using `esptool.py`.

---

## 1. Prerequisites

1. An **ESP32 DevKit V1** (or compatible ESP32-WROOM-32) board.
2. A Micro-USB cable supporting data communication.
3. Python 3 with `esptool`:
   ```bash
   pip install esptool
   ```

---

## 2. Flashing Official Release Binaries

Download or navigate to the `firmware/releases/v1.0.0/` directory in this repository:

| Binary File | Flash Address | Description |
|:---|:---:|:---|
| `bootloader.bin` | `0x1000` | Second-stage bootloader |
| `partitions.bin` | `0x8000` | Custom partition table (`min_spiffs.csv`) |
| `IRX-v1.0.0.bin` | `0x10000` | Main application firmware binary |
| `IRX-v1.0.0-littlefs.bin` | `0x3D0000` | Web application filesystem image |

### Single-Command Flash Procedure (Replace `COMx` or `/dev/ttyUSB0` with your port):

#### Windows:
```bash
esptool.py --chip esp32 --port COM3 --baud 921600 --before default_reset --after hard_reset write_flash -z \
  0x1000 firmware/releases/v1.0.0/bootloader.bin \
  0x8000 firmware/releases/v1.0.0/partitions.bin \
  0x10000 firmware/releases/v1.0.0/IRX-v1.0.0.bin \
  0x3D0000 firmware/releases/v1.0.0/IRX-v1.0.0-littlefs.bin
```

#### Linux / macOS:
```bash
esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 921600 --before default_reset --after hard_reset write_flash -z \
  0x1000 firmware/releases/v1.0.0/bootloader.bin \
  0x8000 firmware/releases/v1.0.0/partitions.bin \
  0x10000 firmware/releases/v1.0.0/IRX-v1.0.0.bin \
  0x3D0000 firmware/releases/v1.0.0/IRX-v1.0.0-littlefs.bin
```

---

## 3. Post-Flash Verification

1. Open a serial terminal at **115200 baud**:
   ```bash
   python -m serial.tools.miniterm COM3 115200
   ```
2. Press the **EN/RST** button on the ESP32. You will see:
   ```text
   ========================================
     IRForge V1: Universal IR Remote System
     Tagline: 'Learn. Store. Control.'
   ========================================
   [IRStorage] LittleFS mounted successfully.
   [WiFi] Access Point started! SSID: IRForge-XXXX, IP: 192.168.4.1
   [WebServer] HTTP Server started.
   ```
3. Look for the Wi-Fi Access Point `IRForge-XXXX` on your mobile phone or computer.
