# AT Commands Changes: u-connectXpress 3.0.1 for NORA-B26 → u-connectXpress 3.2.0 for NORA-B26

This document shows the differences between **u-connectXpress 3.0.1 for NORA-B26** and **u-connectXpress 3.2.0 for NORA-B26** of the AT commands specification.

## Summary

- **Added commands:** 10
- **Removed commands:** 3
- **Renamed commands:** 0
- **Modified commands:** 36


## ✅ Added Events

#### Bluetooth

- **+UEBTBGD:<bd_addr>,<rssi>,<device_name>,<data_type>,<data>** - Event Bluetooth Background Discovery
#### General

- **+STARTUP** - Startup indication


## ✅ Added Commands

#### Bluetooth

- **AT+UBTADL** - Bluetooth Advertisement Data Legacy *(replaces previous functionality)*
- **AT+UBTBGD** - Bluetooth Background Discovery *(replaces previous functionality)*
- **AT+UBTBGDS** - Bluetooth Background Discovery Stop
- **AT+UBTMOP** - Bluetooth Max Output Power
- **AT+UBTMOPC** - Bluetooth Max Output Power Clear
- **AT+UBTSS2** - Bluetooth Scan Directed Advertisements
#### Power

- **AT+UPMS** - Power Management Sleep
#### System

- **AT+USCT** - Chip Die Temperature


## ❌ Removed Commands

#### Bluetooth

- **AT+UBTADL** - Bluetooth Advertisement Data Legacy *(functionality replaced by new version)*
- **AT+UBTBGD** - Bluetooth Background Discovery *(functionality replaced by new version)*
#### System

- **AT+USYTU** - Set/Get system time in unix time format


## 🔄 Modified Commands

#### Bluetooth

### AT+UBTA - ~~Read which advertisments are currently running~~ **Read which advertisements are currently running**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTA?` | Read the current advertisements |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTA:<legacy_advertisement>,<directed_advertisement>,<enabled_extended_advertisements>`~~ | ~~Successful read~~ |
| **`+UBTA:<legacy_adv>,<directed_adv>,<extended_adv_list>`** | **Successful read** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~legacy\_advertisement~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Legacy Advertisement Not Running<br>1: Legacy Advertisement Running~~ |
| ~~directed\_advertisement~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Directed Advertisement Not Running<br>1: Directed Advertisement Running~~ |
| ~~enabled\_extended\_advertisements~~ | ~~int_list~~ | ~~**Length: 0..1**~~ |
| **legacy\_adv** | **enumerator** | ****Valid values:**<br>0: Legacy Advertisement Not Running<br>1: Legacy Advertisement Running** |
| **directed\_adv** | **enumerator** | ****Valid values:**<br>0: Directed Advertisement Not Running<br>1: Directed Advertisement Running** |
| **extended\_adv\_list** | **int_list** | **List of indexes currently being used for extended advertisements<br><br>**Length: 0..1**** |

### AT+UBTADEC - Bluetooth Advertising Data Extended Clear

Clear the custom extended advertise data, i.e. use to the default value during extended advertising

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADEC=<index>` | Clear the extended advertise data for the specified index. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| index | integer | Valid values: 0..0 |

### AT+UBTADLC - Bluetooth Advertising Data Legacy Clear

Clear the custom advertise data, i.e.use the default value when advertising

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADLC` | Clear the custom legacy advertise data. |

### AT+UBTAE - Bluetooth Advertise Extended

Start extended advertisement for the specified configuration

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAE=<indexes_to_advertise>` | Start advertisements for the specified index(es).<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| indexes\_to\_advertise | int_list | Length: 1..2 |

### AT+UBTAL - Bluetooth Advertise Legacy Enable

Start legacy ~~advertisements~~**advertisement** if not started

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAL` | Start legacy advertisement if not started.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

### AT+UBTALD - Bluetooth Advertise Legacy Disable

