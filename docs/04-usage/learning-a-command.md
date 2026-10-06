# Learning a Command — IRX

IRX makes capturing infrared buttons from original manufacturer remotes straightforward and reliable.

---

## 1. Step-by-Step Learning Procedure

```text
[ Step 1: Select Device ] ──> [ Step 2: Button Name ] ──> [ Step 3: Start Listening ]
                                                                   │
                                                                   ▼
       Aim original remote at TSOP sensor (5-15 cm) <──────────────┤ (15s countdown)
       Press button on original remote (e.g. POWER)
                               │
                               ▼
                    [ IR SIGNAL DETECTED ]
                               │
                     [ Test Signal (Send) ] ── (Verify appliance reacts)
                               │
                     [ Save Command ] ─────── (Saved to flash memory)
```

1. Navigate to the **Learn New Signal** tab in the web dashboard.
2. Under **Step 1**, pick your target appliance from the dropdown.
3. Under **Step 2**, enter the button name (e.g., `Power`, `Volume Up`, `Mute`, `HDMI 1`).
4. Under **Step 3**, click **Start Listening**.
   - The status LED will start blinking slowly.
   - A 15-second countdown timer will display on screen.
5. Aim your original remote control directly at the dark dome of the **TSOP1838 receiver** (distance: 5–15 cm) and press the button firmly.
6. The web app will report **IR SIGNAL DETECTED** and display the decoded protocol, carrier frequency, hex code, and raw sample count.
7. Click **Test Signal (Send)** to confirm your appliance responds.
8. Click **Save Command**. The signal is now stored permanently in flash memory.

---

## 2. Unknown or Complex AC Protocols

If your remote uses an unclassified or complex protocol (such as long-frame split air conditioners):
- The system automatically captures the full microsecond mark/space array and labels it as **RAW**.
- Click **Test Signal (Send)** to verify operation, then click **Save Command**. IRX will replay the exact recorded pulse train during normal use.
