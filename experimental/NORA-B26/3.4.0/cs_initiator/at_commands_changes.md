# AT Commands Changes: u-connectXpress 3.2.0 for NORA-B26 → u-connectXpress 3.4.0 for NORA-B26

This document shows the differences between **u-connectXpress 3.2.0 for NORA-B26** and **u-connectXpress 3.4.0 for NORA-B26** of the AT commands specification.

## Summary

- **Added commands:** 5
- **Removed commands:** 2
- **Renamed commands:** 0
- **Modified commands:** 8


## ✅ Added Events

#### Channel Sounding

- **+UEBTCSS:<conn_handle>,<channel_sounding_event>,<hci_status>** - Event Bluetooth Channel Sounding Status


## ✅ Added Commands

#### Bluetooth

- **AT+UBTADE** - Bluetooth Advertising Data Extended *(replaces previous functionality)*
- **AT+UBTAES** - Bluetooth Advertisement Extended Settings
- **AT+UBTDFD** - Bluetooth Discovery Data Filter
#### Channel Sounding

- **AT+UBTCSM** - Bluetooth Channel Sounding Mode


## ❌ Removed Commands

#### Bluetooth

- **AT+UBTADE** - Bluetooth Advertising Data Extended *(functionality replaced by new version)*
- **AT+UBTSS2** - Bluetooth Scan Directed Advertisements


## 🔄 Modified Commands

#### Bluetooth

### AT+UBTADL - Bluetooth Advertisement Data Legacy

['Command for setting custom legacy advertise data **and advertiser type** in Bluetooth low ~~energy. Maximum~~ **energy', 'the maximum length** of **custom advertise data depends on advertiser type,** 28 ~~bytes.', 'Any~~ **bytes for connectable advertisers and 31 bytes for none-connectable.', 'For connectable advertiser (with adv_type == 0), any** custom advertising data will be appended to the default mandatory flags field.', **'it is optional to provide advertiser type. If omitted, the advertiser type is connectable and scannable (0)',** 'Note that the AT command AT+UBTD supports scan modes that can be used to see the complete advertising data.', 'This is useful when testing the advertise data set with the AT+UBTALD. By default, the service UUID for the u-blox Serial Port Service is part of the advertising data.']

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTADL=<adv_data>`~~ | ~~Write custom advertising data.~~ |
| `AT+UBTADL?` | Read custom advertising data and advertiser type. |
| **`AT+UBTADL=<adv_data>[,<adv_type>]`** | **Write custom advertising data and advertiser type.<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTADL:<adv_data>`~~ | ~~Successful read response.~~ |
| **`+UBTADL:<adv_data>,<adv_type>`** | **Successful read response.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| adv\_data | byte_array | Length: ~~3..28~~**3..31** |
| **adv\_type** | **enumerator** | **type of legacy advertisement<br><br>**Valid values:**<br>0: Connectable and Scannable<br>1: Non-Connectable Scannable<br>2: Non-Connectable Non-Scannable<br><br>**Default value: 0**** |

### AT+UBTAL - Bluetooth Advertise Legacy Enable

