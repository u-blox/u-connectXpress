# AT Commands Changes: u-connectXpress 3.5.1 for NORA-W36 → u-connectXpress 3.6.0 for NORA-W36

This document shows the differences between **u-connectXpress 3.5.1 for NORA-W36** and **u-connectXpress 3.6.0 for NORA-W36** of the AT commands specification.

## Summary

- **Added commands:** 4
- **Removed commands:** 1
- **Renamed commands:** 1
- **Modified commands:** 9


## ✅ Added Events

#### Diagnostics

- **+UEDGIC:\<protocol_type\>,\<role\>,\<iperf_status\>,\<transferred\>,\<duration\>,\<throughput\>** - Event Iperf Complete


## ✅ Added Commands

#### Bluetooth

- **AT+UBTFPK** - Fixed BLE passkey
#### HTTP

- **AT+UHTCFRE** - HTTP Client Follow Redirect Enable/Disable
#### Wi-Fi

- **AT+UWSSET** - Wi-Fi Station Security Enterprise Tunneled


## ❌ Removed Events

#### Diagnostics

- **+UEDGI:\<iperf_output\>** - Event Iperf output


## 🔄 Renamed Commands

#### Socket

- **+UESOIC:\<socket_handle\>,\<remote_ip\>,\<listening_socket_handle\>** - 'Event Socket Incoming Connection' has been renamed to **+UESOIC:\<listening_socket_handle\>,\<remote_ip\>,\<socket_handle\>** - 'Event Socket Incoming Connection'


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

#### Diagnostics

### AT+UDGI - Diagnostics Iperf


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UDGI=<iperf_action>,<protocol_type>[,<role>,<port>,<report_interval>[,<time_boundary>,<ip_addr>[,<length>[,<bandwidth>[,<bidirectional>]]]]]` | Start/stop IPERF 2 server/client |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| iperf\_action | enumerator | Action<br><br>Valid values:<br>1: Start iperf<br>2: Stop iperf |
| protocol\_type | enumerator | IP protocol<br><br>Valid values:<br>1: TCP<br>2: UDP |
| role | enumerator | Role<br><br>Valid values:<br>1: Server<br>2: Client |
| port | integer | ~~Port~~ **Port. 0 selects 5001.** |
| report\_interval | integer | ~~Report interval~~ **Interval reports are not supported, ignored.** |
| time\_boundary | integer | ~~Time boundary.~~ **Test time in seconds, 0 for 10 seconds.** Client only. Ignored if role is server |
| ip\_addr | ip_addr | IP address to connect to. Client only. Ignored if role is server |
| bandwidth | integer | Bandwidth to be used for ~~UDP~~ **UDP. Not supported, ignored.** |
| length | integer | Size of packets.<br><br>Valid values: 1..1460<br><br>Default value: 1460 |
| bidirectional | enumerator | Bidirectional flag. Client only. Ignored if role is server<br><br>Valid values:<br>0: False<br><br>~~1: On~~<br>~~When starting bidirectional TCP test, start a server on both tester and DUT, then start a client with bidirectional flag on the DUT.~~<br>~~If doing bidirectional UDP test, start a server on both DUT and tester and then start a client with a bidirectional flag on both.~~<br>**1: On. Not supported, the command returns ERROR.** |

#### HTTP

### AT+UHTCDC - HTTP Client Disconnect


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UHTCDC=<session_id>` | Disconnects the HTTP session identified by `<session_id>`.<br>Also cancels a redirect that is being followed. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| session\_id | integer | Unique http session identifier. Currently only one session is supported, 0.<br><br>Valid values: 0..0 |

#### Wi-Fi

### AT+UWAPCP - Wi-Fi AP Connection Parameters


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UWAPCP=<ssid>[,<channel>]`~~ | ~~Sets connection parameters for the AP configuration~~ |
| `AT+UWAPCP?` | Read the current connection parameters |
| **`AT+UWAPCP=<ssid>[,<channel>[,<hidden_ssid>]]`** | **Sets connection parameters for the AP configuration<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UWAPCP:<ssid>,<channel>`~~ | ~~Successful read response~~ |
| **`+UWAPCP:<ssid>,<channel>,<hidden_ssid>`** | **Successful read response** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| channel | enumerator | channel<br><br>Valid values:<br>1: 1<br>2: 2<br>3: 3<br>4: 4<br>5: 5<br>6: 6<br>7: 7<br>8: 8<br>9: 9<br>10: 10<br>11: 11<br>36: 36<br>40: 40<br>44: 44<br>48: 48<br><br>Default value: 6 |
| ssid | string | SSID<br><br>Length: ~~0..32~~~~**1..32**<br><br>Length: ~~0..32~~**1..32** |
| **hidden\_ssid** | **integer** | **Hide the SSID of the access point.<br>0: The SSID is included in beacons and broadcast probe responses<br>1: The SSID is left out. Stations must know the SSID to find and connect to the access point<br>Left out: 0 (visible)<br><br>**Valid values: 0..1**<br><br>**Default value: 0**** |

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



## 🔄 Modified Events

#### HTTP

### +UEHTCRS:\<session_id\>,\<status_code\>,\<description\> - Event HTTP Client Request Status

Response status from the latest HTTP request. **For an automatically followed redirect chain, this reports only the final response.**

