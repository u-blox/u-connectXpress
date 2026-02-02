# Changelog

All notable changes to the u-connectXpress software relevant for `NORA-B27` will be documented in this file. For added or changed AT commands see at_commands_changes.md

# [3.3.0] - 2026-01-20
### Improvements
- First release of uConnectXpress for NORA-B27

### Changed behavior

### Fixed

### Known limitations
- Bluetooth: GATT read/write with authentication fails if bond not pre-established (UCS_DEV_2-851)
- System: Partial escape sequence never timeout. If you, in transparent mode, send a message that contains part of the escape sequence for leaving transparent mode, such as ++, this will not be transmitted to peer until yet another character is sent. (UCS_DEV_2-1490)
- SPS: Some SPS data sent in persistent mode will be lost when remote disconnects. Data sent over a persistent SPS link after the remote device stops acking BLE data until local device receives a BLE disconnect will be  lost. The window of lost data will be the BLE supervision timeout if for example the remote device is reset. (UCS_DEV_2-1487)
- Bluetooth: The longest advertisement data for extended advertisement is limited to 226 bytes. (UCS_DEV_2-1471)
- Bluetooth: Only one advertisement can by activated at the same time (UCS_DEV_2-1470)

---