Start legacy advertisement if not started

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAL` | Start legacy advertisement if not started.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| **`AT+UBTAL=<max_connection>`** | **Start legacy advertisement if not started with setting the maximum peripheral connections.<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| **max\_connection** | **integer** | ****Valid values: 1..2**** |

### AT+UBTBGD - Bluetooth Background Discovery

Start a background discovery. Use ~~together with AT+UBTSS2~~ **AT+UBTSS to configure the device** to connect to directed advertisements during scanning. If only interested in connecting to directed advertisements, use ~~AT+UBTSS2~~**AT+UBTSS** together with output_events **disabled** to not output discovery events.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTBGD` | Start background discovery |
| `AT+UBTBGD=<discovery_type>[,<discovery_mode>[,<output_events>]]` | Start background discovery |
| **`AT+UBTBGD?`** | **Read background discovery configuration.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTBGD:<discovery_state>` | Successful read response when background discovery is not active. |
| `+UBTBGD:<discovery_state>,<discovery_type>,<discovery_mode>,<output_events>,<connect_to_directed_advertisements>` | Successful read response when background discovery is active. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| discovery\_type | enumerator | Valid values:<br>0: ~~All with no filter.~~ Displays all found devices; devices can be displayed multiple times.<br>1: ~~General inquiry.~~ Displays ~~devices in General or Limited discoverability mode;~~ **all found devices;** each device is displayed only **once.<br>2: Filter discovery results using the configured data filters. Only devices matching a data filter configured with ${ref:AT+UBTDFD} will be reported. Devices can be displayed multiple times.<br>3: Filter discovery results using the configured data filters. Only devices matching a data filter configured with ${ref:AT+UBTDFD} will be reported. Each device is displayed only** once. |
| discovery\_mode | enumerator | Valid values:<br>0: Active discovery.<br>1: Passive, no scan response data will be received.<br><br>Default value: 0 |
| output\_events | enumerator | Valid values:<br>0: Disable output events during background discovery<br>1: Enable output events during background discovery |
| **discovery\_state** | **enumerator** | ****Valid values:**<br>0: Background discovery is not active<br>1: Background discovery is active** |
| **connect\_to\_directed\_advertisements** | **enumerator** | ****Valid values:**<br>0: Connect to directed advertisements during background discovery disabled<br>1: Connect to directed advertisements during background discovery enabled** |

### AT+UBTD - Bluetooth Discovery

Performs a discovery procedure to find any advertising devices in the vicinity.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTD` | Start discovery using default parameters |
| `AT+UBTD=<discovery_type>[,<discovery_mode>[,<discovery_length>]]` | Start discovery. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTD:<bd_addr>,<rssi>,<device_name>,<data_type>,<data>` | This response is sent for every found device. If no name is found, <device_name> is an empty string, if <mode> is set to Active, both Scan responses and Advertisements will be shown. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd_addr | Bluetooth device address of the remote device. |
| rssi | integer | Received signal strength in dBm. |
| device\_name | string | Name of the discovered device. |
| data\_type | enumerator | Type of advertising data received.<br><br>Valid values:<br>0: Scan response data.<br>1: Advertise data.<br>2: Extended advertise data. |
| data | byte_array | Complete advertise/scan response data received from the remote device. |
| discovery\_type | enumerator | Valid values:<br>0: ~~All with no filter.~~ Displays all found devices; devices can be displayed multiple times.<br>1: ~~General inquiry.~~ Displays ~~devices in General or Limited discoverability mode;~~ **all found devices;** each device is displayed only **once.<br>2: Filter discovery results using the configured data filters. Only devices matching a data filter configured with ${ref:AT+UBTDFD} will be reported. Devices can be displayed multiple times.<br>3: Filter discovery results using the configured data filters. Only devices matching a data filter configured with ${ref:AT+UBTDFD} will be reported. Each device is displayed only** once. |
| discovery\_mode | enumerator | Valid values:<br>0: Active discovery.<br>1: Passive, no scan response data will be received.<br><br>Default value: 0 |
| discovery\_length | integer | Timeout measured in milliseconds. Time range: 10 ms - 40 s<br><br>Valid values: 10..40000<br><br>Default value: 5000 |

### AT+UBTP - Bluetooth Persistent


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTP=<bd_addr>,<connect_sps>` | ['Configure an ACL link with automatic re-connection. As opposed to AT+UBTC, this command will not initiate a connection directly but is used for storing a connection configuration persistently so that the link is automatically setup on boot.']<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTP:<config_id>` | Successful write response, returning a configuration id identifying the configuration |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd_addr | Bluetooth device address of the remote device. |
| config\_id | integer | Configuration id<br><br>Valid values: 200..200 |
| connect\_sps | integer | Should start a SPS connection when ACL link is up.<br>Integer Boolean flag  0 = No, 1 = Yes<br><br>Valid values: 0..1 |

### AT+UBTPL - Bluetooth Persistent List

List all configured persistent bluetooth connections

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTPL?` | List the currently configured Persistent Bluetooth Connections |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTPL:<config_id>,<bd_addr>,<connect_sps>` | Successful read response |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd_addr | Bluetooth device address of the remote device. |
| config\_id | integer | Configuration id<br><br>Valid values: 200..200 |
| connect\_sps | integer | Should start a SPS connection when ACL link is up.<br>Integer Boolean flag  0 = No, 1 = Yes<br><br>Valid values: 0..1 |

### AT+UBTSS - Bluetooth Scan Settings

Get and Set Scan Settings.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTSS0=<scan_interval>` | Write scan interval. |
| `AT+UBTSS0?` | Read scan Interval. |
| `AT+UBTSS1=<scan_window>` | Write scan window. |
| `AT+UBTSS1?` | Read scan Interval. |
| `AT+UBTSS?` | Read all scanning parameter setting values. |
| **`AT+UBTSS2=<connect_to_directed_adv>`** | **Enable or disable connecting to directed advertisements during scanning.<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |
| **`AT+UBTSS2?`** | **Read connect to directed advertisements setting.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTSS0:<scan_interval>` | Successful read of scan interval. |
| `+UBTSS1:<scan_window>` | Successful read of scan window. |
| `+UBTSS:<scan_param>,<value>` | Successful read response for AT+UBTSS?. |
| **`+UBTSS2:<connect_to_directed_adv>`** | **Successful read response.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| scan\_interval | integer | Scan interval (must be >= Scan window. <br>Default: 160.<br>Calculation: scan_interval * 0.625 ms)<br><br>Valid values: 16..16384<br><br>Default value: 160 |
| scan\_window | integer | Scan window (must be <= Scan interval. <br>Default: 128.<br>Calculation: scan_interval * 0.625 ms)<br><br>Valid values: 16..16384<br><br>Default value: 128 |
| value | integer | Value of scan parameter.<br><br>Valid values: 0..65535 |
| scan\_param | enumerator | Scan parameter.<br><br>Valid values:<br>0: Scan interval.<br><br>1: Scan window.<br><br>**2: Connect to directed advertisements during scanning.** |
| **connect\_to\_directed\_adv** | **integer** | **Enable (1) or disable (0) connecting to directed advertisements during scanning. Default: 0.<br><br>**Valid values: 0..1**<br><br>**Default value: 0**** |

#### System

### AT+USYUS - Uart Settings


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYUS=<baud_rate>[,<flow_control>[,<change_after_confirm>]]` | Configure new UART settings that will be used after restart. Baudrates above 4000000 bps can be set, but are unsupported. If the flow_control parameter is omitted then no flow control will be used. If change_after_confirm is not provided the baudrate will be changed only after a store and reboot.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USYUS?` | Reads current UART settings from the module |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USYUS:<baud_rate>,<flow_control>` | Successful read response |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200,2400,4800,9600,14400,28800,31250,38400,56000,57600,76800,115200,230400,250000,460800,921600,1000000<br><br>Default value: U_CONFIG_DEFAULT_BAUDRATE |
| flow\_control | integer | 0: **(Factory default)** No flow control<br>1: Use CTS/RTS flow control<br><br>Valid values: 0..1 |
| change\_after\_confirm | integer | 0: Switch baudrate after reboot. When set AT&W must be called.<br>1: Switch baudrate directly after status OK have been sent.<br><br>Valid values: 0..1 |

