# System Architecture — IRX

The IRX system is divided into three distinct operational layers: **Hardware Physical Layer**, **Embedded Firmware Layer**, and the **Presentation / Client Layer**.

---

## 1. High-Level Block Diagram

```text
+=============================================================================+
|                           CLIENT LAYER (Web Browser)                        |
|                                                                             |
|      [ Appliance Dashboard ]    [ Learn Wizard ]    [ Hardware Setup ]      |
+======================================|======================================+
                                       | HTTP Port 80 (JSON REST API)
+======================================v======================================+
|                         EMBEDDED FIRMWARE LAYER                             |
|                                                                             |
|   +---------------------------------------------------------------------+   |
|   |                       Async HTTP Web Server                         |   |
|   +-------------------+-----------------+-------------------+-----------+   |
|                       |                 |                   |               |
|               +-------v-------+  +------v------+     +------v------+        |
|               | DeviceManager |  | WiFiManager |     | OLEDManager |        |
|               +-------+-------+  +-------------+     +-------------+        |
|                       |                                                     |
|               +-------v-------+                                             |
|               |   IRStorage   | (LittleFS /commands/ + Preferences)         |
|               +---+-------+---+                                             |
|                   |       |                                                 |
|          +--------v-+   +-v---------+                                       |
|          | IREngine |   |  RMT TX   |                                       |
|          | (Decode) |   | (Carrier) |                                       |
|          +----+-----+   +-----+-----+                                       |
+===============|===============|=============================================+
                |               |
+===============|===============|=============================================+
|               |               |       HARDWARE PHYSICAL LAYER               |
|               v               v                                             |
|          TSOP1838 OUT    2N2222 Base Driver                                 |
|            (GPIO 14)          (GPIO 4)                                      |
|               ▲               │                                             |
|               │               ▼                                             |
|          Original Remote   940nm High-Power IR Output                       |
|          Photons (38kHz)   to Target Consumer Appliance                     |
+=============================================================================+
```

---

## 2. Firmware Subsystems

1. **Optical Capture Engine (`IRReceiver`)**:
   - High-speed ISR records mark/space intervals into a 1024-element buffer.
   - Detects frame completion upon a 50 ms silence gap.
   - Converts raw timer ticks into microsecond intervals and executes protocol decoding.
2. **Pulse Transmission Engine (`IRTransmitter`)**:
   - Uses ESP32 Remote Control (RMT) hardware modules to synthesize carrier modulation with sub-microsecond precision.
   - Evaluates stored commands: utilizes encoded protocol synthesis when recognized, or replays raw microsecond timing arrays.
3. **Storage Engine (`IRStorage`)**:
   - Manages non-volatile storage using LittleFS for appliance configurations and individual command JSON files.
   - Caches network parameters in ESP32 NVS preferences.
4. **Appliance Profile Engine (`DeviceManager`)**:
   - Bridges high-level appliance models with persistent file storage and enforces cascaded deletion of command files.
5. **Network Watchdog (`WiFiManager`)**:
   - Manages standalone SoftAP mode (`IRForge-XXXX`), connects to home routers in Station mode, and restores AP on signal loss.
6. **Web Server & REST Interface (`WebServer`)**:
   - Asynchronous HTTP server hosting the single-page application and servicing JSON REST endpoints.

---

## 3. Signal Flow Lifecycle

```
[ Step 1: Learning ]
Original Remote ──> TSOP1838 ──> GPIO 14 ISR ──> Ring Buffer ──> Protocol Decoder
                                                                      │
                                                (Store Decoded + RAW) │
                                                                      ▼
                                                              LittleFS Flash

[ Step 2: Transmission ]
User Click ──> REST API ──> Fetch from Flash ──> RMT Driver ──> 2N2222 ──> 940nm LEDs ──> TV/AC
```
