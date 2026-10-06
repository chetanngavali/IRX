# IRX Firmware Repository

This directory contains release metadata and official pre-compiled firmware binaries for the **IRX Universal IR System**.

---

## 1. Official Releases

- [Release v1.0.0 (Latest)](file:///c:/Users/cheta/Desktop/IRX/firmware/releases/v1.0.0/)
  - `IRX-v1.0.0.bin`: Application firmware binary (ESP32 Xtensa Dual-Core)
  - `IRX-v1.0.0-littlefs.bin`: Embedded web application filesystem partition
  - `bootloader.bin`: Official ESP32 2nd-stage bootloader
  - `partitions.bin`: Partition table mapping
  - `SHA256SUMS.txt`: Cryptographic integrity checksums

---

## 2. Flashing Instructions

To flash pre-compiled binaries directly to your ESP32 board, follow the instructions in the [Installation Guide](file:///c:/Users/cheta/Desktop/IRX/docs/03-firmware/installation.md).

```bash
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash -z \
  0x1000 firmware/releases/v1.0.0/bootloader.bin \
  0x8000 firmware/releases/v1.0.0/partitions.bin \
  0x10000 firmware/releases/v1.0.0/IRX-v1.0.0.bin \
  0x3D0000 firmware/releases/v1.0.0/IRX-v1.0.0-littlefs.bin
```
