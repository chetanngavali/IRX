# Hardware Overview — IRX

IRX is designed to run on the **Espressif ESP32-WROOM-32** (DevKit V1 38-Pin), augmented by discrete optical receiving and high-current optical transmission stages.

---

## 1. Key Components

1. **Microcontroller**: ESP32-WROOM-32 (240 MHz dual-core, 520 KB SRAM, 4 MB SPI Flash).
2. **Optical Receiver**: TSOP1838 or VS1838B (integrated 38 kHz bandpass filter and PIN photodiode).
3. **Optical Emitter**: 5mm 940 nm High-power infrared LEDs (such as Vishay TSAL6200).
4. **Switching Transistor**: 2N2222 / 2N2222A NPN BJT in TO-92 package.
5. **Passive Network**: 1 kΩ base resistor, 100 Ω current limiter, 0.1 µF ceramic MLCC, 10 µF tantalum capacitor, and 100 µF bulk capacitor.
6. **User Interface**: Blue LED (GPIO 2), tactile switches (GPIO 32, GPIO 27), and optional SSD1306 0.96" OLED on I2C.

---

## 2. Power Tree & Safety Design

Because infrared LEDs require significant peak currents during pulse bursts (up to $100\,\text{mA}$ peak at 33% duty cycle), driving LEDs directly from ESP32 GPIOs will damage the microcontroller. IRX uses a dedicated transistor driver:

```text
USB +5V Rail
    │
    ├─────────────────────────────> [2N2222 Driver & IR LEDs] ── (100µF Bulk Cap)
    │
    ▼
[3.3V LDO Regulator]
    │
    ├─────────────────────────────> [ESP32 3V3 Rail]
    │
    └─[ 100Ω Resistor ]───────────> [TSOP1838 VCC] ───────────── (0.1µF Bypass Cap)
```

- **Bulk Storage Capacitor (100 µF)**: Positioned close to the IR LED circuit on the 5V rail to prevent voltage dips during optical bursts that could trigger ESP32 brownout resets.
- **TSOP Power Filtering (100 Ω + 0.1 µF)**: Forms an RC low-pass filter protecting the receiver's automatic gain control (AGC) against high-frequency Wi-Fi RF noise.
