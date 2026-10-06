# Transmitting a Command — IRX

Transmitting infrared commands with IRX can be done via the web interface, physical buttons, or the REST API.

---

## 1. Transmitting via the Web Interface

1. Open `http://192.168.4.1` (or your local Station IP).
2. Go to the **Devices & Remotes** tab.
3. Tap on your appliance card to display its remote control keypad.
4. Click any button (e.g., `Power`, `Volume Up`).
5. A confirmation toast (`Transmitting: Power...`) will appear, and the IR LEDs will emit the pulse packet.

---

## 2. Transmitting via REST API (Automation & Scripts)

You can trigger any learned command from a script, Home Assistant, curl, or automation platform:

```bash
# Transmit a command by ID:
curl -X POST http://192.168.4.1/api/commands/cmd_1712345678/send
```

**Response**:
```json
{
  "status": "transmitted",
  "id": "cmd_1712345678"
}
```

---

## 3. Optical Positioning & Range Tips

- **Direct Line of Sight**: Aim the IR LEDs toward the target appliance for best performance.
- **Operating Range**: With the standard 100 Ω current-limiting resistor, range is approximately **5–8 meters**.
- **Camera Check**: You can verify that the IR LEDs are transmitting by pointing a smartphone camera (front-facing camera recommended) at the LEDs while clicking transmit. You will observe a distinct violet-pink flicker.
