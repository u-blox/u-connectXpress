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

## [1.2.0] - 2024-10-18
### Improvements
- Wi-Fi: Roaming between Wi-Fi access points based-on Received Signal Strength Indicator, RSSI.
- Application: Auto sleep mode for optimizing consumption depending on configuration and activity.

### Fixed
- Could accept unauthenticated bonding even when configured to demand authenticated bonding (UCS_DEV_2-1067)
- Ping fails if sent both from the module and to the module at the same time (UCS_DEV_2-1075)
- Wi-Fi station could end up with the wrong color LED if disconnect was sent during an ongoing connection attempt (UCS_DEV_2-1133)
- Throughput reduced over time when sending data in one direction over a TCP socket (UCS_DEV_2-1127)
- Module crashes during automatic reconnect to a Wi-Fi Access Point (UCS_DEV_2-1130)

## [1.0.0] - 2024-05-15
- Platform: NORA-W36
### Improvements
- NORA-W36 introduced
### Known limitations
- Wi-Fi: Crash may occur when AP is brought down while station is associating (UCS_DEV_2-595)
- Security: EAP-TLS fails with certificates >2048 bytes (UCS_DEV_2-812)
- Network: TCP “No Delay” feature reduces throughput (UCS_DEV_2-833)
- Bluetooth: GATT read/write with authentication fails if bond not pre-established (UCS_DEV_2-851)


> For complete changelogs, see each release’s notes in the [Releases tab](https://github.com/u-blox/u-connectXpress/releases).

---

## 📖 Documentation

- AT manual is included with each release

---

## ℹ️ About

- **This repo**: Public distribution of stable builds and documentation

