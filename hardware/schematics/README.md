# IRX Hardware Schematics Reference

The official schematic package for **IRX** is documented below in ASCII schematic format.

```text
=============================================================================
                       IRX V1.0 SCHEMATIC DIAGRAM
=============================================================================

1. OPTICAL RECEIVER (TSOP1838)
   +3.3V ──[ 100Ω ]──┬── VCC (Pin 3)
                     │
                    === 0.1µF Ceramic Bypass
                     │
   GND ──────────────┴── GND (Pin 2)
   
   ESP32 GPIO 14 ─────── OUT (Pin 1)


2. HIGH-POWER OPTICAL TRANSMITTER (2N2222 DRIVER)
   +5V (USB / VIN) ──┬── [ 100Ω, 0.5W ] ──┬── [A >| K] IR LED 1 (940nm)
                     │                    │
                    === 100µF Bulk        └── [A >| K] IR LED 2 (Optional)
                     │                               │
   GND ──────────────┘                               │
                                                     ▼ Collector (C)
                                                  +─────+
   ESP32 GPIO 4 ──────[ 1kΩ Base Resistor ]───────┤ Q1  │ 2N2222 NPN
                                         Base (B) │     │
                                                  +──┬──+
                                                     │ Emitter (E)
   GND ──────────────────────────────────────────────┴───────────────


3. TACTILE CONTROL BUTTONS
   ESP32 GPIO 32 ──────[ LEARN Pushbutton ]────── GND (Internal Pullup Active)
   ESP32 GPIO 27 ──────[ RESET Pushbutton ]────── GND (Internal Pullup Active)


4. OPTIONAL SSD1306 OLED (I2C)
   ESP32 GPIO 21 ────── SDA
   ESP32 GPIO 22 ────── SCL
   3.3V ─────────────── VCC
   GND ──────────────── GND
=============================================================================
```
