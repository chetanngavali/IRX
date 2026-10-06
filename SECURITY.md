# Security Policy — IRX

## 1. Scope & Security Boundaries

IRX is an embedded infrared device operating inside local home and office networks.

### Explicit Security Controls:
- **No Automotive / Access Control**: The software strictly avoids vehicle key cloning, immobilizer circumvention, and rolling-code access control protocols.
- **Local Network Isolation**: The device does not connect to external third-party cloud infrastructure or send telemetry data.
- **Standalone Mode**: By default, the device acts as a private, isolated Access Point protected with WPA2 passphrase authentication.

---

## 2. Reporting a Vulnerability

If you discover a potential vulnerability in the IRX firmware, web application, or API:

1. **Do not create a public issue**.
2. Email details to the project maintainers with subject line `[SECURITY] IRX Vulnerability Report`.
3. Provide reproduction steps, affected firmware version, and target hardware configuration.
4. We aim to acknowledge receipt within 48 hours and provide patches within 14 days.