Stop legacy advertisement if started

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTALD` | Stop legacy advertisement if started.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

### AT+UBTALS - Bluetooth Advertisement Legacy Settings

Get and Set Advertisement Legacy Settings.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTALS=<advertisement_interval_minimum>,<advertisement_interval_maximum>` | Configure advertisement parameters for legacy advertisements |
| `AT+UBTALS?` | Read advertisement parameters for legacy advertisements |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTALS:<advertisement_interval_minimum>,<advertisement_interval_maximum>` | Successful read of advertisement configuration. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| advertisement\_interval\_minimum | integer | Advertising interval minimum (must be <= Advertising interval maximum. <br>Default: 1600.<br>Calculation: advertisement_interval_minimum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 1600 |
| advertisement\_interval\_maximum | integer | Advertising interval maximum (must be >= Advertising interval minimum. <br>Default: 2000.<br>Calculation: advertisement_interval_maximum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 2000 |

### AT+UBTASDC - Bluetooth Scan Data Clear

Clear the custom scan response data, i.e. use the default value when advertising

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTASDC` | Clear the custom scan response data. |

### AT+UBTB - Bluetooth Bond

Performs a GAP bond procedure with another Bluetooth device. For some I/O Capabilities, user interaction is required during the bonding procedure. The procedure to use is determined by the I/O Capabilities and security mode. **The maximum number of stored bonds is 30 for NORA-B26.**

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTB=<bd_addr>` | Initiate bonding. To perform the bonding, the remote device must be in a pairable and connectable mode. Bond Event +UEBTB is generated once the bond is complete. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd_addr | Bluetooth device address of the remote device. |

### AT+UBTBSM - Bluetooth Bond Security Mode

Set the **minimum** security mode ~~of the device.~~ **required when bonding.** This command works together with AT+UBTIOC to determine the bonding procedure used. **The module will try to use the highest level possible based on the settings of this command, AT+UBTIOC and the capabilities of the remote device. If the remote device does not support the required security level, the bonding procedure will fail.**

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTBSM=<bt_security_mode>`~~ | ~~Writes the security mode~~ |
| `AT+UBTBSM?` | Reads the security mode |
| **`AT+UBTBSM=<security_mode>`** | **Writes the security mode<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTBSM:<bt_security_mode>`~~ | ~~Successful read response for AT+UBTBSM?~~ |
| **`+UBTBSM:<security_mode>`** | **Successful read response for AT+UBTBSM?** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~bt\_security\_mode~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Security Disabled.<br>1: Allow unauthenticated bonding.<br>2: Only allow authenticated bonding. No secure connections.<br>3: Only allow authenticated bonding with encrypted Bluetooth link. Support secure connections. Fallback to simple pairing if the remote side does not support secure connections.<br>4: Only allow authenticated bonding with encrypted Bluetooth link. Strictly uses secure connections.<br><br>**Default value: 0**~~ |
| **security\_mode** | **enumerator** | ****Valid values:**<br>0: Security not required. No encryption enforced.<br>1: Require at least unauthenticated bonding.<br>2: Require authenticated bonding. No secure connections.<br>3: Require authenticated bonding. Support secure connections. Fallback to simple pairing if the remote side does not support secure connections.<br>4: Require authenticated bonding. Strictly uses secure connections.<br><br>**Default value: 0**** |

### AT+UBTCS - Bluetooth Connection Settings

Get and set connection related settings

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCS0=<connection_interval_minimum>` | Write connection interval minimum.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCS0?` | Read Connection Interval minium. |
| `AT+UBTCS1=<connection_interval_maximum>` | Write connection interval maximum.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCS1?` | Read Connection Interval maximum. |
| `AT+UBTCS2=<connection_peripheral_latency>` | Write connection peripheral latency.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCS2?` | Read connection peripheral latency. |
| `AT+UBTCS3=<connection_linkloss_timeout>` | Write connection linkloss timeout.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCS3?` | Read connection linkloss timeout. |
| `AT+UBTCS4=<preferred_tx_phy>` | Write Preferred TX PHY.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCS4?` | Read Preferred TX PHY. |
| `AT+UBTCS5=<preferred_rx_phy>` | Write Preferred RX PHY.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTCS5?` | Read Preferred RX PHY. |
| `AT+UBTCS?` | Read all Bluetooth Configuration param values. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTCS0:<connection_interval_minimum>` | Successful read of connection interval minimum. |
| `+UBTCS1:<connection_interval_maximum>` | Successful read of connection interval maximum. |
| `+UBTCS2:<connection_peripheral_latency>` | Successful read of connection peripheral latency. |
| `+UBTCS3:<connection_linkloss_timeout>` | Successful read of connection linkloss timeout. |
| `+UBTCS4:<preferred_tx_phy>` | Successful read of Preferred TX PHY. |
| `+UBTCS5:<preferred_rx_phy>` | Successful read of Preferred RX PHY. |
| `+UBTCS:<param>,<value>` | Successful read response for AT+UBTCS. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| connection\_interval\_minimum | integer | Connection interval minimum (must be <= Connection interval maximum). Final results will be a result of negotiation between devices.<br>Default: 24.<br>Calculation: connection_interval_minimum * 1.25. ms<br><br>Valid values: 6..3200<br><br>Default value: 24 |
| connection\_interval\_maximum | integer | Connection interval maximum (must be >= Connection interval minimum). Final results will be a result of negotiation between devices.<br>Default: 40.<br>Calculation: connection_interval_maximum * 1.25 ms.<br><br>Valid values: 6..3200<br><br>Default value: 40 |
| connection\_peripheral\_latency | integer | Connection peripheral latency.<br>Default: 0<br>Calculation: Number of connection events.<br><br>Valid values: 0..500<br><br>Default value: 0 |
| connection\_linkloss\_timeout | integer | Connection linkloss timeout.<br>Default: 2000<br>Calculation: connection_linkloss_timeout ms<br><br>Valid values: 100..32000<br><br>Default value: 2000 |
| preferred\_tx\_phy | integer | Preferred Transmitter PHY<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br>Bit 3: Coded PHY type. 0: Use S8 coding, 1: Use S2 coding<br><br>Valid values: 0..15<br><br>Default value: 0 |
| preferred\_rx\_phy | integer | Preferred PHY for Receiver<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br><br>Valid values: 0..15<br><br>Default value: 0 |
| param | enumerator | Connection parameter.<br><br>Valid values:<br>0: Connection interval minimum.<br><br>1: Connection interval maximum.<br><br>2: Connection peripheral latency.<br><br>3: Connection linkloss timeout.<br><br>4: Preferred Transmitter PHY<br><br>5: Preferred Receiver PHY |
| value | integer | Value of connection parameter.<br><br>Valid values: 0..65535 |

### AT+UBTCST - Bluetooth Connection Status

Read negotiated properties of a Bluetooth low energy ACL connection.
Some of the properties are a result of negotiation when a connections is set up, and this command gives the possibility
to see what properties the connection actually uses.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCST=<conn_handle>` | Read all properties of an existing Bluetooth low energy ACL connection. |
| ~~`AT+UBTCST=<conn_handle>,<property_id>`~~ | ~~Read a specific property of an existing Bluetooth low energy ACL connection.~~ |
| **`AT+UBTCST=<conn_handle>,<prop_id>`** | **Read a specific property of an existing Bluetooth low energy ACL connection.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTCST:<property_id>,<status_val>`~~ | ~~Successful read response.~~ |
| **`+UBTCST:<prop_id>,<status_val>`** | **Successful read response.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| status\_val | integer | Value of the preceding property. |
| ~~property\_id~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Connection interval used on this connection.<br> Range: 6 to 3200<br> Time = status_val * 1.25 ms<br> Time range: 7.5 ms to 4000 ms<br><br>1: Peripheral latency for the connection in number of connection events. Range: 0 to 499<br>2: Supervision timeout (in ms) for this connections. Range: 100 ms to 32000 ms<br>3: MTU size for this connections.<br>4: Data Channel TX PDU Payload Length.<br>5: Data Channel RX PDU Payload Length.<br>6: Data Length Extension state. 0: Data Length Extension Off \ 1: Data Length Extension On<br>7: Local role in this connection. 1: Low Energy Central \ 2: Low Energy Peripheral<br>8: TX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: Coded<br><br>9: RX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: Coded~~ |
| **prop\_id** | **enumerator** | ****Valid values:**<br>0: Connection interval used on this connection.<br> Range: 6 to 3200<br> Time = status_val * 1.25 ms<br> Time range: 7.5 ms to 4000 ms<br><br>1: Peripheral latency for the connection in number of connection events. Range: 0 to 499<br>2: Supervision timeout (in ms) for this connections. Range: 100 ms to 32000 ms<br>3: MTU size for this connections.<br>4: Data Channel TX PDU Payload Length.<br>5: Data Channel RX PDU Payload Length.<br>6: Data Length Extension state. 0: Data Length Extension Off \ 1: Data Length Extension On<br>7: Local role in this connection. 1: Low Energy Central \ 2: Low Energy Peripheral<br>8: TX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: Coded<br><br>9: RX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: Coded** |

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
| discovery\_type | enumerator | Valid values:<br>0: All with no filter. Displays all found devices; devices can be displayed multiple times.<br>1: General inquiry. Displays devices in General or Limited discoverability mode; each device is displayed only once. |
| discovery\_mode | enumerator | Valid values:<br>0: Active discovery.<br>1: Passive, no scan response data will be received.<br><br>Default value: 0 |
| discovery\_length | integer | Timeout measured in milliseconds. Time range: 10 ms - 40 s<br><br>Valid values: 10..40000<br><br>Default value: 5000 |
| device\_name | string | Name of the discovered device. |
| data\_type | enumerator | Type of advertising data received.<br><br>Valid values:<br>0: Scan response data.<br><br>1: Advertise data.<br><br>2: Extended advertise data. |
| data | byte_array | Complete advertise/scan response data received from the remote device. |

### AT+UBTDIS - Bluetooth Device Information Service

Write and read the module's Device Information Service (DIS) characteristics.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTDIS=<characteristic_id>,<characteristic_value>`~~ | ~~Set a characteristic value.~~ |
| ~~`AT+UBTDIS=<characteristic_id>`~~ | ~~Read a characteristic value.~~ |
| `AT+UBTDIS?` | Read all individual characteristic of the Device Information Service characteristics. |
| **`AT+UBTDIS=<char_id>,<char_value>`** | **Set a characteristic value.<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |
| **`AT+UBTDIS=<char_id>`** | **Read a characteristic value.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTDIS:<characteristic_id>,<characteristic_value>`~~ | ~~Successful read response.~~ |
| **`+UBTDIS:<char_id>,<char_value>`** | **Successful read response.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~characteristic\_id~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Manufacturer name string. Maximum length of the custom string is 31 characters.<br>1: Model name string. Maximum length of the custom string is 20 characters.<br>2: Firmware revision string. Maximum length of the custom string is 20 characters.<br>3: Software revision string. Maximum length of the custom string is 20 characters.~~ |
| ~~characteristic\_value~~ | ~~string~~ | ~~Value of Device Information Service characteristic.~~ |
| **char\_id** | **enumerator** | ****Valid values:**<br>0: Manufacturer name string. Maximum length of the custom string is 31 characters.<br>1: Model name string. Maximum length of the custom string is 20 characters.<br>2: Firmware revision string. Maximum length of the custom string is 20 characters.<br>3: Software revision string. Maximum length of the custom string is 20 characters.** |
| **char\_value** | **string** | **Value of Device Information Service characteristic.** |

### AT+UBTIOC - Bluetooth I/O Capabilities

Set Bluetooth I/O Capabilities, this impacts the possible bonding procedure between devices.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTIOC=<io_capabilities>`~~ | ~~Set I/O Capabilities~~ |
| `AT+UBTIOC?` | Read I/O Capabilities |
| **`AT+UBTIOC=<io_cap>`** | **Set I/O Capabilities<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTIOC:<io_capabilities>`~~ | ~~Successful read response for AT+UBTIOC?.~~ |
| **`+UBTIOC:<io_cap>`** | **Successful read response for AT+UBTIOC?.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~io\_capabilities~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Set I/O Capabilities to No Input No Output.<br>1: Set I/O Capabilities to Display Only.<br>2: Set I/O Capabilities to Display Yes/No<br>3: Set I/O Capabilities to Keyboard Only.<br>4: Set I/O Capabilities to Keyboard Display.<br><br>**Default value: 0**~~ |
| **io\_cap** | **enumerator** | ****Valid values:**<br>0: Set I/O Capabilities to No Input No Output.<br>1: Set I/O Capabilities to Display Only.<br>2: Set I/O Capabilities to Display Yes/No<br>3: Set I/O Capabilities to Keyboard Only.<br>4: Set I/O Capabilities to Keyboard Display.<br><br>**Default value: 0**** |

### AT+UBTLN - Bluetooth Local Name

Set the **BLE** local name used ~~as device name for Bluetooth Classic,~~ in the ~~advertising~~ **default scan response** data ~~of the device~~ and in the ~~Device Information service for Bluetooth low energy.~~ **Generic Access Profile service.**

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTLN?` | Reads the local Bluetooth device name. |
| `AT+UBTLN=<device_name>` | Writes the local Bluetooth device name.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTLN:<device_name>` | Successful read response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| device\_name | string | ~~For Bluetooth low energy~~ **Default local name is** the ~~maximum size~~ **MODEL-xxxxxx where xxxxxx are the last 3 bytes of the device MAC address in hexadecimal format. If the local name** is ~~29 characters.~~ **set to "" it is cleared but will revert to the default name after a restart.**<br><br>Length: 0..29<br><br>Length: 0..29 |

### AT+UBTM - Bluetooth Mode

Set and read Bluetooth Mode.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTM=<bt_mode>`~~ | ~~Set Bluetooth Mode.~~ |
| `AT+UBTM?` | Read Bluetooth Mode. |
| **`AT+UBTM=<mode>`** | **Set Bluetooth Mode.<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+UBTM:<bt_mode>`~~ | ~~Successful read response.~~ |
| **`+UBTM:<mode>`** | **Successful read response.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~bt\_mode~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Disabled.<br>1: Bluetooth Low Energy Central.<br>In this mode, starting advertisements, direct advertisements and other functions associated<br>with the Peripheral role is not possible.<br><br>2: Bluetooth Low Energy Peripheral.<br>In this mode, initiating connections, discovery and other functions associated with<br>the Central role is not possible.<br><br>3: Bluetooth Low Energy Simultaneous Central and Peripheral. This is the factory default for NORA-W36.~~ |
| **mode** | **enumerator** | ****Valid values:**<br>0: Disabled.<br>1: Bluetooth Low Energy Central.<br>In this mode, starting advertisements, direct advertisements and other functions associated<br>with the Peripheral role is not possible.<br><br>2: Bluetooth Low Energy Peripheral.<br>In this mode, initiating connections, discovery and other functions associated with<br>the Central role is not possible.<br><br>3: Bluetooth Low Energy Simultaneous Central and Peripheral. This is the factory default.** |

### AT+UBTPM - Bluetooth Pairing Mode

Enable or disable pairing.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTPM=<pairing_mode>` | Writes the pairing mode.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTPM?` | Read current pairing mode. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTPM:<pairing_mode>` | Successful read response for AT+UBTPM? |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| pairing\_mode | enumerator | Valid values:<br>0: Disable pairing mode.<br>1: Enable pairing mode.<br><br>Default value: 0 |

