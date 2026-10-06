# Bill of Materials (BOM) — IRX

| Document ID | IRX-BOM-001 |
|:---|:---|
| **Revision** | Rev 1.0 |
| **System** | Universal IR Learning & Control Appliance |

---

## 1. Component Master Table

| Item | Component Description | Designator | Package / Footprint | Qty | Target Specification | Est. Unit Cost ($) | Est. Total Cost ($) |
|:---|:---|:---|:---|:---:|:---|:---:|:---:|
| **1** | ESP32 Development Board | U1 | DevKit V1 38-Pin | 1 | Dual-core 240 MHz, 4MB Flash | $3.50 | $3.50 |
| **2** | 38 kHz IR Receiver IC | U2 | 3-Pin Through-Hole | 2 | TSOP1838 / VS1838B 38 kHz | $0.40 | $0.80 |
| **3** | 940 nm High-Power IR LED | D1, D2 | 5mm Round T-1 3/4 | 4 | 940 nm, $V_F \approx 1.3\,\text{V}$, 100 mA pulsed | $0.15 | $0.60 |
| **4** | NPN Switching Transistor | Q1 | TO-92 Through-Hole | 2 | 2N2222 / 2N2222A ($I_C=800\,\text{mA}$) | $0.10 | $0.20 |
| **5** | Base Resistor 1 kΩ | R1 | 1/4W Axial | 4 | 1 kΩ, 5% Carbon/Metal Film | $0.02 | $0.08 |
| **6** | Current Limiting Resistor 100 Ω | R2, R3 | 1/2W Axial | 4 | 100 Ω, 5%, 0.5 Watt | $0.04 | $0.16 |
| **7** | Status Resistor 330 Ω | R4 | 1/4W Axial | 2 | 330 Ω, 5% | $0.02 | $0.04 |
| **8** | Bypass Capacitor 0.1 µF | C1 | Ceramic 5.08mm | 5 | 100 nF / 50V X7R MLCC | $0.03 | $0.15 |
| **9** | Filter Capacitor 10 µF | C2 | Radial Electrolytic | 3 | 10 µF / 25V Electrolytic | $0.05 | $0.15 |
| **10**| Bulk Rail Capacitor 100 µF | C3 | Radial Electrolytic | 2 | 100 µF / 16V Low-ESR | $0.08 | $0.16 |
| **11**| Tactile Push Buttons | SW1, SW2 | 6x6x5mm Momentary | 3 | SPST Through-Hole Tact Switch | $0.08 | $0.24 |
| **12**| Blue Status LED | D3 | 3mm / 5mm Through-Hole | 2 | 3mm / 5mm Blue LED | $0.05 | $0.10 |
| **13**| Prototype Breadboard / Perfboard | BRD1 | 400 Tie-Point / Perfboard | 1 | Standard Solderless Breadboard | $2.20 | $2.20 |
| **14**| Dupont Jumper Wires | W1 | 22 AWG M-to-M / M-to-F | 1 | 40-pin Ribbon Wire Bundle | $1.20 | $1.20 |
| **15**| Micro-USB Data Cable | CB1 | 1 Meter USB-A to Micro-B | 1 | 28/24 AWG Data & Sync Cable | $1.50 | $1.50 |

---

## 2. Total Cost Summary

- **Total Prototype BOM Cost (Single Unit)**: **~$11.08 USD**
- **Estimated Production Cost (100+ PCB Units)**: **~$5.40 USD** per device
