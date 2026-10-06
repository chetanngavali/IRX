<p align="center">
  <img src="../../assets/logo/IRX-logo.png" alt="IRX Logo" width="280" />
</p>

# Getting Started — IRX

Welcome to **IRX**! This guide walks you through setting up and using your universal remote device.

---

## 1. Quick Setup in 4 Steps

```text
Step 1: Power On       Step 2: Connect Wi-Fi     Step 3: Open Browser      Step 4: Control!
+---------------+       +------------------+     +------------------+     +---------------+
| Plug ESP32    | ----> | Join Wi-Fi:      | --> | Open URL:        | --> | Learn and send|
| into 5V USB   |       | "IRForge-XXXX"   |     | http://192.168.4.1|    | IR commands   |
+---------------+       +------------------+     +------------------+     +---------------+
```

1. **Power Up**: Plug your IRX device into any 5V USB port. The onboard blue LED will illuminate solid.
2. **Join Wi-Fi**: On your smartphone or laptop, connect to the Wi-Fi network:
   - **SSID**: `IRForge-XXXX`
   - **Password**: `irforge123`
3. **Open Dashboard**: In any browser, navigate to:
   ```
   http://192.168.4.1
   ```
4. **Create Appliance**:
   - Go to the **Devices & Remotes** tab.
   - Click **+ Add Appliance**.
   - Enter your device name (e.g., `Living Room TV`) and category (e.g., `Television (TV)`).
   - Click **Create Appliance**.

---

## 2. LED Status Indicators

| LED State | Status Meaning |
|:---|:---|
| **Solid ON** | System ready and idle. |
| **Slow Blink** (500 ms) | Listening for an IR signal (Learn mode active). |
| **Fast Blink** (80 ms) | Signal detected; decoding and processing. |
| **Triple Quick Blink** | Capture or transmission error. |
