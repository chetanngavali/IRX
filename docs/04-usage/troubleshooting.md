# Troubleshooting Guide — IRX

This guide addresses common hardware and software questions when using IRX.

---

## 1. Hardware Issues

### Issue 1: TSOP1838 does not detect any IR signals
- **Remedy 1: Verify Pinout**. Facing the front dome:
  - Pin 1 (Left) = `OUT` $\rightarrow$ GPIO 14
  - Pin 2 (Center) = `GND` $\rightarrow$ GND
  - Pin 3 (Right) = `VCC` $\rightarrow$ 3.3V
- **Remedy 2: Add Decoupling**. Place a 0.1 µF capacitor across `VCC` and `GND` right at the TSOP sensor leads.
- **Remedy 3: Receiver Saturation**. Keep the remote at a distance of 5–15 cm. Holding it closer than 5 cm can overwhelm the sensor's automatic gain control.

### Issue 2: Signal captures but TV does not react when transmitted
- **Remedy 1: LED Polarity**. Ensure the long lead (Anode) connects to the resistor/rail, and short lead (Cathode) connects to the transistor collector.
- **Remedy 2: Transistor Pinout**. For the 2N2222 (facing the flat side):
  - Pin 1 (Left) = `Emitter` $\rightarrow$ GND
  - Pin 2 (Center) = `Base` $\rightarrow$ 1 kΩ to GPIO 4
  - Pin 3 (Right) = `Collector` $\rightarrow$ IR LED cathode
- **Remedy 3: Optical Camera Test**. View the IR LED through a smartphone front camera while transmitting. A violet flash confirms the LED is firing.

### Issue 3: ESP32 restarts during IR transmission
- **Remedy**: IR LED pulse bursts draw significant instantaneous current. Install a **100 µF bulk electrolytic capacitor** across the 5V rail and GND close to the transistor circuit.

---

## 2. Network Issues

### Issue 4: Cannot connect to `IRForge-XXXX` Wi-Fi
- **Remedy**: Default password is `irforge123`. If changed or forgotten, hold down the **Reset Button (GPIO 27)** for 2 seconds to revert to default AP mode.

### Issue 5: Web UI does not load at `http://192.168.4.1`
- **Remedy**: Confirm your device hasn't disconnected due to "No internet connection" warnings on mobile phones (select "Stay connected"). Ensure the LittleFS partition was flashed using `IRX-v1.0.0-littlefs.bin`.
