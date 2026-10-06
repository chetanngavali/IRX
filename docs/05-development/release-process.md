# Release Process — IRX

This document outlines the standard release lifecycle for building, testing, and publishing new IRX releases.

---

## 1. Release Lifecycle Stages

```text
[ 1. Private Dev ] ──> [ 2. Hardware EVT ] ──> [ 3. Build Binaries ] ──> [ 4. Checksums ] ──> [ 5. GitHub Release ]
   (IRX-PRIVATE)         (Pass 11 Tests)         (firmware.bin)           (SHA256)           (Tagged vX.Y.Z)
```

1. **Development & Bugfixes**:
   - Completed inside the private source tree (`IRX-PRIVATE/`).
2. **Hardware Engineering Verification**:
   - Firmware tested on physical test benches against reference TVs and ACs.
3. **Artifact Compilation**:
   - Official production binaries compiled via PlatformIO:
     - `bootloader.bin`
     - `partitions.bin`
     - `IRX-vX.Y.Z.bin`
     - `IRX-vX.Y.Z-littlefs.bin`
4. **Cryptographic Checksumming**:
   - Generation of `SHA256SUMS.txt` matching all release binaries.
5. **Public Release Tag**:
   - Tagged release created on GitHub with change notes and attached binary archives.
