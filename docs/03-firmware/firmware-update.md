# Firmware Update Guide — IRX

This guide explains how to update the IRX firmware and web interface filesystem on existing hardware.

---

## 1. Release Verification

Before updating, verify that the downloaded firmware binaries match the official cryptographic hashes in `firmware/releases/<version>/SHA256SUMS.txt`:

```bash
# On Windows:
certutil -hashfile firmware/releases/v1.0.0/IRX-v1.0.0.bin SHA256

# On Linux / macOS:
sha256sum -c firmware/releases/v1.0.0/SHA256SUMS.txt
```

---

## 2. In-Place Firmware Updating via Serial

To upgrade firmware while **preserving all stored appliance profiles and learned buttons**:
- Flash **only** the application partition (`0x10000`).
- Do **not** re-flash the filesystem image or erase flash.

```bash
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash 0x10000 firmware/releases/v1.0.0/IRX-v1.0.0.bin
```

Because your stored appliances and buttons reside in LittleFS at offset `0x3D0000`, writing to `0x10000` leaves all user commands intact.

---

## 3. Web UI Asset Update Only

If updating only the web interface files without touching the core firmware:
```bash
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash 0x3D0000 firmware/releases/v1.0.0/IRX-v1.0.0-littlefs.bin
```
