# AT Commands Changes: u-connectXpress 3.5.0 for NORA-W36 → u-connectXpress 3.6.0 for NORA-W36

This document shows the differences between **u-connectXpress 3.5.0 for NORA-W36** and **u-connectXpress 3.6.0 for NORA-W36** of the AT commands specification.

## Summary

- **Added commands:** 1
- **Removed commands:** 0
- **Renamed commands:** 0
- **Modified commands:** 3


## ✅ Added Commands

#### Wi-Fi

- **AT+UWSSET** - Wi-Fi Station Security Enterprise Tunneled


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

#### Wi-Fi

### AT+UWAPS - Wi-Fi AP Security


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPS?` | Get the current security configuration for Wi-Fi AP |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWAPS:<security_mode>,<wpa_version>` | Response if security mode is WPA |
| `+UWAPS:<security_mode>` | Response if security mode is Open |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wpa\_version | enumerator | Valid values:<br>0: WPA 2<br><br>Default value: WPA 2 |
| security\_mode | enumerator | The current security mode.<br><br>Valid values:<br>0: Open security<br><br>1: WPA security<br><br>2: EAP-TLS security<br><br>3: PEAP security<br><br>**4: EAP-TTLS security** |

### AT+UWSS - Wi-Fi Security Config

Read the current security parameter configuration, for Wi-Fi station

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSS=<wlan_handle>` | Get the current Wi-Fi station security config |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSS:<wlan_handle>,<security_mode>,<wpa_threshold>` | Response if security mode is WPA |
| `+UWSS:<wlan_handle>,<security_mode>` | Response if security mode is Open |
| `+UWSS:<wlan_handle>,<security_mode>,<ca_name>,<client_cert_name>,<client_key_name>,<identity>` | Response if security mode is EAP-TLS. Emitted when security was configured<br>using AT+UWSSE without <tls_version> (DEPRECATED). Prefer configuring with<br><tls_version> so that the +UWSS variant including <tls_version> is emitted instead |
| `+UWSS:<wlan_handle>,<security_mode>,<tls_version>,<ca_name>,<client_cert_name>,<client_key_name>,<identity>` | Response if security mode is EAP-TLS |
| `+UWSS:<wlan_handle>,<security_mode>,<username>,<ca_name>` | Response if security mode is PEAP. Emitted when security was configured<br>using AT+UWSSP without <tls_version> (DEPRECATED). Prefer configuring with<br><tls_version> so that the +UWSS variant including <tls_version> is emitted instead |
| `+UWSS:<wlan_handle>,<security_mode>,<tls_version>,<username>,<ca_name>` | Response if security mode is PEAP |
| **`+UWSS:<wlan_handle>,<security_mode>,<tls_version>,<ttls_inner_auth>,<username>,<ca_name>,<server_name>,<anonymous_identity>`** | **EAP-TTLS configuration. The password is never returned.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0..0 |
| security\_mode | enumerator | The current security mode.<br><br>Valid values:<br>0: Open security<br><br>1: WPA security<br><br>2: EAP-TLS security<br><br>3: PEAP security<br><br>**4: EAP-TTLS security** |
| wpa\_threshold | enumerator | Lowest WPA version to connect to<br><br>Valid values:<br>0: Only connect to access points that support WPA2 or up<br>1: Only connect to access points that support WPA3<br><br>Default value: 0 |
| tls\_version | enumerator | TLS version to use<br><br>Valid values:<br>0: Disable TLS<br>1: TLS 1.2<br>2: TLS 1.3<br>3: TLS 1.2 or 1.3 (negotiate highest) |
| ca\_name | string | Name of the certificate authority (CA) certificate to use<br><br>Length: 1..32 |
| client\_cert\_name | string | Name of the client certificate to use<br><br>Length: 1..32 |
| client\_key\_name | string | Name of the private key for client certificate<br><br>Length: 1..32 |
| username | string | User name for PEAP authentication.<br><br>Length: 1..31 |
| identity | string | Identity for EAP-TLS<br><br>Length: 1..31 |
| **ttls\_inner\_auth** | **enumerator** | **Inner authentication method for EAP-TTLS. No automatic fallback is performed.<br><br>**Valid values:**<br>0: MSCHAPv2<br>1: PAP** |
| **server\_name** | **string** | **Expected DNS name in the RADIUS server certificate, empty if name matching is disabled<br><br>**Length: 0..253**** |
| **anonymous\_identity** | **string** | **Anonymous outer identity, empty when not configured<br><br>**Length: 0..31**** |

