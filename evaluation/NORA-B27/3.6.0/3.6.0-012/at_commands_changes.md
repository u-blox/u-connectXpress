# AT Commands Changes: u-connectXpress 3.5.0 for NORA-B27 → u-connectXpress 3.6.0 for NORA-B27

This document shows the differences between **u-connectXpress 3.5.0 for NORA-B27** and **u-connectXpress 3.6.0 for NORA-B27** of the AT commands specification.

## Summary

- **Added commands:** 0
- **Removed commands:** 0
- **Renamed commands:** 0
- **Modified commands:** 1


## 🔄 Modified Commands

#### Bluetooth

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

