# Changelog

All notable changes to the u-connectXpress software relevant for `NORA-B27` will be documented in this file. This includes new features, behavior changes, bug fixes, and known limitations that may impact users.
For a detailed list of added or changed AT commands see at_commands_changes.md
This project adheres to Semantic Versioning (MAJOR.MINOR.PATCH).

# [3.5.0] - 2026-10-13
### Improvements
- System: The Host Wakeup pin can be set to indicate the transparent-mode connection status with `AT+USYHWP`.
### Changed behavior
### Fixed
- System: At high socket throughput, URCs could come out cut in half (for example `+UESODS`), resulting in lost payload bytes on the host
- SPS: A client with flow control now waits for the server's credit notification.
- SPS: Fixed an assert when a disconnect happens while the credit timer runs.
- SPS: Fixed an overflow in the credit calculation.
- Bluetooth: An MTU exchange that arrived early could leave SPS at MTU 23, which lowered throughput.
- Bluetooth: Fixed a race while ATT was being torn down

### Known limitations
- Bluetooth: GATT read/write with authentication fails if bond not pre-established (UCS_DEV_2-851)
- System: Partial escape sequence never timeout. If you, in transparent mode, send a message that contains part of the escape sequence for leaving transparent mode, such as ++, this will not be transmitted to peer until yet another character is sent. (UCS_DEV_2-1490)
- SPS: Some SPS data sent in persistent mode will be lost when remote disconnects. Data sent over a persistent SPS link after the remote device stops acking BLE data until local device receives a BLE disconnect will be  lost. The window of lost data will be the BLE supervision timeout if for example the remote device is reset. (UCS_DEV_2-1487)
- Bluetooth: The longest advertisement data for extended advertisement is limited to 226 bytes. (UCS_DEV_2-1471)
- Bluetooth: Only one advertisement can be activated at the same time (UCS_DEV_2-1470)


---

# [3.4.0] - 2026-04-10
### Improvements
- Bluetooth: Added AT+UBTAES to set advertising interval for extended advertisements (UCS_DEV_2-1644)
- Bluetooth: Return identity address immediately after it is available for privacy peers (UCS_DEV_2-1351)
- Bluetooth: Added non-connectable advertisement support in AT+UBTADL (UCS_DEV_2-1149)
- Bluetooth: Added non-connectable advertisement support in AT+UBTADE (UCS_DEV_2-1658)
### Changed behavior
### Fixed

### Known limitations
- Bluetooth: GATT read/write with authentication fails if bond not pre-established (UCS_DEV_2-851)
- System: Partial escape sequence never timeout. If you, in transparent mode, send a message that contains part of the escape sequence for leaving transparent mode, such as ++, this will not be transmitted to peer until yet another character is sent. (UCS_DEV_2-1490)
- SPS: Some SPS data sent in persistent mode will be lost when remote disconnects. Data sent over a persistent SPS link after the remote device stops acking BLE data until local device receives a BLE disconnect will be  lost. The window of lost data will be the BLE supervision timeout if for example the remote device is reset. (UCS_DEV_2-1487)
- Bluetooth: The longest advertisement data for extended advertisement is limited to 226 bytes. (UCS_DEV_2-1471)
- Bluetooth: Only one advertisement can be activated at the same time (UCS_DEV_2-1470)


---

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
- Bluetooth: Only one advertisement can be activated at the same time (UCS_DEV_2-1470)

---

