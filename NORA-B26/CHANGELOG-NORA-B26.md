# Changelog

All notable changes to the u-connectXpress software relevant for `NORA-B26` will be documented in this file. For added or changed AT commands see at_commands_changes.md


# [3.2.0] - 2025-12-19
### Improvements
- Bluetooth: Added `AT+UBTSS2` command to configure automatic connection to directed advertisements during scanning (UCS_DEV_2-1327)
- Bluetooth: Added new AT command for setting max output power `AT+UBTMOP` (UCS_DEV_2-1074)
- System: Added `AT+USCT` to read out chip temperature (UCS_DEV_2-1550)

### Changed behavior
- Bluetooth: Max number of bonded devices set to 30, oldest one dropped if a new bond is initiated when full  (UCS_DEV_2-1553)
- Bluetooth: `AT+UBTBGD` (Background Discovery) now supports configurable discovery type, mode, and output events parameters, enabling true background scanning instead of just directed advertisement connection (UCS_DEV_2-1327)
- Deep Sleep: `AT+UPMDS=0` now only enables wakeup from module wakeup pin instead of also UART RX, wakeup from UART RX moved to a new `wakeup_mode` `AT+UPMDS=2`.
- System: Upgrading to version 3.2.0 from previous versions will automatically factory restore the device due to internal storage changes. All stored settings and Bluetooth bonding information will be lost. Users should document their current configuration before upgrading.

### Fixed
- Reconnecting to a bonded device when having +UBTBSM mode 0 did not output a +UEBTC event. (UCS_DEV_2-1534, UCS_DEV_2-1535)
- UART framing error resulted in stopped UART reception (UCS_DEV_2-1563)
- System: Missing OK for AT+CPWROFF command when AT echo is turned off (UCS_DEV_2-1569)

### Known limitations
- Bluetooth: GATT read/write with authentication fails if bond not pre-established (UCS_DEV_2-851)
- System: Partial escape sequence never timeout. If you, in transparent mode, send a message that contains part of the escape sequence for leaving transparent mode, such as ++, this will not be transmitted to peer until yet another character is sent. (UCS_DEV_2-1490)
- SPS: Some SPS data sent in persistent mode will be lost when remote disconnects. Data sent over a persistent SPS link after the remote device stops acking BLE data until local device receives a BLE disconnect will be  lost. The window of lost data will be the BLE supervision timeout if for example the remote device is reset. (UCS_DEV_2-1487)
- Bluetooth: The longest advertisement data for extended advertisement is limited to 226 bytes. (UCS_DEV_2-1471)
- Bluetooth: Only one advertisement can by activated at the same time (UCS_DEV_2-1470)


---
## [3.0.1] 2025-08-13
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

---

