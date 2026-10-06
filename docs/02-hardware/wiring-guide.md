# Wiring Guide & Circuit Schematic — IRX

This guide describes the complete electrical connections for wiring IRX on a breadboard, perfboard, or custom PCB.

---

## 1. Schematic Diagrams

### 1.1 IR Receiver Circuit (TSOP1838)

```text
       TSOP1838 (Front view, bump facing you)
               +-------------+
               |    [ O ]    |
               +-------------+
                 |    |    |
                OUT  GND  VCC
                 |    |    |
                 |    |    +------- +3.3V Rail (via 100Ω filter resistor)
                 |    |               │
                 |    |              === 0.1µF Ceramic Capacitor
                 |    |               │
                 |    +-------------- GND Rail
                 |
                 +------------------- ESP32 GPIO 14
```

> **Note**: Pinout order for TSOP1838 / VS1838B (facing the dome) from left to right is **Pin 1: OUT**, **Pin 2: GND**, **Pin 3: VCC**.

---

### 1.2 High-Power IR Transmitter Circuit (2N2222 Driver)

```text
                                  +5V Rail (USB 5V / ESP32 VIN)
                                   │
                                   ├────────────────────────┐
                                   │                        │
                                  [R2: 100Ω, 0.5W]         === C3: 100µF Bulk Cap
                                   │                        │
                                   ▼ Anode (+)              │
                                 [ |>| ] 940nm IR LED 1     │
                                   │ Cathode (-)            │
                                   ▼ Anode (+)              │
                                 [ |>| ] 940nm IR LED 2     │
                                   │ Cathode (-)            │
                                   │                        │
                                   ▼ Collector (C)          │
                                +─────+                     │
ESP32 GPIO 4 ──[ R1: 1kΩ ]──────┤ Q1  │ 2N2222 NPN BJT      │
 (RMT Signal)    Base (B)       │     │                     │
                                +──┬──+                     │
                                   │ Emitter (E)            │
                                   │                        │
                                   └────────────────────────┴── GND Rail
```

---

### 1.3 Driver Current Calculations

1. **Base Drive Current ($I_B$)**:
   $$I_B = \frac{3.3\,\text{V} - V_{BE(\text{sat})}}{R_1} = \frac{3.3\,\text{V} - 0.7\,\text{V}}{1000\,\Omega} = 2.6\,\text{mA}$$
   *Well within the ESP32 GPIO limit of 12 mA, fully driving the transistor into saturation.*

2. **Collector / LED Pulse Current ($I_C$)**:
   $$I_C = \frac{V_{CC} - V_{F(\text{LED})} - V_{CE(\text{sat})}}{R_2} = \frac{5.0\,\text{V} - 1.3\,\text{V} - 0.2\,\text{V}}{100\,\Omega} = 35\,\text{mA}$$
   *Under pulsed 33% carrier modulation, peak current can be increased up to ~100 mA by using a 33–47 Ω resistor for extended range ($>8$ meters).*

---

## 2. Hardware Buttons & OLED

```text
ESP32 GPIO 32 ──[ Tactile Switch (Learn) ]── GND
ESP32 GPIO 27 ──[ Tactile Switch (Reset) ]── GND

SSD1306 OLED (I2C):
  VCC ──> 3.3V
  GND ──> GND
  SDA ──> GPIO 21
  SCL ──> GPIO 22
```