### AT+UBTRSS - Bluetooth RSSI

Returns the current received RSSI for a specified Bluetooth connection.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTRSS=<conn_handle>` | Returns the current RSSI for a specified Bluetooth connection. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTRSS:<rssi>` | Successful response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| rssi | integer | Received signal strength in dBm. |

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

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTSS0:<scan_interval>` | Successful read of scan interval. |
| `+UBTSS1:<scan_window>` | Successful read of scan window. |
| `+UBTSS:<scan_param>,<value>` | Successful read response for AT+UBTSS?. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| scan\_interval | integer | Scan interval (must be >= Scan window. <br>Default: 160.<br>Calculation: scan_interval * 0.625 ms)<br><br>Valid values: 16..16384<br><br>Default value: 160 |
| scan\_window | integer | Scan window (must be <= Scan interval. <br>Default: 128.<br>Calculation: scan_interval * 0.625 ms)<br><br>Valid values: 16..16384<br><br>Default value: 128 |
| value | integer | Value of scan parameter.<br><br>Valid values: 0..65535 |
| scan\_param | enumerator | Scan parameter.<br><br>Valid values:<br>0: Scan interval.<br><br>1: Scan ~~interval~~**window**. |

### AT+UBTUC - Bluetooth User Confirmation

The user confirmation is used together with IO capability DisplayYesNo to ~~repond~~**respond** to a user confirmation request (+UEBTUC). The command shall be used only after +UEBTUC has been received.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTUC=<bd_addr>,<yes_no>`~~ | ~~Respond to +UEUBTUC and confirm/deny bonding.~~ |
| **`AT+UBTUC=<bd_addr>,<confirm>`** | **Respond to +UEUBTUC and confirm/deny bonding.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd_addr | Bluetooth device address of the remote device. |
| ~~yes\_no~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Deny bonding.<br>1: Confirm bonding.~~ |
| **confirm** | **enumerator** | ****Valid values:**<br>0: Deny bonding.<br>1: Confirm bonding.** |

