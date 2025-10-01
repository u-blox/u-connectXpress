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

## [3.0.0] - 2025-06-27

- Platform: NORA-W36

### Improvements
- Application: Added HTTP client (UCS_DEV_2-393)
- Network: Added `AT+USOB` (Socket Bind) command (UCS_DEV_2-1353)
- Network: Added support for Persistent Socket in `AT+USOL` and `AT+USOB` (UCS_DEV_2-1333)
- Network: Added SNTP support (UCS_DEV_2-1356)
- Security: Added `AT+USECD` (Security Certificates Details) command (UCS_DEV_2-1357)
- Wi-Fi: Added `AT+UWCL` (Wi-Fi Channel List) command (UCS_DEV_2-1177)

### Changed behavior
- Network: `AT+USOL` (Socket Listen) split into `AT+USOL` and `AT+USOB` (UCS_DEV_2-1419)
- Network: Changed response to `AT+USOPL?` (Socket Persistent List) (UCS_DEV_2-1363)
- Wi-Fi: Added more domains in `AT+UWRD` (Wi-Fi Regulatory Domains) (UCS_DEV_2-1206)
- Bluetooth: Renamed advertise commands:
  - `AT+UBTA` → `AT+UBTAL` (Legacy Enable)
  - `AT+UBTAD` → `AT+UBTADL` (Legacy Data)
  - `AT+UBTDA` → `AT+UBTAD` (Directed Advertisement)

### Fixed
- Bluetooth: Encryption not used when reconnecting to bonded device (UCS_DEV_2-1417)
- Application: Memory leak during MQTT publish (UCS_DEV_2-1429)
- Security: EAP-TLS connection failed with certificates >2048 bytes (UCS_DEV_2-812)
- Wi-Fi: Adaptivity not enabled (UCS_DEV_2-1330)
- Application: `AT+UMQPS` and `AT+UMQPB` returned OK too early (UCS_DEV_2-1362)
- Bluetooth: Module crash during SPS data transmission in buffered receive mode with `AT+USPSRM`(UCS_DEV_2-1347)
- Bluetooth: Missing support for SPS write without response and notification (UCS_DEV_2-1336)
- Wi-Fi: Wrong `authentication_suites` shown for EAP in scan results (UCS_DEV_2-1461)


> For complete changelogs, see each release’s notes in the [Releases tab](https://github.com/u-blox/u-connectXpress/releases).

---

## 📖 Documentation

- AT manual is included with each release

---

## ℹ️ About

- **This repo**: Public distribution of stable builds and documentation

