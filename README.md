# 📦 u-connectXpress Releases

This repository is dedicated to **releases of u-connectXpress** — binaries, manuals, and changelogs for each supported platform.
The source code lives in a private repository.

---

## 🔖 Latest Release

[![GitHub release](https://img.shields.io/github/v/release/u-blox/u-connectXpress?sort=semver)](https://github.com/u-blox/u-connectXpress/releases/latest)

**Download the latest release assets here:**
[Releases page](https://github.com/u-blox/u-connectXpress/releases/latest)

---

## 📜 Recent Release Notes

# [3.1.0] - 2025-09-28

- Platform: NORA-W36

### Improvements
- Bluetooth: Support up to 23 characteristics with notification, indication (UCS_DEV_2-1529)
- Security: Support for TLS 1.3 added
- Security: Mbed TLS upgraded to version 3.6.4
    Note! Server Name Identification is now enforced by default during Server Authentication, even for TLS 1.2. This may cause problems if using an old certificate without the server name included. See AT+USETE0 for how to turn this off.
- MQTT: `AT+UMQRB` MQTT Read Binary now supports reading up to 5000 bytes (UCS_DEV_2-1460)

### Fixed
- HTTP client: Get Body feature not working with TLS and string mode (UCS_DEV_2-1509)
- HTTP client: Fixed POST truncation between requests by resetting contentLength after request completion (UCS_DEV_2-1524)
- Bluetooth: Crash if >8 characteristics used on one GATT service (UCS_DEV_2-1468)
- System: Escape sequence not working after AT+USYUS (UCS_DEV_2-1469)
- System: Escape sequence (+++) leaks as payload (UCS_DEV_2-1489)

## [3.0.1] 2025-08-13

- Platform: NORA-B26

### Improvements
- First release of uConnectXpress for NORA-B26

### Fixed
- System: Escape sequence not working after AT+USYUS (UCS_DEV_2-1469)
- System: Escape sequence (+++) leaks as payload (UCS_DEV_2-1489)

### Known limitations
- Bluetooth: GATT read/write with authentication fails if bond not pre-established (UCS_DEV_2-851)
- System: Partial escape sequence never timeout. If you, in transparent mode, send a message that contains part of the escape sequence for leaving transparent mode, such as ++, this will not be transmitted to peer until yet another character is sent. (UCS_DEV_2-1490)
- SPS: Some SPS data sent in persistent mode will be lost when remote disconnects. Data sent over a persistent SPS link after the remote device stops acking BLE data until local device receives a BLE disconnect will be  lost. The window of lost data will be the BLE supervision timeout if for example the remote device is reset. (UCS_DEV_2-1487)
- Bluetooth: The longest advertisement data for extended advertisement is limited to 226 bytes. (UCS_DEV_2-1471)
- Bluetooth: Only one advertisement can by activated at the same time (UCS_DEV_2-1470)

> For complete changelogs, see each release’s notes in the [Releases tab](https://github.com/u-blox/u-connectXpress/releases).

---

## 📖 Documentation

- AT manual is included with each release

---

## ℹ️ About

- **This repo**: Public distribution of stable builds and documentation