### AT+UBTUPE - User passkey entry

The user passkey entry is used together with IO capability KeyboardOnly to respond on a user passkey entry request (+UEBTUPE). This command shall be used only after +UEBTUPE has been received.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTUPE=<bd_addr>,<yes_no>[,<passkey>]`~~ | ~~Respond to +UEBTUPE event and confirm/deny bonding.~~ |
| **`AT+UBTUPE=<bd_addr>,<confirm>[,<passkey>]`** | **Respond to +UEBTUPE event and confirm/deny bonding.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd_addr | Bluetooth device address of the remote device. |
| ~~yes\_no~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: Deny bonding.<br>1: Confirm bonding.~~ |
| passkey | integer | Passkey used to confirm bonding, if ~~yes_no~~ **confirm** is set to no, this can be omitted.<br><br>Valid values: 0..999999 |
| **confirm** | **enumerator** | ****Valid values:**<br>0: Deny bonding.<br>1: Confirm bonding.** |

#### GATT Server

### AT+UBTGC - GATT Characteristic define

Command to add a GATT characteristic to the most recent GATT service record created with AT+UBTGS.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTGC=<uuid>,<properties>,<security_read>,<security_write>,<value>[,<max_length>]`~~ | ~~Create a new characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported.~~ |
| **`AT+UBTGC=<uuid>,<properties>,<read_security>,<write_security>,<value>[,<max_length>]`** | **Create a new characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGC:<value_handle>,<cccd_handle>` | Successful write response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~security\_read~~ | ~~enumerator~~ | ~~**Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.~~ |
| properties | byte_array | Property value (a bit field):<br>Broadcast: 0x01 - If set, it allows broadcasts of the Characteristic Value using Characteristic Configuration Descriptor.<br>Read: 0x02 - If set, it allows reads of the Characteristic Value.<br>Write Without Response: 0x04 - If set, it allows writing of the Characteristic Value without response.<br>Write: 0x08 - If set, it allows writing of the Characteristic Value with response.<br>Notify: 0x10 - If set, it allows notifications of a characteristic value.<br>Indicate: 0x20 - If set, it allows indication of a characteristic value with acknowledgement.<br>Authenticated Signed Writes: 0x40 - If set, it allows signed writes to the characteristic value.<br>Reserved Bit: 0x80 - Do not use. Reserved for future use.<br><br>Length: 1..1 |
| ~~security\_write~~ | ~~enumerator~~ | ~~**Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.~~ |
| uuid | byte_array | UUID of characteristic. This can be either 16 bit or 128 bit. |
| value | byte_array | Default characteristic value before any value is pushed to it. A characteristic value can be 244 bytes long. |
| max\_length | integer | Maximum length of the characteristic in bytes. The maximum value is 244 bytes.<br><br>Valid values: 1..244 |
| value\_handle | integer | Added characteristic handle. |
| cccd\_handle | integer | CCCD characteristic handle. This value is zero if there is no CCCD. |
| **read\_security** | **enumerator** | ****Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.** |
| **write\_security** | **enumerator** | ****Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.** |

### AT+UBTGD - GATT Descriptor define

Define a vendor defined descriptor. Standard Bluetooth low energy descriptors such as CCCD are created while creating the characteristic in AT+UBTGC command.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTGD=<uuid>,<security_read>,<security_write>,<value>[,<max_length>]`~~ | ~~Define descriptor.~~ |
| **`AT+UBTGD=<uuid>,<read_security>,<write_security>,<value>[,<max_length>]`** | **Define descriptor.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGD:<desc_handle>` | Successful write response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~security\_read~~ | ~~enumerator~~ | ~~**Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.~~ |
| ~~security\_write~~ | ~~enumerator~~ | ~~**Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.~~ |
| uuid | byte_array | UUID of characteristic. This can be either 16 bit or 128 bit. |
| value | byte_array | Descriptor value. This can be 23 bytes long. |
| max\_length | integer | Maximum length of the descriptor in bytes. The maximum value is 23 bytes.<br><br>Valid values: 1..23 |
| desc\_handle | integer | Handle of the created descriptor. |
| **read\_security** | **enumerator** | ****Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.** |
| **write\_security** | **enumerator** | ****Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.** |

### AT+UBTGHCC - GATT Host Controlled Characteristic

Create a new host controlled characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+UBTGHCC=<uuid>,<properties>,<security_read>,<security_write>`~~ | ~~Define a characteristic.~~ |
| **`AT+UBTGHCC=<uuid>,<properties>,<read_security>,<write_security>`** | **Define a characteristic.** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGHCC:<value_handle>,<cccd_handle>` | Successful write response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~security\_read~~ | ~~enumerator~~ | ~~**Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.~~ |
| properties | byte_array | Property value (a bit field):<br>Broadcast: 0x01 - If set, it allows broadcasts of the Characteristic Value using Characteristic Configuration Descriptor.<br>Read: 0x02 - If set, it allows reads of the Characteristic Value.<br>Write Without Response: 0x04 - If set, it allows writing of the Characteristic Value without response.<br>Write: 0x08 - If set, it allows writing of the Characteristic Value with response.<br>Notify: 0x10 - If set, it allows notifications of a characteristic value.<br>Indicate: 0x20 - If set, it allows indication of a characteristic value with acknowledgement.<br>Authenticated Signed Writes: 0x40 - If set, it allows signed writes to the characteristic value.<br>Reserved Bit: 0x80 - Do not use. Reserved for future use.<br><br>Length: 1..1 |
| ~~security\_write~~ | ~~enumerator~~ | ~~**Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.~~ |
| uuid | byte_array | UUID of characteristic. This can be either 16 bit or 128 bit. |
| value\_handle | integer | Value handle of the added characteristic. |
| cccd\_handle | integer | Client Characteristic Configuration Descriptor (CCCD) handle of the added characteristic. This value is zero if there is no CCCD. |
| **read\_security** | **enumerator** | ****Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.** |
| **write\_security** | **enumerator** | ****Valid values:**<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required.** |

#### GATT client

### AT+UBTGCCW - GATT Client Configuration Write

Write characteristic configuration to enable notifications or indications.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGCCW=<conn_handle>,<desc_handle>,<config>` | Writes the client characteristic configuration. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| desc\_handle | integer | Descriptor handle. |
| config | enumerator | Valid values:<br>0: None<br>1: Enable notifications<br>2: Enable indications<br>3: Enable notifications and indications |

