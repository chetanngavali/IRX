# Features & Capabilities — IRX

IRX combines optical hardware conditioning, high-speed microcontroller timing, and an embedded responsive web application.

---

## 1. Core Hardware & Optical Capabilities

- **38 kHz Optical Front-End**: TSOP1838 / VS1838B active-low receiver with internal bandpass filter and automatic gain control (AGC).
- **Sub-microsecond Capture Buffer**: 1024-sample ring buffer capable of recording long complex multi-byte transmissions (such as Daikin, Mitsubishi, and LG split AC state codes).
- **Hardware-Generated Sub-Carrier (RMT)**: Modulates infrared carriers (36 kHz to 56 kHz) directly using ESP32 hardware Remote Control (RMT) channels with zero CPU jitter.
- **Transistor Optical Driver**: Discrete 2N2222 NPN BJT driver stage capable of driving multiple 940 nm LEDs up to 100 mA peak pulses for $>5$ meters range.
- **Power Decoupling Network**: 100 µF bulk electrolytic reservoir, 10 µF tantalum filter, and 0.1 µF ceramic MLCC bypass to ensure optical bursts do not induce Wi-Fi brownouts.
- **Optional SSD1306 Display**: I2C auto-detection supporting 0.96" 128×64 OLED status displays, with fallback to headless operation.

---

## 2. Firmware & Processing Features

- **Non-Blocking Learning State Machine**: 15-second capture timeout window with visual countdown, allowing uninterrupted web server responsiveness.
- **Multi-Protocol Decoder**: Automatically recognizes standard protocols:
  - NEC / NEC Extended (32-bit)
  - Samsung (32-bit)
  - Sony SIRC (12, 15, and 20-bit)
  - LG (28 and 32-bit)
  - Philips RC5 and RC6
  - Panasonic, JVC, Sharp, Denon
- **Universal RAW Timing Fallback**: When decoding cannot identify a standard frame, the system stores the unadulterated microsecond mark/space array and reproduces it pulse-for-pulse.
- **Atomic Storage**: Every learned command is written to its own JSON file under LittleFS `/commands/<id>.json`, protecting flash lifetime and preventing data corruption.
- **Cascaded Profile Deletion**: Removing an appliance profile automatically removes all corresponding button commands.

---

## 3. Wireless & Network Features

- **Standalone Access Point Mode**: Broadcasts an independent Wi-Fi AP (`IRForge-XXXX`, default password `irforge123`) requiring no external router.
- **Station Mode Support**: Easily attaches to existing home Wi-Fi networks via web UI settings.
- **Automatic Fallback Watchdog**: If home router connection drops for $>20\,\text{seconds}$, IRX automatically restores its standalone Access Point so access is never lost.
- **Local Embedded Single-Page App (SPA)**: Modern, lightweight HTML5/CSS/JavaScript web dashboard served directly from flash memory.
- **Full REST API**: Asynchronous JSON endpoints on port 80 for status, appliance profiles, signal acquisition, and transmission.
