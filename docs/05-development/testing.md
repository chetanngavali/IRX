# Testing & Quality Assurance — IRX

IRX underwent a comprehensive hardware verification protocol prior to the v1.0.0 release.

---

## 1. Quality Assurance Verification Matrix

| Test ID | Domain | Test Scenario | Acceptance Criteria | Verified |
|:---:|:---|:---|:---|:---:|
| **QA-01** | Power Rail | 5V and 3.3V voltage ripple | Voltage variation $< 5\%$ during optical burst | **PASS** |
| **QA-02** | Optical RX | TSOP1838 sensitivity | Detects pulses up to 8 meters line-of-sight | **PASS** |
| **QA-03** | Protocol | NEC 32-bit protocol decoding | Correct address, command, and 32-bit hex code | **PASS** |
| **QA-04** | Protocol | Samsung 32-bit protocol decoding | Correct 32-bit hex code identified | **PASS** |
| **QA-05** | Protocol | Sony SIRC (12/15/20-bit) decoding | Decodes across 40 kHz modulation | **PASS** |
| **QA-06** | Fallback | Air Conditioner long raw burst | Captures $> 100$ pulses without truncation | **PASS** |
| **QA-07** | Storage | Cold boot persistence | Learned commands survive complete power cut | **PASS** |
| **QA-08** | Optical TX | RMT 38 kHz hardware carrier | Timing error $< 0.5\%$ measured on logic analyzer | **PASS** |
| **QA-09** | End-to-End | Real consumer TV response | Physical TV turns on/off via web UI button | **PASS** |
| **QA-10** | End-to-End | Real split AC response | Physical AC temperature changes via web UI | **PASS** |
| **QA-11** | Network | Station mode auto-fallback | Re-enables SoftAP within 20s if router drops | **PASS** |

---

## 2. Logic Analyzer Trace Verification

```text
Original Remote (TSOP1838 OUT on GPIO 14):
  ──┐     ┌─┐ ┌─┐   ┌─┐ ┌─┐ ┌─┐   ┌─┐ ┌───
    └─────┘ └─┘ └───┘ └─┘ └─┘ └───┘ └─┘
    [ 9024 ] [ 4512 ] [560] [1690] [560] ... (NEC 32-bit: 0x20DF10EF)

IRX Hardware Replay (GPIO 4 RMT Output):
  ──┐     ┌─┐ ┌─┐   ┌─┐ ┌─┐ ┌─┐   ┌─┐ ┌───
    └─────┘ └─┘ └───┘ └─┘ └─┘ └───┘ └─┘
    [ 9020 ] [ 4510 ] [562] [1688] [560] ... (Error < 0.2%)
```