### AT+UBTGWL - GATT Write long

Write a long characteristic.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGWL=<conn_handle>,<value_handle>,<hex_data>,<reliable>,<flag>,<offset>` | Write long characteristic. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |
| reliable | enumerator | Valid values:<br>0: Not reliable<br>1: Reliable |
| flag | enumerator | Valid values:<br>0: Final data<br>1: More data<br>2: Cancel **data writing** |
| offset | integer |  |

#### Power

### AT+UPMDS - Power Management Deep Sleep


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UPMDS` | Enter Deep Sleep Mode with GPIO wakeup. |
| `AT+UPMDS=<wakeup_mode>` | Enter Deep Sleep Mode with specified wakeup mode. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wakeup\_mode | enumerator | Selects how to wake up from deep sleep.<br><br>Valid values:<br>0: Wakeup by pulling the module wakeup pin low.<br><br>1: Wakeup by module reset pin.<br><br>**2: Wakeup by module UART RX pin.**<br><br>Default value: 0 |

#### SPS

### AT+USPS - SPS - Enable/Disable Service

Enable or disable the SPS ~~service~~ **service. SPS Service will use the security mode set in AT+UBTBSM**

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| ~~`AT+USPS=<sps_service_option>`~~ | ~~Enables or disable the SPS Service.~~ |
| `AT+USPS?` | Read if the SPS service is enabled or disabled. |
| **`AT+USPS=<service_option>`** | **Enables or disable the SPS Service.<br><br>Notes:<br>Can be stored using [AT&W](#atw).** |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| ~~`+USPS:<sps_service_option>`~~ | ~~Successful read response.~~ |
| **`+USPS:<service_option>`** | **Successful read response.** |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ~~sps\_service\_option~~ | ~~enumerator~~ | ~~**Valid values:**<br>0: This option disables the SPS service after saving the configuration and restarting the device. (Default)<br>1: This option enables the SPS service directly.<br>If this option is set, and the configuration is saved,<br>SPS will be enabled after reboot.~~ |
| **service\_option** | **enumerator** | ****Valid values:**<br>0: This option disables the SPS service after saving the configuration and restarting the device. (Default)<br>1: This option enables the SPS service directly.<br>If this option is set, and the configuration is saved,<br>SPS will be enabled after reboot.** |

### AT+USPSRM - SPS Receive Mode


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPSRM=<read_mode>` | Set the mode in which to receive SPS data in AT mode.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USPSRM?` | Read mode set. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPSRM:<read_mode>` | Successful read response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| read\_mode | enumerator | Modes to read data in AT<br><br>Valid values:<br>0: Buffered mode<br><br>1: Direct String mode<br><br>2: Direct Binary Mode |

#### System

### AT+USYBL - Start the boot loader command line interface

Force start of the boot loader. The boot loader will start at the defined baud rate.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYBL=<baud_rate>[,<flow_control>]` | Force start of the boot loader. |
| `AT+USYBL` | Force start of the boot loader with default settings. Baudrate 115200 and flow control off. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200,2400,4800,9600,14400,28800,31250,38400,56000,57600,76800,115200,230400,250000,460800,921600,1000000<br><br>Default value: ~~115200~~~~**U_CONFIG_DEFAULT_BAUDRATE**<br><br>Default value: ~~115200~~**U_CONFIG_DEFAULT_BAUDRATE** |
| flow\_control | integer | Valid values: 0..1<br><br>Default value: 0 |

### AT+USYFWUS - Firmware Update using serial port

Start serial port firmware upgrade. The module will indicate that it is ready to receive
the new firmware by regularly sending the XModem start byte C until either an XModem transfer has started,
or a timeout has occurred


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYFWUS=<baud_rate>[,<flow_control>]` | Start firmware upgrade on the serial port with provided settings |
| `AT+USYFWUS` | Start firmware upgrade on the serial port with default settings, baudrate 115200 and no flow control |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200,2400,4800,9600,14400,28800,31250,38400,56000,57600,76800,115200,230400,250000,460800,921600,1000000<br><br>Default value: ~~115200~~~~**U_CONFIG_DEFAULT_BAUDRATE**<br><br>Default value: ~~115200~~**U_CONFIG_DEFAULT_BAUDRATE** |
| flow\_control | integer | Valid values: 0..1<br><br>Default value: 0 |

### AT+USYLA - Local Address


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYLA=<interface_id>` | Get interface address |
| `AT+USYLA=<interface_id>,<address>` | Set interface address<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USYLA:<address>` | Successful read response |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| interface\_id | enumerator | Valid values:<br>0: ~~Bluetooth<br>1: Wi-Fi station<br>2: Wi-Fi Access point~~ **Bluetooth** |
| address | mac_addr | MAC address of the interface id. If the address is set to 000000000000, the local address will be restored to factory-programmed value. The least significant bit of the first octet of the ~~<address>~~ **address** must be 0. |

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
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200,2400,4800,9600,14400,28800,31250,38400,56000,57600,76800,115200,230400,250000,460800,921600,1000000<br><br>Default value: ~~115200~~~~**U_CONFIG_DEFAULT_BAUDRATE**<br><br>Default value: ~~115200~~**U_CONFIG_DEFAULT_BAUDRATE** |
| flow\_control | integer | 0: No flow control<br>1: Use CTS/RTS flow control<br><br>Valid values: 0..1 |
| change\_after\_confirm | integer | 0: Switch baudrate after reboot. When set AT&W must be called.<br>1: Switch baudrate directly after status OK have been sent.<br><br>Valid values: 0..1 |

#### Transparent

### AT+UTM - Transparent Mode

Use this command to directly switch to transparent mode for a specific SPS link or a socket.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UTM=<link_type>,<handle>` | Enter Transparent Mode |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| link\_type | enumerator | Valid values:<br>0: BLE SPS Link<br>1: Socket |
| handle | integer | For SPS links, set this to the connection handle<br>For sockets, set this to the socket handle |

### AT+UTMP - Transparent Mode Persistent

This command is used for automatically setting up a transparent mode connection on boot.

**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UTMP=<link_type>,<config_id>` | Set persistent transparent mode for link<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UTMP?` | Get current persistent transparent mode configuration |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UTMP:<link_type_read>,<config_id>` | Successful read response. |

**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| link\_type | enumerator | Valid values:<br>0: BLE SPS Link<br>1: Socket |
| link\_type\_read | enumerator | Valid values:<br>-1: No link type set<br>0: BLE SPS Link<br>1: Socket |
| config\_id | integer | For SPS, set this to the config_id returned by AT+UBTP. |

