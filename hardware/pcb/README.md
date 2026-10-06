# IRX PCB Layout & Fabrication Notes

### Mechanical & Physical Specifications:
- **Board Type**: 2-Layer FR4 Perfboard / Custom PCB
- **Dimensions**: 50 mm × 70 mm
- **Copper Weight**: 1 oz (35 µm)
- **Minimum Trace Width**: 10 mil (signal), 25 mil (5V LED pulse power traces)
- **Mounting Holes**: 4× M3 mounting holes at corners

### Placement Guidelines:
1. **IR Transmitter LEDs**: Mount at the front edge of the board with clear line of sight, angled slightly outward (~15 degrees) if using multiple LEDs for wider beam spread.
2. **TSOP1838 Receiver**: Mount adjacent to the LEDs with an optical baffle or set back 5 mm to prevent optical feedback when transmitting.
3. **Decoupling Capacitors**: Place the 0.1 µF ceramic capacitor within 10 mm of the TSOP1838 pins. Place the 100 µF bulk capacitor adjacent to the 2N2222 transistor collector loop.
