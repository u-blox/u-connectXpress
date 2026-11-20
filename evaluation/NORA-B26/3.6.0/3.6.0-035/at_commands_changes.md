# AT Commands Changes: u-connectXpress 3.5.1 for NORA-B26 → u-connectXpress 3.6.0 for NORA-B26

This document shows the differences between **u-connectXpress 3.5.1 for NORA-B26** and **u-connectXpress 3.6.0 for NORA-B26** of the AT commands specification.

## Summary

- **Added commands:** 1
- **Removed commands:** 0
- **Renamed commands:** 0
- **Modified commands:** 3


## ✅ Added Commands

#### Bluetooth

- **AT+UBTFPK** - Fixed BLE passkey


## 🔄 Modified Commands

#### Bluetooth

### AT+UBTALS - Bluetooth Advertisement Legacy Settings

Get and Set Advertisement Legacy Settings.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTALS=<advertisement_interval_minimum>,<advertisement_interval_maximum>` | Configure advertisement parameters for legacy advertisements<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTALS?` | Read advertisement parameters for legacy advertisements |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTALS:<advertisement_interval_minimum>,<advertisement_interval_maximum>` | Successful read of advertisement configuration. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| advertisement\_interval\_minimum | integer | Advertising interval minimum (must be <= Advertising interval maximum. <br>Default: 1600.<br>Calculation: advertisement_interval_minimum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 1600 |
| advertisement\_interval\_maximum | integer | Advertising interval maximum (must be >= Advertising interval minimum. <br>Default: 2000.<br>Calculation: advertisement_interval_maximum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 2000 |

### AT+UBTCST - Bluetooth Connection Status

Read negotiated properties of a Bluetooth low energy ACL connection. Some of the properties are a result of negotiation when a ~~connections~~**connection** is set up, and this command gives the possibility to see what properties the connection actually uses.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCST=<conn_handle>` | Read all properties of an existing Bluetooth low energy ACL connection. |
| `AT+UBTCST=<conn_handle>,<prop_id>` | Read a specific property of an existing Bluetooth low energy ACL connection. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTCST:<prop_id>,<status_val>` | Successful read response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| status\_val | integer | Value of the preceding property. |
| prop\_id | enumerator | Valid values:<br>0: Connection interval used on this connection. Range: 6 to 3200 Time = status_val * 1.25 ms Time range: 7.5 ms to 4000 ms <br>1: Peripheral latency for the connection in number of connection events. Range: 0 to 499<br>2: Supervision timeout (in ms) for this ~~connections~~**connection**. Range: 100 ms to 32000 ms<br>3: MTU size for this ~~connections.<br>4~~**connection.<br>4**: Data Channel TX PDU Payload Length.<br>5: Data Channel RX PDU Payload Length.<br>6: Data Length Extension state. 0: Data Length Extension Off \ 1: Data Length Extension On<br>7: Local role in this connection. 1: Low Energy Central \ 2: Low Energy Peripheral<br>8: TX Phy used in this connection Bit 0: 1 Mbps Bit 1: 2 Mbps Bit 2: Coded <br>9: RX Phy used in this connection Bit 0: 1 Mbps Bit 1: 2 Mbps Bit 2: Coded |

### AT+UBTSS - Bluetooth Scan Settings

Get and Set Scan Settings.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTSS0=<scan_interval>` | Write scan interval.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTSS0?` | Read scan Interval. |
| `AT+UBTSS1=<scan_window>` | Write scan window.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTSS1?` | Read scan Interval. |
| `AT+UBTSS2=<connect_to_directed_adv>` | Enable or disable connecting to directed advertisements during scanning.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTSS2?` | Read connect to directed advertisements setting. |
| `AT+UBTSS?` | Read all scanning parameter setting values. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTSS0:<scan_interval>` | Successful read of scan interval. |
| `+UBTSS1:<scan_window>` | Successful read of scan window. |
| `+UBTSS2:<connect_to_directed_adv>` | Successful read response. |
| `+UBTSS:<scan_param>,<value>` | Successful read response for AT+UBTSS?. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| scan\_interval | integer | Scan interval (must be >= Scan window. <br>Default: 160.<br>Calculation: scan_interval * 0.625 ms)<br><br>Valid values: 16..16384<br><br>Default value: 160 |
| scan\_window | integer | Scan window (must be <= Scan interval. <br>Default: 128.<br>Calculation: scan_interval * 0.625 ms)<br><br>Valid values: 16..16384<br><br>Default value: 128 |
| value | integer | Value of scan parameter.<br><br>Valid values: 0..65535 |
| connect\_to\_directed\_adv | integer | Enable (1) or disable (0) connecting to directed advertisements during scanning. Default: 0.<br><br>Valid values: 0..1<br><br>Default value: 0 |
| scan\_param | enumerator | Scan parameter.<br><br>Valid values:<br>0: Scan interval.<br>1: Scan window.<br>2: Connect to directed advertisements during scanning. |

