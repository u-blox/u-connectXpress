# **NORA-W36 u-connectXpress**

## Stand-alone multiradio modules

## <span style="color: gray;">User guide</span>

![short range](https://content.u-blox.com/sites/default/files/2024-02/shortrange.png)

This document provides an overview of the u-connectXpress software for u-blox short range modules
and describes how the products can be configured for Wi-Fi and Bluetooth Low Energy use cases.

![NORA-W36](https://content.u-blox.com/sites/default/files/2026-01/NORA-W36.png)

**Quick Navigation Guide for First-Time Users:**

- **Getting Started Fast** → [Quick Start Guide](#quick-start-guide) (quick setup)
- **Wi-Fi Connection** → [Wi-Fi station WPA2/WPA3](#wi-fi-station-wpa2-and-wpa3) (most common)
- **Bluetooth Setup** → [Bluetooth GATT server](#bluetooth-gatt-server) (peripheral mode)
- **Data Transfer** → [Send and receive data](#send-and-receive-data) (modes explained)
- **Troubleshooting** → [Error codes](#error-codes) (when things go wrong)
- **AT Commands Index** → [Appendix A](#appendix) (command lookup)

## Document information

| Title | NORA-W36 series u-connectXpress |
| :------------ | ---------------- |
| Subtitle    |  Stand-alone multiradio modules             |
| Document type | User guide |
| Version and date |3.2.0 14-Jan-2026 |
| Disclosure restriction    |C1-Public |

**This document applies to the following products**
| Product name    |  Software version |
| :------------ | ---------------- |
| NORA-W36 series    |  3.2.0|

**Disclaimer**
u-blox or third parties may hold intellectual property rights in the products, names, logos, and designs included in this document. Copying, reproduction, or modification of this document or any part thereof is only permitted with the express written permission of u-blox. Disclosure to third parties is permitted for clearly public documents only.
The information contained herein is provided "as is" and u-blox assumes no liability for its use. No warranty, either express or implied, is given, including but not limited to, with respect to the accuracy, correctness, reliability, and fitness for a particular purpose of the information. This document may be revised by u-blox at any time without notice. For the most recent documents, visit [www.u-blox.com](https://www.u-blox.com).
Copyright © u-blox AG

# Overview

This document describes how to set up and use u-blox short range stand-alone modules with u-connectXpress software for NORA-W36. It explains the functionality of different u-blox short range stand-alone modules and includes examples that describe how to use the software in different environments with AT commands. The document is applicable for Bluetooth® Low Energy (LE), multiradio, and Wi-Fi modules.
Several u-blox short range stand-alone modules support open software variants. For more information about the available options, see the corresponding system integration manuals for u-blox short range stand-alone modules.
For older generation modules like ODIN-W2, NINA-W15 and ANNA-B1, the [u-connectXpress user guide](https://www.u-blox.com/docs/UBX-16024251) describes the functionality of these modules.

## Getting started with s-center

**Downloading and installing**
1. Download the latest version of [s-center](https://www.u-blox.com/en/product/s-center)
2. Double click the downloaded file and follow the installation instructions
3. Launch s-center when the installation is completed

## Product description

u-blox modules are developed for integration into a vast range of devices that demand a high level of reliability, such as those that are typically used in industrial and medical applications.
These professional grade modules operate over an extended temperature range and are approved for radio type application products in many countries. By choosing to use u-blox short range stand-alone modules, the cost and work involved in developing wireless communication solutions is significantly reduced.

| Concept             | Definition |
| ------------------ | :------------ |
|**Host**                |In this document, a host refers to the device connected to a u-blox short range stand-alone module through any of the available physical interfaces. In a real application, the host is typically a microcontroller Unit (MCU) running a customer specific application. |
|**Module**               | In this document, module refers to a u-blox stand-alone module running the u-connectXpress software. |
|**Remote device**    | A remote device in a wireless network connecting over the Bluetooth Low Energy or Wi-Fi interfaces supported in the module.|

## Multiradio and Wi-Fi modules

u-blox compact and powerful stand-alone, multiradio modules are designed for the development of Internet-of-Things (IoT) applications. NORA-W36 modules include an embedded Bluetooth stack, Wi-Fi driver, IP stack, and an application for wireless data transfer. The wireless support includes Bluetooth Low Energy 5.3 Wi-Fi 4 dual band 2,4 and 5 GHz.
The modules support point-to-point and point-to-multipoint configurations and can accommodate concurrent Bluetooth and Wi-Fi connections. The software provides support for micro Access Point.
They are delivered with u-connectXpress software that provides support for u-blox Bluetooth LE Serial Port Service, Generic Attribute Profile (GATT) server, Bluetooth beacons, Peripheral role - all configurable from a host by means of AT commands.

# Quick Start Guide

## Initial setup checklist

Before starting with NORA-W36 configuration, ensure the following setup is complete:

### Hardware setup

**Essential Hardware Connections:**

- ☐ **Power Supply (3.3V)** - Connect regulated 3.3V power to VCC pin
- ☐ **Ground Connection** - Connect GND pin to your system's ground reference
- ☐ **UART Interface** - Connect TX/RX pins between NORA-W36 and host system

**Recommended:**

- ☐ **Reset Circuit** - Wire reset pin for hardware reset capability
- ☐ **Bootloader Recovery Switches** - Install SW1 and SW2 for easy factory reset and bootloader access (see NORA-W36 SIM for details)

### Software setup

- ☐ **s-center 2 Installation**: Download and install [s-center 2](https://www.u-blox.com/en/product/s-center)
- ☐ **Serial Connection**: Configure correct COM port and baud rate (115200 default)
- ☐ **AT Command Testing**: Verify communication with basic `AT` command

#### UART configuration defaults

**Current NORA-W36 UART Settings:**

- **Baud Rate**: 115200 bps
- **Data Bits**: 8
- **Start Bits**: 1
- **Stop Bits**: 1
- **Parity**: None (8N1 format)
- **Hardware Flow Control**: **Disabled by default** (only TX/RX/GND required)

**📌 Connection Requirements:**
- **Minimum**: TX, RX, and GND pins only
- **Recommended for higher baud rates**: CTS/RTS pins for hardware flow control

### Initial verification commands

| Step | Command | Expected Response | Purpose |
|------|---------|------------------|---------|
| 1 | `AT` | `OK` | Test basic communication |
| 2 | `ATI` | Module information | Verify module identity |
| 3 | `AT+GMI` | `u-blox` | Check manufacturer |
| 4 | `AT+GMM` | `NORA-W36` | Check model |
| 5 | `AT+GMR` | Software version | Check firmware version |

## First connection examples

### Quick Wi-Fi connection

**📶 Wi-Fi Connection Flow:**

```
    ┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
    │ 📋 Configure    │───▶│ 🔒 Authenticate │───▶│ ✅ Connected   │
    │    Network      │    │    & Secure      │    │    & Online     │
    └─────────────────┘    └──────────────────┘    └─────────────────┘
             │                       │                       │
         SSID/PWD                UWSC=0                  Link Up

    🔧 AT Commands:            🔒 Security:            ✅ Status Events:

    • AT+UWSCP (SSID)         • WPA2/WPA3             • +UEWLU (Link)
    • AT+UWSSW (Password)     • Auto-negotiate        • +UEWSNU (Network)
    • AT+UWSC=0 (Connect)     • 2048-bit keys         • Ready for data!

```

**Basic WPA2/WPA3 Station Connection:**

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UWSCP=0,"YourSSID"` | Set network name |
| 2 | `AT+UWSSW=0,"YourPassword",0` | Set password (WPA2/WPA3 compatible) |
| 3 | `AT+UWSC=0` | Connect to network |
| 4 | Wait for `+UEWLU:0,BBBBBBBBBBB,6` | Wi-Fi link up |
| 5 | Wait for `+UEWSNU` | Network interface up |
| 6 | `AT+UWSNST?` | Check network configuration |

**Full Network Configuration Response:**
```
AT+UWSNST?
+UWSNST:0,192.168.1.59             // IPv4 address
+UWSNST:1,255.255.255.0            // Subnet mask
+UWSNST:2,192.168.1.1              // Gateway
+UWSNST:3,192.168.1.1              // Primary DNS
+UWSNST:4,0.0.0.0                  // Secondary DNS
+UWSNST:5,[fe80::56f8:2aff:fe10:aad4]        // IPv6 address
OK
```

**Quick Check:** For basic connectivity verification, you can query just the IP address:
```
AT+UWSNST=0
+UWSNST:0,192.168.1.59             // IPv4 address sufficient for most use cases
OK
```

### Quick Bluetooth advertising

**📱 Bluetooth LE Advertisement Flow:**

```
    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 🔧 Configure    │───▶│ 📡 Advertise   │───▶│ 📲 Discoverable │
    │   Parameters    │    │   & Beacon      │    │   by Devices    │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
             │                       │                       │
        Set Interval           Start Broadcast          Device Scan

    ⚙️ Configuration:          📡 Broadcasting:         📱 Detection:

    • Interval: 100ms         • Device name            • "NORA-W36"
    • Legacy mode             • BLE 5.3 compliant     • RSSI signal
    • Auto-connectable        • Low power mode        • Available services

```

**Basic BLE Advertising Setup:**

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UBTALS=160,160` | Set legacy advertising parameters (100ms interval) |
| 2 | `AT+UBTAL` | Start legacy advertising |
| 3 | Device is now discoverable | Check with smartphone BLE scanner |

**Expected Result:** Module appears as "NORA-W36" in Bluetooth device scans

### Quick TCP connection test

**TCP Socket Communication Flow:**

```
    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │  🔌 Create      │───▶│ 🔗 Connect     │───▶│ 📤 Send/Receive │
    │     Sockt       │    │   to Server     │    │      Data       │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
             │                       │                       │
        USOCR=6              httpbin.org:80              HTTP GET

    🔧 Socket Setup:          🔗 TCP Connection:         📊 Data Exchange:

    • IPv4 TCP socket         • Remote server            • HTTP protocol
    • System allocated        • Port 80 (HTTP)          • Request/Response
    • Ready for connection    • Bidirectional           • Text-based data

```

**After Wi-Fi connection, test TCP socket:**

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+USOCR=6` | Create TCP socket |
| 2 | `AT+USOC=0,"httpbin.org",80` | Connect to test server |
| 3 | `AT+USOWS=0,"GET / HTTP/1.1\r\nHost: httpbin.org\r\n\r\n"` | Send HTTP request |
| 4 | `AT+USORS=0,100` | Read response |

**Expected Result:** HTTP response from httpbin.org server

## Common quick start issues

### Communication problems

**🔧 Hardware & Communication Troubleshooting:**

| Issue | Symptom | Solution |
|-------|---------|----------|
| 🔇 No response to AT | Silent or garbled text | ✅ Check baud rate (115200), TX/RX/GND wiring (CTS/RTS optional) |
|  `ERROR` responses | Commands not recognized | ✅ Check firmware version, command syntax |
|  Connection timeouts | Commands hang | ✅ Check power supply stability, reset module |

### Wi-Fi connection issues

**📶 Wi-Fi Network Troubleshooting:**

| Issue | Symptom | Quick Fix |
|-------|---------|-----------|
| 🚫 Connection fails | `ERROR` on `AT+UWSC=0` | ✅ Verify SSID and password spelling |
|  No IP address | Wi-Fi connects but no `+UEWSNU` | ✅ Check DHCP server, router configuration |
| 📡 Weak signal | Connection drops frequently | ✅ Move closer to router, check antenna |

**Quick Debug Commands:**

| Command | Purpose | Usage |
|---------|---------|-------|
| `AT+USYEE=1` | Enable extended error codes | Run first to get detailed error information |
| `AT+USYEC?` | Check last error code | Query after any failed operation |
| `AT+UWSST=4` | Check signal strength (RSSI) | Monitor connection quality |

## Next steps

After successful quick start:
1. **Explore specific use cases** → [Wi-Fi use cases](#wi-fi-connection-use-cases) or [Bluetooth use cases](#bluetooth-use-cases)
2. **Learn about security** → [WPA2/WPA3 configuration](#wi-fi-station-wpa2-and-wpa3)
3. **Understand data modes** → [Send and receive data](#send-and-receive-data)
4. **Advanced features** → [TLS configuration](#tls-version-configuration), [MQTT](#mqtt-use-cases)


# Key features

The possibility of replacing serial cables with simple wireless connections is a key feature of u-blox modules. It allows system hosts to transfer data to one another over wireless Bluetooth connections that are established between u-blox modules in Central/Peripheral configuration.
Depending on the module capabilities, data from each host is transferred to local u-blox modules over a serial UART interface.
u-blox modules can, depending on module capabilities, be configured to automatically establish new connections and/or accept incoming connections using AT commands. For connected hosts, this means that physical serial cables can be replaced with more convenient wireless solutions.

## Bluetooth GATT connection

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
NORA-W36 can function as either a Central or Peripheral unit, connecting to devices such as laptops, cellular phones, and tablets using the Generic Attribute Profile (GATT).

## Bluetooth SPS connection

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
NORA-W36 can function as either a Central or Peripheral unit, connecting to devices such as laptops, cellular phones, and tablets via the u-blox Serial Port Service (SPS).

## Wi-Fi station connection

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)
NORA-W36 can operate as a Station connecting to an Access Point.

## Wi-Fi access point connection

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)
NORA-W36 can operate as an Access Point connecting to other devices that operate as Stations.

# u-connectXpress software

## Operating modes

NORA-W36 operates in the following modes:

- **AT mode (default)**:  AT commands and data can be sent at the same time. Data is sent and received in AT commands and events - in string or binary mode
- **Transparent Mode (TM)**:  All data sent and received on the UART is connected to the remote device
- **Transparent Mode Persistent (TMP)**:  Same as TM, but the connection is established at startup or when the connection is dropped
Additionally, the module supports various low-power modes, which optimize power consumption regardless of the operating mode. See also Low power modes and Power consumption optimization.


## Changing operating modes

u-blox modules can be configured to start in any operating mode. Once up and running, the modules can be switched between most modes. The modes are changed with a command or escape sequence sent to the module:
- Switch from Command mode to Transparent mode using an AT command
- Switch from Transparent mode to command mode with an escape sequence.

The module is controlled using AT commands in (default) Command mode. In this mode, the host sends control and configuration commands and indicates when data is to be sent over the UART interface.

## NORA-W36 capabilities

|u-connectXpress Features |Capability in 3.1.0 |
|:-----------------|:------------------|
|Chipset | Realtek RTL8720DF |
|Multiradio | Bluetooth Low Energy 5.3 Wi-Fi 4 dual band 2,4 and 5 GHz |
|Wi-Fi capabilities | 802.11a/b/g/n WPA2 Personal (Station & AP) and WPA3 Personal (Station only) Wi-Fi Multimedia WMM/WME/QoS (802.11e) Protected Management Frames (802.11w) Roaming using Fast BSS Transition (802.11r), Radio Measurement (802.11k), and Wireless Network Management (802.11v) |
|Wi-Fi Alliance certified | Certification ID: [WFA112253](https://api.cert.wi-fi.org/api/certificate/download/public?variantId=102907) Date of Certification: 2021-06-07 |
|Bluetooth Qualification | Declaration ID: [D065864](https://qualification.bluetooth.com/ListingDetails/207605) QDID: [194774](https://qualification.bluetooth.com/ListingDetails/161598) Qualification date: 2022-02-26 NORA-W36 listing date: 2024-02-19 |
|Wi-Fi Access Point    | 5 Stations connected |
|TCP/UDP sockets    |6 Simultaneous sockets (Note that a listening socket requires 2 sockets) |
|MQTT Connections    |1 Connection (client) |
|BLE Central connections |3 Peripherals connected |
|BLE Peripheral connections|1 Central connected |
|BLE Scatternet connections (C+P)| Central with 1 Peripheral connected, advertising and allow incoming connection as Peripheral |
|BLE Link key storage    |20 Devices. The keys that are the least used are removed first when storage is full |
|Coexistence Wi-Fi, BLE and TLS |Max  1 TLS client, 1 BLE, 2 TCP Client|
|Data transfer modes | Buffer Mode (event and read data), Direct Mode (data in event), Transparent mode (like serial port cable replacement). Buffer Mode is Default, Transparent mode only supports one link. Transparent Mode has highest throughput, then Direct Mode and then Buffer Mode |
|SPS MTU size | 244 bytes, 1000 bytes can be sent in AT command |
|TCP MTU size | 1460 bytes, 1000 bytes can be sent in AT command |
|UDP MTU size | 1460 bytes, 1000 bytes can be sent in AT command |
|HTTP MTU size | 1460 bytes, 1000 bytes can be sent in AT command |


|u-connectXpress software components |Versions in 3.2.0|
|:-----------------|:------------------|
|Realtek SDK including Bluetooth stack and Wi-Fi drivers| 6.2 + 6.2_patch_integrated_241111_f5eb173c https://online.realtek.com/Home/Login |
|lwIP TCP/IP stack | 2.0.2 https://savannah.nongnu.org/news/?group_id=3159 |
|Mbed TLS cryptographic algorithms| 3.6.4 https://github.com/Mbed-TLS/mbedtls/releases |



|u-connectXpress MQTT client |Versions in 3.1.0|
|:----------------|:------------------|
|MQTT version | 3.1.1 |
|MQTT capabilities | Publish, Subscribe, TLS, QoS, Testament and Last will |
|MQTT maximum packets size | 5k (5000) bytes for Publish and Subscribe packets |




|u-connectXpress Enterprise security | Capability in 3.1.0|
|:-----------------|:------------------|
|PEAP Authentication method | PEAPv0 with EAP-MSCHAPv2 |
|EAP Authentication method | EAP Transport Layer Security (EAP-TLS) |
|EAP-TLS certificate key size supported | 2048 and 4096 bits |

|u-connectXpress TLS feature | TLS capability in 3.1.0|
|:-----------------|:------------------|
|TLS version | TLS 1.2 and TLS 1.3 |
|TLS max number of connections | 1 |
|TLS extensions enabled by default| Server Name Indication (SNI), Maximum Fragment Length Negotiation |
|TLS Encryption keys | Advanced Encryption Standard (AES).  Data Encryption Standard (DES), Rivest Cipher 4 (RC4), and the Camellia cipher are not supported. |
|X.509 security certificate formats supported | PEM (DER not supported) |
|TLS over TCP certificate key size supported | 4096 bits |
|TLS certificates | Up to 8 certifications (or certificate chains) can be stored. Certificates can be maximum 15360 bytes. |
|TLS Extensions | Server name (SNI) Max fragment length: 4096 (4) |

More information about the AT commands used in this use cases can be found in the [NORA-W36 AT command manual](https://www.u-blox.com/en/sho-online-documentation/nora-w36/at-manual).


# AT Command Programming

This chapter covers the fundamental concepts of AT command programming with NORA-W36, including command response handling, event management, and timing considerations that are essential before diving into specific protocol implementations.


This chapter covers the fundamental concepts of event-driven programming with NORA-W36, including AT command response handling, Unsolicited Result Code (URC) event management, and data flow fundamentals that are essential before diving into specific protocol implementations.

## Event-driven programming fundamentals

## Understanding the event model

NORA-W36 operates on an **event-driven architecture** where the module continuously monitors for various conditions and notifies the host application through events. This approach enables efficient, asynchronous programming patterns.

**Key Concepts:**

- **Events are asynchronous** - They can occur at any time regardless of when commands are sent
- **Events require handling** - Your application must be prepared to process events when they arrive
- **Events provide real-time status** - They inform about connection status, data availability, errors, and more

## Event types overview

NORA-W36 generates several categories of events:

| Event Category | Purpose | Examples |
|----------------|---------|----------|
| **Connection Events** | Network and device connectivity | `+UEBTC`, `+UESOC`, `+UEWLU` |
| **Data Events** | Incoming data availability | `+UESODA`, `+UESODS`, `+UESPSDS` |
| **Status Events** | Module state changes | `+STARTUP`, `+UEWSNU`, `+UEMQC` |
| **Error Events** | Problem notifications | `+UESOCL`, `+UEWLD`, `+UEMQDC` |
| **Security Events** | Authentication and bonding | `+UEBTB`, `+UEBTUC`, `+UEBTUPE` |

## AT command response handling

## Command response types

Every AT command generates predictable response patterns that your application must handle:

#### Synchronous responses (immediate)

```bash

// Command sent:

AT+UWSNST?

// Immediate response:

+UWSNST:0,192.168.1.59             // IPv4 address
+UWSNST:1,255.255.255.0            // Subnet mask
+UWSNST:2,192.168.1.1              // Gateway
+UWSNST:3,192.168.1.1              // Primary DNS
+UWSNST:4,0.0.0.0        // Secondary DNS
+UWSNST:5,[fe80:0000:0000:0000:56f8:2aff:fe10:aad4]    // IPv6 address
OK
```

#### Asynchronous responses (delayed)

```bash

// Command sent:

AT+UWSC=0

// Immediate acknowledgment:

OK

// Later event (when connection completes):

+UEWLU:0
+UEWSNU
```

## Response parsing best practices

## Command response validation

#### Always check for ok/error

```bash
AT+UBTM=1
OK               // Success - command accepted

// vs

AT+UBTM=1
ERROR            // Failure - command rejected
```

#### Parse multi-line responses

```bash
AT+UBTBDL
+UBTBDL:AAAAAAAAAAAAp              // Bonded device 1 (BD address)
+UBTBDL:BBBBBBBBBBBBp              // Bonded device 2 (BD address)
+UBTBDL:CCCCCCCCCCCCp              // Bonded device 3 (BD address)
OK               // Final confirmation
```

#### Handle parameter responses

```bash
AT+UWSNST?
+UWSNST:0,192.168.1.59             // IPv4 address
+UWSNST:1,255.255.255.0            // Subnet mask
+UWSNST:2,192.168.1.1              // Gateway
+UWSNST:3,192.168.1.1              // Primary DNS
+UWSNST:4,0.0.0.0        // Secondary DNS
+UWSNST:5,[fe80:0000:0000:0000:56f8:2aff:fe10:aad4]    // IPv6 address
OK
```

## Command timing considerations

**Response Timeouts by Command Type:**

| Command Type | Typical Timeout | Max Timeout | Example |
|--------------|----------------|-------------|---------|
| Configuration | 1 second | 5 seconds | `AT+UBTM=1` |
| Connection | 10 seconds | 30 seconds | `AT+UWSC=0` |
| Data Transfer | 5 seconds | 15 seconds | `AT+USOWS=0,"data"` |
| Network Query | 3 seconds | 10 seconds | `AT+UWSNST?` |

## Unsolicited result code (URC) event management

## Understanding urcs

**Unsolicited Result Codes (URCs)** are events generated by NORA-W36 without being prompted by a command. They provide real-time information about module status, incoming data, and connectivity changes.

**URC Characteristics:**

- **Unprompted** - Arrive without commands being sent
- **Time-critical** - Often require immediate handling
- **Context-dependent** - May require maintaining state information
- **Protocol-specific** - Different protocols generate different URCs

## Critical URC categories

#### Connectivity urcs

```bash
+UEBTC:0,AAAAAAAAAAAAp             // Bluetooth connected
+UEBTDC:0        // Bluetooth disconnected
+UESOC:0         // Socket connected
+UESOCL:0        // Socket closed
+UEWLU:0         // Wi-Fi link up
+UEWLD:0,4       // Wi-Fi link down (reason code)
```

#### Data availability urcs

```bash
+UESODA:0,128            // 128 bytes available on socket 0
+UESODS:0,"Hello World"            // Direct string data on socket 0
+UESPSDS:0,"SPS Data"              // SPS string data received
+UEMQDA:0        // MQTT data available
```

#### Status change urcs

```bash
+STARTUP         // Module started/restarted
+UEWSNU          // Wi-Fi station network up
+UEWSND          // Wi-Fi station network down
+UEMQC:0         // MQTT connected
+UEMQDC:0        // MQTT disconnected
```

## URC handling strategies

#### Strategy 1: event-driven state machine

```bash

// Maintain connection state

connection_state = "DISCONNECTED"

// Handle connection events

if URC == "+UEBTC:0,*":

- connection_state = "BT_CONNECTED"
- start_data_monitoring()


if URC == "+UEBTDC:0":

- connection_state = "DISCONNECTED"
- stop_data_monitoring()

```

#### Strategy 2: data-driven processing

```bash

// Handle data events immediately

if URC == "+UESODS:0,*":

- data = extract_data_from_urc()
- process_incoming_data(data)


if URC == "+UESODA:0,*":

- bytes_available = extract_count_from_urc()
- read_buffered_data(bytes_available)

```

#### Strategy 3: error recovery

```bash

// Handle error conditions

if URC == "+UESOCL:0":

- log_error("Socket closed unexpectedly")
- attempt_reconnection()


if URC == "+UEWLD:0,4":

- log_error("Wi-Fi disconnected - reason 4")
- retry_wifi_connection()

```


# Data Handling and Processing

This chapter covers advanced data handling concepts, event processing patterns, and practical implementation strategies for building robust NORA-W36 applications.

## Data flow fundamentals

## Data mode overview

NORA-W36 supports multiple data handling modes, each optimized for different use cases:

| Data Mode | Behavior | Event Type | Best For |
|-----------|----------|------------|----------|
| **String Mode** | Text data only | `+UESODS`, `+UESPSDS` | JSON, XML, sensor readings |
| **Binary Mode** | All data types | `+UESODB`, `+UESPSDB` | Files, certificates, images |
| **Buffered Mode** | Store until read | `+UESODA`, `+UESPSDA` | Event-driven applications |
| **Direct Mode** | Immediate delivery | `+UESODS`/`+UESODB`, `+UESPSDS`/`+UESPSDB` | Real-time applications |
| **Transparent Mode** | UART passthrough | None (direct UART) | Legacy protocol support |

## Event-data relationship

**Understanding Data Event Flow:**

1. **Data Arrives** at module
2. **Module Processes** according to current mode
3. **Event Generated** to notify host
4. **Host Application** handles event appropriately

#### Buffered mode flow

```bash

// Data arrives → stored in buffer
// Event generated:

+UESODA:0,256            // 256 bytes available on socket 0

// Host reads data:

AT+USORS=0,256
+USORS:0,256,"actual data content here..."
OK
```

#### Direct mode flow

```bash

// Data arrives → immediately delivered

+UESODS:0,"immediate data"         // String data delivered directly

// No additional read command needed

```

## Protocol-specific event patterns

## Event categories

#### Wi-Fi socket events

```bash

// Connection sequence:

+UESOC:0         // Socket connected
+UESODA:0,128            // Data available (buffered mode)
+UESODS:0,"data"         // Data delivered (direct mode)
+UESOCL:0        // Socket closed
```

#### Bluetooth SPS events

```bash

// SPS connection sequence:

+UESPSC:0        // SPS connected
+UESPSDS:0,"Hello"       // String data received
+UESPSDA:0,64            // Binary data available
+UESPSDC:0       // SPS disconnected
```

#### MQTT events

```bash

// MQTT lifecycle:

+UEMQC:0         // MQTT connected
+UEMQDA:0        // Data available
+UEMQPC:0,123,45         // Publish completed
+UEMQDC:0        // MQTT disconnected
```

## Event processing best practices

## Event handler design patterns

#### Pattern 1: central event dispatcher

```pseudocode
function handle_event(event_string):

- if event_string.startswith("+UEBTC"):
- handle_bluetooth_connected(event_string)
- elif event_string.startswith("+UESODS"):
- handle_socket_data(event_string)
- elif event_string.startswith("+STARTUP"):
- handle_module_startup()

```

#### Pattern 2: state-based processing

```pseudocode
function process_event(event, current_state):

- switch current_state:
- case CONNECTING:
- if event == "+UESOC:0":
- transition_to_state(CONNECTED)
- case CONNECTED:
- if event.startswith("+UESODA"):
- handle_data_available(event)

```

## Error handling strategies

#### Robust event processing

```pseudocode
function safe_event_handler(event):

- try:
- process_event(event)
- except ParseError:
- log_error("Failed to parse event: " + event)


// Continue processing other events

    except ConnectionError:

- log_error("Connection lost during event processing")
- initiate_reconnection()

```

#### Event queue management

```pseudocode

// Buffer events during critical operations

event_queue = []
critical_operation_active = False

function queue_or_process_event(event):

- if critical_operation_active:
- event_queue.append(event)
- else:
- process_event_immediately(event)

```

## Performance considerations

**Event Processing Guidelines:**

- **Keep handlers fast** - Long processing can cause event loss
- **Use buffering** for high-frequency events
- **Prioritize critical events** (connection status over data)
- **Batch process** multiple data events when possible

**Memory Management:**

- **Limit event queue size** to prevent memory exhaustion
- **Clean up resources** when connections close
- **Monitor buffer usage** in high-throughput scenarios

## Practical implementation examples

## Basic event loop

```bash

// Simple event monitoring loop

while True:
    line = read_from_uart()

    if line.startswith("+"):

// This is an event (URC)

        handle_event(line)
    elif line in ["OK", "ERROR"]:

// This is a command response

        handle_command_response(line)
    elif line.startswith("+STARTUP"):

// Module restarted

        reinitialize_module()
```

## Connection state management

```bash

// Track multiple connection types

connection_states = {
    "wifi": "DISCONNECTED",
    "bluetooth": "DISCONNECTED",
    "mqtt": "DISCONNECTED"
}

// Update states based on events

function update_connection_state(event):

- if "+UEWLU" in event:
- connection_states["wifi"] = "CONNECTED"
- elif "+UEWLD" in event:
- connection_states["wifi"] = "DISCONNECTED"
- elif "+UEBTC" in event:
- connection_states["bluetooth"] = "CONNECTED"
-                // ... etc

```

## Data collection pattern

```bash

// Collect data from multiple sources

data_sources = {
    "socket_0": [],
    "sps_0": [],
    "mqtt": []
}

function handle_data_event(event):

- if "+UESODS:0" in event:
- data = extract_data(event)
- data_sources["socket_0"].append(data)
- elif "+UESPSDS:0" in event:
- data = extract_data(event)
- data_sources["sps_0"].append(data)

```

## Troubleshooting event handling

## Common issues

| Problem | Symptoms | Solution |
|---------|----------|----------|
| **Missing Events** | Expected URCs not received | Check event flow control, verify module state |
| **Event Overflow** | Events arriving faster than processing | Implement event queue, optimize handlers |
| **Parse Errors** | Malformed event strings | Add robust parsing with error recovery |
| **State Confusion** | Application state out of sync with module | Implement state verification commands |

## Debugging event flow

**Enable Debug Logging:**
```bash

// Log all events for analysis

function debug_log_event(event):

- timestamp = get_current_time()
- log_file.write(f"{timestamp}: {event}")

```

**Verify Event Sources:**
```bash
// Check which events are actually being generated
AT+UBTM?         // Check Bluetooth mode
AT+UWSNST?       // Check Wi-Fi status
AT+USOST=0       // Check socket status
```

This foundation in event-driven programming and data handling prepares you for implementing specific protocol use cases covered in subsequent chapters. Understanding these fundamentals is crucial for building robust IoT applications with NORA-W36.

# Bluetooth use cases

## Bluetooth GATT use cases

The following Bluetooth Low Energy use case, show some functionality to get started with GATT client and GATT server.

|u-connectXpress BLE default values | 3.2.0 |
|:----------------|:-----------------|
|BLE Mode default |**ON**, Central and Peripheral (Mode = 3) |
|BLE Legacy Advertising default    |**OFF**, enable with `AT+UBTAL` |

The following examples use the MAC address below, this must be replaced by the real MAC address of the devices that are used.
- Peripheral MAC address: AAAAAAAAAAAA
- Central MAC address: BBBBBBBBBBB

### Bluetooth GATT client

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
![bt-gatt-client](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-client.png)
This use case configures NORA-W36 as a Central device that operates as a GATT client and receives data.

This use case configuration is used in combination with [Bluetooth GATT server](#bluetooth-gatt-server).



| Nr| Instructions                              | AT command                        | AT event              |
|:---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Check that Bluetooth Central is enabled. **1: Central or 3: Central and Peripheral**. If so jump to step 6.   | `AT+UBTM?`     |   `+UBTM:1` or `+UBTM:3`         |
| 2 | Enable Bluetooth **1: Central** or **3: Central and Peripheral** | `AT+UBTM=1` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-W36 to startup          |                 | `+STARTUP` |
| 6 | Connect to remote device    |          `AT+UBTC=AAAAAAAAAAAAp` | `+UEBTC:0,AAAAAAAAAAAAp` |
| 7 | Discover Services and look for **180D**, which is the descriptor for the Heart Rate service. | `AT+UBTGPSD=0` | `+UBTGPSD:0,12,65535,180D` |
| 8 | Discover all Service Characteristics and look for **2A37**, which is the descriptior for the Heart Rate Measurement characteristics. | `AT+UBTGSCD=0,12,65535`                  | `+UBTGSCD:0,13,10,14,2A37` |
| 9 | Use the Value handle, which in this case is 14. The value can vary. Look for **2902**, which is the descriptor for the notification.                | `AT+UBTGCDD=0,14,15`            | `+UBTGCDD:0,13,15,2902` |
| 10 | Enable notification on the GATT Client the Central in this example | `AT+UBTGCCW=0,15,1` | `OK` |
| 11 | Notification is received on the GATT Client |                              | `+UEBTGCN:0,14,60` `+UEBTGCN:0,14,61` `+UEBTGCN:0,14,62` |

### Bluetooth GATT server

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
![bt-gatt-server](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-server.png)
This use case configures NORA-W36 as a Peripheral device that operates as GATT server and sends notifications.

This configuration works in combination with [Bluetooth GATT client](#bluetooth-gatt-client).



| Nr| Instructions                              | AT command                        | AT event              |
|---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled **2: Peripheral** and **3: Central and Peripheral**. If so jump to step 6.   | `AT+UBTM?`     |   `+UBTM:2` or `+UBTM:3`         |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-W36 to start | | `+STARTUP` |
| 6 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 7 | Write the Heart Rate service | `AT+UBTGS=180D` | `+UBTGS:21` |
| 8 | Write the GATT characteristic | `AT+UBTGC=2A37,3A,01,01,00`  | `+UBTGC:30,31` |
| 9 | Activate GATT Service           | `AT+UBTGSA`  | `OK` |
| 10 | Wait for incoming Bluetooth connection                |  | `+UEBTC:0,BBBBBBBBBBB` |
| 11 | Get the MTU for the connection (optional) | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 12 | Get the Role for the connection (optional)| `AT+UBTCST=0,7` | `+UBTCST:7,1` |
| 13 | Send a notification from the GATT Server using the value handle| `AT+UBTGNS=0,14,60` `AT+UBTGNS=0,14,61` `AT+UBTGNS=0,14,62` | `OK` |

## Bluetooth SPS use cases

The following Bluetooth Low Energy use case, show some functionality to get started with proprietary u-blox Serial Port Service - SPS [u-blox Serial Port Service](https://content.u-blox.com/sites/default/files/u-connectXpress-LowEnergySerialPortService_ProtocolSpec_UBX-16011192.pdf).

### Bluetooth SPS central

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
![bt-sps-central](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-central.png)
This use case configures NORA-W36 as a Central device that sends and receives data from another NORA-W36 module operating as a Peripheral device. The communication between the two modules is facilitated using the SPS. It is also possible to connect to other devices that supports the SPS protocol.
This use case operates in combination with [Bluetooth SPS peripheral](#bluetooth-sps-peripheral).


| Nr| Instructions                          | AT command  | AT event|
|:---|:---------------------------------------|:---------------------|:---|
| 1 | Check that Bluetooth Central is enabled. **1:Central or 3:Central and Peripheral**. If so, jump to step 6.   | `AT+UBTM?`     |   `+UBTM:1` or `+UBTM:3`         |
| 2 | Enable Bluetooth **1:Central** or **3:Central and Peripheral** | `AT+UBTM=1` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-W36 to start | | `+STARTUP` |
| 6 | Initiate Bluetooth discovery. Listen for advertising packets broadcast from Peripheral device.| `AT+UBTD` |`+UBTD:AAAAAAAAAAAAp,-52,"NORA-W36-AAAAAA",0,10094E4F52412D5733362D414141414141` |
| 7 | Connect Bluetooth | `AT+UBTC=AAAAAAAAAAAAp` | `+UEBTC:0,AAAAAAAAAAAAp` |
| 8 | Read MTU, maximum data size | `AT+UBTCST=0,3` |  `+UBTCST:3,247` |
| 9 | Read RSSI (optional)   | `AT+UBTRSS=0`     |  `+UBTRSS:-52` |
| 10 | Connect SPS using handle of Bluetooth connection       | `AT+USPSC=0`  | `OK` |
| 11 | SPS connection is up  |  | `+UESPSC:0` |
| 12 | It is now possible to send and receive SPS data in [String](#string-mode) or  [Binary](#binary-mode) mode |  |  |
| 13 | Disconnect the SPS and Bluetooth connection |`AT+UBTDC=0` |`+UESPSDC:0` `+UEBTDC:0` |

### Bluetooth SPS peripheral

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
![bt-sps-central](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-peripheral.png)
This use case configures NORA-W36 module as a Peripheral device that sends and receives data from another NORA-W36 module operating as a Central device. The communication between the two modules is facilitated using the proprietary [u-blox Serial Port Service](https://content.u-blox.com/sites/default/files/u-connectXpress-LowEnergySerialPortService_ProtocolSpec_UBX-16011192.pdf). It is also possible to connect to other devices that support the SPS protocol.
This use case configuration is used in combination with [Bluetooth SPS central](#bluetooth-sps-central).



| Nr| Instructions                          | AT command  |  AT events |
|---|:---------------------------------------|:--------------------------------------|:--------------------|
| 1 | Check that Bluetooth Peripheral is enabled. **2: Peripheral** and **3: Central and Peripheral**. If so, jump to step 6   | `AT+UBTM?`     |   `+UBTM:2` or `+UBTM:3`         |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-W36 to startup | | `+STARTUP` |
| 6 | Enable SPS on Peripheral              | `AT+USPS=1`        | `OK` |
| 7 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 8 | Peripheral receives Incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 9 | Read MTU, maximum data size on both | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 10 | Read RSSI (optional)   | `AT+UBTRSS=0`     | `+UBTRSS:-52` |
| 11 | Central Connect SPS using handle of Bluetooth connection       |   `AT+USPSC=0` | `+UESPSC:0` |
| 12 | It is now possible to send and receive SPS data in [String](#string-mode) or  [Binary](#binary-mode) mode |  |  |
| 13 | SPS and Bluetooth link is down | `+UESPSDC:0` `+UEBTDC:0` |  |

## Bluetooth advertise

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
This use case configures NORA-W36 as a peripheral device that operates as a GATT client and receives data.

This use case configuration is used in combination with Apple iPhone using the Apple Notification Center Service (ANCS).

| Nr| Instructions                              | AT command                        | AT event              |
|---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled **2: Peripheral** and **3: Central and Peripheral**. If so, jump to step 6. | `AT+UBTM?` | `+UBTM:2` or `+UBTM:3` |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-W36 to start | | `+STARTUP` |
| 6 | Set Apple ANCS Advertise data packet  | `AT+UBTAD=1115D0002D121E4B0FA4994ECEB531F40579`     | `OK` |
| 7 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 8 | Peripheral receives Incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 9 | Discover Services and look for **180A** that is the Device Information | `AT+UBTGPSD=0` | `+UBTGPSD:0,1,5,1800` `+UBTGPSD:0,6,9,1801` `+UBTGPSD:0,10,14,180A` `+UBTGPSD:0,15,19,D0611E78BBB44591A5F8487910AE4366` `+UBTGPSD:0,20,24,9FA480E0496745429390D343DC5D04AE` `+UBTGPSD:0,25,28,180F` `+UBTGPSD:0,29,34,1805` `+UBTGPSD:0,35,44,7905F431B5CE4E99A40F4B1E122D00D0` `+UBTGPSD:0,45,56,89D3502B0F36433A8EF4C502AD55F8DC` |
| 10 | Discover all Service Characteristics and look for the attribute **2A29**, which describes the Manufacturer Name String characteristics | `AT+UBTGSCD=0,10,14` | `+UBTGSCD:0,11,02,12,2A29` `+UBTGSCD:0,13,02,14,2A24` |
| 11 | Read the Manufacturer Name String **Apple Inc.** characteristics on handle 12  | `AT+UBTGR=0,12`  | `+UBTGR:0,12,4170706C6520496E632E` (Apple Inc.) |

## Bluetooth security

**Pairing**
- Pairing is the initial process where two Bluetooth devices exchange information necessary to establish an encrypted connection
- During pairing, devices negotiate security parameters, such as encryption keys and authentication methods
- It ensures that communication between devices remains confidential and secure
Think of pairing as the handshake that sets the foundation for a secure link

**Bonding**
- Bonding occurs after successful pairing
- It involves storing the information from the pairing process on both devices
- Once bonded, devices remember each other's security credentials (keys) for future reconnections
- Bonding eliminates the need to repeat the pairing process every time the devices reconnect
- Essentially, bonding creates a permanent security relationship between the devices

**In summary**
- Pairing: Establishes the initial secure connection
- Bonding: Ensures that the devices remember each other's security details for subsequent interactions
- Remember, these processes are essential for maintaining the confidentiality and integrity of data exchanged over Bluetooth connections

### Bluetooth security initiator

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
Bluetooth Security is disabled by default and must be configured and enabled before use.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set Bluetooth I/O Capabilities to Display Yes/No (2)   |          `AT+UBTIOC=2` |  |
| 2 | Set Only allow authenticated bonding with encrypted Bluetooth link (3)| `AT+UBTBSM=3` |  |
| 3 | Allow Pairing| `AT+UBTPM=1` |  |
| 4 | Bluetooth Bond| `AT+UBTB=BBBBBBBBBBBBp` |  |
| 5 | Bluetooth Connected event |  | `+UEBTC:0,BBBBBBBBBBBBp` |
| 6 | Bluetooth User Confirmation event, check the number on both devices, should be the same| | `+UEBTUC:BBBBBBBBBBBBp,786920` |
| 7 | Bluetooth User Confirmation, confirm with yes| `AT+UBTUC=BBBBBBBBBBBBp,1` |  |
| 8 | Bluetooth Bond success | | `+UEBTB:BBBBBBBBBBBBp,0` |
| 9 | Bluetooth Bonded Devices List (optional) | `AT+UBTBDL` | `+UBTBDL:BBBBBBBBBBBBp` |

### Bluetooth security responder

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
Bluetooth Security is disabled by default and must be configured and enabled before use.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled, **2: Peripheral** or **3: Central and Peripheral**, if so move to step 6   | `AT+UBTM?`     |   `+UBTM:2` or `+UBTM:3`         |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-W36 to startup | | `+STARTUP` |
| 6 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 7 | Set Bluetooth I/O Capabilities to Display Yes/No (2)   |          `AT+UBTIOC=2` |  |
| 8 | Set Only allow authenticated bonding with encrypted Bluetooth link (3)| `AT+UBTBSM=3` |  |
| 9 | Allow Pairing| `AT+UBTPM=1` |  |
| 10 | Bluetooth Connected event |  | `+UEBTC:0,AAAAAAAAAAAAp` |
| 11 | Bluetooth User Confirmation event, check the number on both devices, should be the same| | `+UEBTUC:AAAAAAAAAAAAp,786920` |
| 12 | Bluetooth User Confirmation, confirm with yes| `AT+UBTUC=AAAAAAAAAAAAp,1` |  |
| 13 | Bluetooth Bond success | | `+UEBTB:AAAAAAAAAAAAp,0` |
| 14 | Bluetooth Bonded Devices List (optional) | `AT+UBTBDL` | `+UBTBDL:AAAAAAAAAAAAp` |

# Wi-Fi Connection Use Cases

The following Wi-Fi use cases show basic connectivity functionality to get started with Wi-Fi Station and Access Point connections.

The following examples use the MAC address below, this must be replaced by the real MAC address of the devices that are used.

- Station MAC address: AAAAAAAAAAAA
- Access Point MAC address: BBBBBBBBBBB

## Wi-Fi station WPA2 and WPA3

![wi-fi-ap](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)
![wi-fi-station](https://content.u-blox.com/sites/default/files/2024-02/wi-fi-station.png)

Connect as a Wi-Fi station to an Access Point to get access to network.

This use case connects NORA-W36 as a Wi-Fi station to an Access Point for access to the network. The connection is set to **DHCP client** by default.

To use static IP the `AT+UWSIPS` set the IP address, gateway, subnet mask and DNS.

## WPA2/WPA3 security overview

The NORA-W36 module supports both **WPA2 Personal** and **WPA3 Personal** security protocols when operating as a Wi-Fi station, providing enhanced wireless network protection:

| Security Protocol | Encryption | Key Benefits | Use Cases |
|---|---|---|---|
| **WPA2 Personal** | AES-CCMP | Industry standard, broad compatibility | Legacy networks, mixed environments |
| **WPA3 Personal** | AES-CCMP/GCMP-256 | Enhanced security, forward secrecy, SAE protection | Modern secure networks, IoT applications |

**WPA3 Security Enhancements (Station Mode Only):**

- **SAE (Simultaneous Authentication of Equals)**: Stronger password-based authentication
- **Forward Secrecy**: Previous session keys remain secure even if password is compromised
- **Enhanced Protection**: Resistant to offline dictionary attacks
- **Improved Handshake**: More robust authentication process

**Note:** WPA3 support is available for **station mode only**. When operating as an Access Point, NORA-W36 supports **WPA2 Personal only**.

## Station connection configuration

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set SSID for the Network                  | `AT+UWSCP=0,"ssid"`               | `OK` |
| 2a | Set Password (WPA2/WPA3 compatible)       | `AT+UWSSW=0,"password",0`         | `OK` |
| 2b | Set Password (WPA3 only)                  | `AT+UWSSW=0,"password",1`         | `OK` |
| 3 | Connect Wi-Fi station                     | `AT+UWSC=0`                      | `OK` |
| 4 | Wait for Wi-Fi interface                  |                                   | `+UEWLU:0,BBBBBBBBBBB,6` |
| 5 | Wait for Network interface                |                                   | `+UEWSNU` |
| 6 | Check IP address (optional)               | `AT+UWSNST?`                     | `+UWSNST:0,192.168.1.179` etc. |
| 7 | Check RSSI (optional)                     | `AT+UWSST=4`                     | `+UWSST:4,-66` |
| 8 | It is now possible to connect [TCP](#wi-fi-tcp-client) and [UDP](#wi-fi-udp-client), and then send and receive data in [String](#string-mode) or [Binary](#binary-mode) mode. It is also possible to connect [MQTT](#mqtt-use-cases). |  |  |
| 9 | Disconnect Wi-Fi station                  | `AT+UWSDC`                       | `OK` |

## Wpa security parameter details

**`AT+UWSSW` Command Format:**
```
AT+UWSSW=<interface_id>,<password>,<wpa_threshold>
```

**Parameters:**
- `interface_id`: Wi-Fi interface (0 = station)
- `password`: WPA/WPA2/WPA3 password (8-63 characters)
- `wpa_threshold`: Security level selection
  - `0`: Accept WPA2 or higher (WPA2/WPA3 compatible)
  - `1`: Require WPA3 only (enhanced security)

**Security Recommendations:**
- Use `wpa_threshold=1` for WPA3-only networks requiring maximum security
- Use `wpa_threshold=0` for broader compatibility with WPA2/WPA3 networks
- Ensure password meets complexity requirements (minimum 8 characters)

**Important Note**: If NORA-W36 should connect to Wi-Fi at startup, the **Connect, Store** and **Reset** commands should be sent: `AT+UWSC=0`, `AT&W` and `AT+CPWROFF`. **The current Wi-Fi Station state is stored in flash** and NORA-W36 will try to connect using the Service Set Identifier (SSID) and password stored at startup.

## Wi-Fi station command reference

The following section provides detailed documentation for key Wi-Fi station commands using the standardized format:

#### AT+uwscp - Wi-Fi station connection parameters

**Purpose:** Configure SSID for Wi-Fi station connection

**Syntax:**
```
AT+UWSCP=<interface_id>,<ssid>
```

**Parameters:**
- `interface_id`: Wi-Fi interface ID (0 = station)
- `ssid`: Network SSID name (1-32 characters, quoted string)

**Examples:**
```
AT+UWSCP=0,"MyNetwork"             // Set SSID to "MyNetwork"
AT+UWSCP=0,"Office_WiFi_5G"        // Set SSID with special characters
```

**Response:** `OK` on success, `ERROR` on failure

**Notes:**
- Channel selection is automatic during connection
- Settings can be stored with `AT&W` followed by `AT+CPWROFF` to ensure safe flash storage

#### AT+uwssw - Wi-Fi station security/password

**Purpose:** Set WPA/WPA2/WPA3 password and security threshold

**Syntax:**
```
AT+UWSSW=<interface_id>,<password>,<wpa_threshold>
```

**Parameters:**
- `interface_id`: Wi-Fi interface ID (0 = station)
- `password`: WPA password (8-63 characters, quoted string)
- `wpa_threshold`: Security level
  - `0`: Accept WPA2 or higher (recommended for compatibility)
  - `1`: Require WPA3 only (enhanced security)

**Examples:**
```
AT+UWSSW=0,"MyPassword",0          // WPA2/WPA3 compatible
AT+UWSSW=0,"SecurePass123",1       // WPA3 only
```

**Response:** `OK` on success, `ERROR` on invalid parameters

#### AT+uwsc - Wi-Fi station connect

**Purpose:** Initiate connection to configured Wi-Fi network

**Syntax:**
```
AT+UWSC=<interface_id>
```

**Parameters:**
- `interface_id`: Wi-Fi interface ID (0 = station)

**Example:**
```
AT+UWSC=0
```

**Response:**
- `OK` - Connection process started
- `+UEWLU:0,<mac_address>,<channel>` - Wi-Fi link established
- `+UEWSNU` - Network interface ready

**Common Errors:**
- `ERROR:1` - Invalid parameters
- `ERROR:8` - Connection timeout
- `ERROR:16` - Authentication failed

#### AT+uwsdc - Wi-Fi station disconnect

**Purpose:** Disconnect from current Wi-Fi network

**Syntax:**
```
AT+UWSDC[=<interface_id>]
```

**Parameters:**
- `interface_id`: Optional Wi-Fi interface ID (default: 0)

**Example:**
```
AT+UWSDC
```

**Response:** `OK` on success

## Wi-Fi station troubleshooting

#### Common connection issues

| Issue | Symptoms | Possible Causes | Solutions |
|-------|----------|-----------------|-----------|
| Authentication failure | `ERROR` on `AT+UWSC=0` | Wrong password, unsupported security | Verify password, check WPA mode support |
| Connection timeout | Command hangs, no `+UEWLU` | Weak signal, network issues | Check RSSI with `AT+UWSST=4`, move closer to AP |
| No IP address | `+UEWLU` received but no `+UEWSNU` | DHCP issues, network config | Check router DHCP settings, try static IP |
| Frequent disconnections | Intermittent connectivity | Signal interference, power save | Disable power save, check for interference |

#### Debug commands

| Command | Purpose | Example Response |
|---------|---------|------------------|
| `AT+USYEE=1` | Enable extended error codes | `OK` |
| `AT+USYEC?` | Check last error code | `+USYEC:16` (auth failed) |
| `AT+UWSST=4` | Check signal strength | `+UWSST:4,-65` (RSSI in dBm) |
| `AT+UWSNST?` | Check network status | `+UWSNST:0,192.168.1.179` + more params |
| `AT+UWSSC` | Scan for Wi-Fi networks | `+UWSSC:<bssid>,<ssid>,<channel>,<rssi>,...` |

#### Step-by-step troubleshooting

1. **Test Basic Communication**
   ```
   AT
   OK
   ```

2. **Enable Extended Errors**
   ```
   AT+USYEE=1
   OK
   ```

3. **Check Current Configuration**
   ```
   AT+UWSCP=0
   +UWSCP:0,"MyNetwork"
   ```

4. **Verify Signal Strength**
   ```
   AT+UWSST=4
   +UWSST:4,-45          // Good signal (-30 to -50 dBm)
   ```

5. **Test Connection**
   ```
   AT+UWSC=0
   OK
   // Wait for events...
   ```

6. **If Connection Fails, Check Error**
   ```
   AT+USYEC?
   +USYEC:16     // Error code 16 = Authentication failed
   ```

## Wi-Fi PEAP enterprise security

![wi-fi-ap](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)
Connect as a Wi-Fi station to an Access Point using PEAP (Protected Extensible Authentication Protocol) and a RADIUS server to get access to network.

This use case connects NORA-W36 as a Wi-Fi station to an Access Point for access to the network. The connection is set to **DHCP client** by default.


<!--- ![wi-fi-station](https://content.u-blox.com/sites/default/files/2024-02/wi-fi-station.png)
--->

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set SSID for the Network                  | `AT+UWSCP=0,"NORA-W36 Access Point"`               | `OK` |
| 2 | Set the User and Password with TLS 1.3    | `AT+UWSSP=0,2,"peap_user_name","peap_password"`            | `OK` |
| 3 | Connect Wi-Fi station           | `AT+UWSC=0`                         | `OK` |
| 4 | Wait for Wi-Fi interface        |                                   | `+UEWLU:0,BBBBBBBBBBB,6` |
| 5 | Wait for Network interface        |                                   | `+UEWSNU` |
| 6 | Check IP address (optional)                | `AT+UWSNST=0`                         | `+UWSNST:0,192.168.1.179` |
| 7 | Check RSSI (optional)                        | `AT+UWSST=4`                        | `+UWSST:4,-66` |
| 8 | It is now possible to connect [TCP](#wi-fi-tcp-client) and [UDP](#wi-fi-udp-client), and then send and receive data in [String](#string-mode) or [Binary](#binary-mode) mode. It is also possible to connect [MQTT](#mqtt-use-cases). |  |  |
| 9 | Disconnect Wi-Fi station                  | `AT+UWSDC`                       | `OK` |

**Important Note**: If NORA-W36 should connect to Wi-Fi at startup the **Connect, Store** and **Reset** should be sent, `AT+UWSC=0`, `AT&W` and `AT+CPWROFF`, **the current Wi-Fi Station state is stored in flash** and NORA-W36 will try to connect using Service Set Identifier (SSID) and password stored at startup.

## Wi-Fi EAP-TLS enterprise security

![wi-fi-ap](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)
Connect as a Wi-Fi station to an Access Point using Extensible Authentication Protocol (EAP) and EAP Transport Layer Security (EAP-TLS) to get access to network.

This use case connects NORA-W36 as a Wi-Fi station to an Access Point for access to the network. The connection is set to **DHCP client** by default.

To use static IP the `AT+UWSIPS` set the IP address, gateway, subnet mask and DNS.

<!---![wi-fi-station](https://content.u-blox.com/sites/default/files/2024-02/wi-fi-station.png)
--->

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Write X.509 certificate and private key using [Binary data](#simple-binary-data-example) | `AT+USECUB=0,"ca.pem"{binary_content}` + `AT+USECUB=1,"client.pem"{binary_content}` + `AT+USECUB=2,"client.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 2 | Set SSID for the Network                  | `AT+UWSCP=0,"NORA-W36 Access Point"`               | `OK` |
| 3 | Set the certificates and key with TLS 1.3    | `AT+UWSSE=0,2,"ca.pem","client.pem","client.key"`            | `OK` |
| 4 | Connect Wi-Fi station           | `AT+UWSC=0`                         | `OK` |
| 5 | Wait for Wi-Fi interface        |                                   | `+UEWLU:0,BBBBBBBBBBB,6` |
| 6 | Wait for Network interface        |                                   | `+UEWSNU` |
| 7 | Check IP address (optional)                | `AT+UWSNST=0`                         | `+UWSNST:0,192.168.1.179` |
| 8 | Check RSSI (optional)                        | `AT+UWSST=4`                        | `+UWSST:4,-66` |
| 9 | It is now possible to connect [TCP](#wi-fi-tcp-client) and [UDP](#wi-fi-udp-client), and then send and receive data in [String](#string-mode) or [Binary](#binary-mode) mode. It is also possible to connect [MQTT](#mqtt-use-cases). |  |  |
| 10 | Disconnect Wi-Fi station                  | `AT+UWSDC`                       | `OK` |

**Important Note**: If NORA-W36 should connect to Wi-Fi at startup the **Connect, Store** and **Reset** should be sent, `AT+UWSC=0`, `AT&W` and `AT+CPWROFF`, **the current Wi-Fi Station state is stored in flash** and NORA-W36 will try to connect using Service Set Identifier (SSID) and password stored at startup.

**TLS Version Options for EAP-TLS:**
The second parameter in `AT+UWSSE` specifies the TLS version:
- `0`: Disable TLS (not recommended for EAP-TLS)
- `1`: TLS 1.2 only
- `2`: TLS 1.3 only (recommended for enhanced security)
- `3`: TLS 1.2 or 1.3 (negotiate highest available)

**Security Recommendation**: Use TLS 1.3 (parameter `2`) for the strongest security posture, as it provides improved encryption algorithms, forward secrecy, and reduced handshake latency.


## Wi-Fi access point WPA2

![wi-fi-ap](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)
This use case configures NORA-W36 to act as a Wi-Fi Access Point that allows Wi-Fi Stations to connect, send, and receive data to the module.

The Wi-Fi connection has **WPA2** encryption and a **DHCP server** that automatically assigns IP addresses to devices when they connect to the network.

The server assigns connected devices with IP addresses from 192.168.1.100 + x, where 'x' represents the additional IP addresses that can be assigned to other devices connected to the network.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set the SSID and select network channel to 6 to define the frequency band   | `AT+UWAPCP="NORA-W36 Access Point",6`               | `OK` |
| 2 | Set the Password, using WPA2      | `AT+UWAPSW="mypassword"`            | `OK` |
| 3 | Activate the Wi-Fi Access point. DHCP Server is enabled by default    | `AT+UWAPA`                        | `OK` |
| 4 | Wait for Access Point        |                                   | `+UEWAPU` |
| 5 | Wait for Network interface        |                                   | `+UEWAPNU` |
| 6 | Check the IP address of the AP (optional)        | `AT+UWAPNST=0`    | `+UWAPNST:0,192.168.1.80` |
| 7 | Station connected            |                    | `+UEWAPSA:AAAAAAAAAAAA`  |
| 8 | It is now possible to connect over [TCP](#wi-fi-tcp-client) and [UDP](#wi-fi-udp-client), and then send and receive data in [String](#string-mode) or [Binary](#binary-mode) mode. It is also possible to connect [MQTT](#mqtt-use-cases). |  |  |
| 9 | Station disconnect            |                    | `+UEWAPSDA:AAAAAAAAAAAA`  |
| 10 | Deactivate Wi-Fi Access Point           |    `AT+UWAPD`        | `OK` |

**Note:** If NORA-W36 activates Wi-Fi Access Point at startup, **Activate** (`AT+UWAPA`), **Store** (`AT&W`) and  **Reset** (`AT+CPWROFF`) commands should be sent. The current Wi-Fi Access Point state is  stored in flash and NORA-W36 then activates the Access Point using the stored SSID and password at startup.
IP address range is 192.168.1.100 + x to connected stations.


## Access point security details

**Security Limitation:** Access Point mode supports **WPA2 Personal only**. WPA3 is not supported when operating as an Access Point.

**`AT+UWAPSW` Command Format:**
```
AT+UWAPSW=<password>
```

**Parameters:**
- `password`: WPA2 password (8-63 characters)

**Security Features:**
- **WPA2 Personal**: Industry-standard security with AES-CCMP encryption
- **Password Protection**: 8-63 character password requirement
- **DHCP Server**: Automatic IP address assignment for connected devices

# Wi-Fi Security Configuration

This chapter provides comprehensive security guidance for NORA-W36 implementation in production environments, covering wireless security, encryption protocols, certificate management, and operational security considerations.

## Wireless security configuration

## Wi-Fi security protocol selection

**Recommended Security Hierarchy (Best to Acceptable):**

| Priority | Security Mode | Use Case | Implementation |
|----------|---------------|----------|----------------|
| **1st** | **WPA3 Personal** | New deployments, high-security IoT | `AT+UWSSW=0,"password",1` |
| **2nd** | **WPA2/WPA3 Compatible** | Mixed environments, broader compatibility | `AT+UWSSW=0,"password",0` |
| **3rd** | **EAP-TLS Enterprise** | Corporate networks, certificate-based | `AT+UWSSE=0,2,"ca.pem","client.pem","client.key"` |
| **4th** | **PEAP Enterprise** | Corporate networks, username/password | `AT+UWSSP=0,2,"username","password"` |
|  **Avoid** | **Open Networks** | Never use in production | Not recommended |

## Password security standards

**WPA/WPA2/WPA3 Password Requirements:**

✅ **Strong Password Criteria:**
- **Minimum 12 characters** (8 is technical minimum, 12+ recommended)
- **Mixed case letters** (A-Z, a-z)
- **Numbers** (0-9)
- **Special characters** (!@#$%^&*)
- **Avoid dictionary words** and predictable patterns

**Examples:**
```bash
// Weak passwords (avoid)
AT+UWSSW=0,"password",0            // Dictionary word
AT+UWSSW=0,"12345678",0            // Sequential numbers
AT+UWSSW=0,"CompanyName",0         // Predictable

// Strong passwords (recommended)
AT+UWSSW=0,"Mx7$kL2@Rt9!uP",0      // Random strong password
AT+UWSSW=0,"BlueTree#2024$IoT",0             // Memorable but complex
```

## Network architecture security

**Station Mode Security:**
- ✅ **Use WPA3** when available (`wpa_threshold=1`)
- ✅ **Verify network authenticity** before connecting
- ✅ **Monitor signal strength** to detect rogue APs
- ✅ **Implement connection timeouts** to prevent hanging

**Access Point Mode Security:**
- ✅ **Change default SSID** from "NORA-W36"
- ✅ **Use complex passwords** (12+ characters)
- ✅ **Limit connected devices** (max 5 stations)
- ✅ **Monitor connected devices** with `+UEWAPSA` events
- ✅ **Regular password rotation** in production

## TLS/SSL security implementation

## TLS version configuration

** TLS Security Layer Architecture:**

```
    ┌─────────────    ┌─────────────    ┌─────────────
    │🛡 TLS 1.3   │ ── │🔒 TLS 1.2   │ ── │⚠ No TLS    │
    │   (Best)    │    │ (Legacy)    │    │  (Never!)   │
    └─────────────┘    └─────────────┘    └─────────────┘
           │                     │                     │
      Max Security         Good Security         No Security

    🔧 TLS 1.3 Benefits:    🔧 TLS 1.2 Support:    ⚠ Security Risk:

- • Forward secrecy      • Legacy compatibility  • Plain text data
- • 0-RTT handshake      • Proven stability      • No encryption
- • Modern encryption    • Wide support          • Vulnerable to attacks

```

**TLS Security Hierarchy:**

| Priority | TLS Version | Parameter | Use Case | Security Level |
|----------|-------------|-----------|----------|----------------|
| **1st** | **TLS 1.3** | `2` | New implementations, maximum security | 🛡 Highest |
| **2nd** | **TLS 1.2/1.3** | `3` | Transition period, server compatibility | 🔒 High |
| **3rd** | **TLS 1.2** | `1` | Legacy server support only | ⚠ Medium |
|  **Never** | **No TLS** | `0` | Never use for secure connections | 🚫 None |

**Implementation Examples:**
```bash
// Best: TLS 1.3 only (recommended for new projects)
AT+USOTLS=0,2            // Socket TLS 1.3
AT+UMQTLS=0,2            // MQTT TLS 1.3
AT+UHTCTLS=0,2           // HTTP TLS 1.3

// Good: TLS 1.2/1.3 compatible (legacy support)
AT+USOTLS=0,3            // Negotiate highest available
```

## Certificate management security

**Certificate Security Best Practices:**

✅ **Certificate Validation:**
- **Always validate server certificates** in production
- **Use complete certificate chains** (CA + intermediate + server)
- **Verify certificate expiration dates** before deployment
- **Test certificate chain validity** with openssl

✅ **Certificate Storage:**
- **Limit certificate lifetime** (1-2 years maximum)
- **Use secure certificate sources** (trusted CAs only)
- **Monitor certificate expiration** (automated renewal)
- **Remove unused certificates** to free storage

**Certificate Upload Security:**
```bash
// Upload complete certificate chain
AT+USECUB=0,"ca.pem"{binary_ca_cert}         // Root CA
AT+USECUB=1,"intermediate.pem"{binary_int_cert}    // Intermediate CA
AT+USECUB=2,"client.pem"{binary_client_cert}    // Client certificate
AT+USECUB=3,"client.key"{binary_private_key}    // Private key (secure!)
```

**Certificate Validation Commands:**
```bash
// List all certificates
AT+USECL?

// Verify specific certificate details
AT+USECD="ca.pem"

// Remove expired certificates
AT+USECR=1,"expired_cert.pem"
```

## TLS extensions security

**Recommended TLS Extension Configuration:**

```bash
// Enable Server Name Indication (SNI) - Required for modern TLS
AT+USETE0=1      // Enable SNI (default: enabled)

// Enable Handshake Fragmentation - Prevents MTU issues
AT+USETE1=1      // Enable fragmentation (default: enabled)

// Store TLS extension settings
AT&W             // Persist configuration
AT+CPWROFF       // Reset to apply stored settings safely
```

## Application protocol security

## MQTT security configuration

**Comprehensive MQTT Security Setup:**

```bash
// Secure connection with TLS 1.3
AT+UMQCP=0,"secure-mqtt-broker.com",8883
AT+UMQTLS=0,2,"ca.pem","client.pem","client.key"

// Strong authentication (set connection parameters with credentials)
AT+UMQCP=0,"mqtt.broker.com",8883,"device_id_12345","device_id_12345","complex_password_67890"

// Connect securely
AT+UMQC=0
```

**MQTT Security Checklist:**
- ✅ **Always use port 8883** (TLS) instead of 1883 (plain)
- ✅ **Implement client certificates** for mutual authentication
- ✅ **Use unique client IDs** to prevent conflicts
- ✅ **Avoid predictable topics** (use device-specific prefixes)
- ✅ **Implement message encryption** for sensitive data
- ✅ **Monitor connection events** for security anomalies

## HTTP/HTTPS security configuration

**Secure HTTP Implementation:**

```bash
// Always use HTTPS (port 443)
AT+UHTCCP=0,"api.secure-service.com",443
AT+UHTCTLS=0,2,"ca.pem"

// Add security headers
AT+UHTCRHAF=0,"Authorization","Bearer secure_token_here"
AT+UHTCRHAF=0,"User-Agent","NORA-W36/3.2.0"
AT+UHTCRHAF=0,"Content-Type","application/json"

// Make secure request
AT+UHTCRG=0,"/api/v1/secure-endpoint"
```

**HTTP Security Checklist:**
- ✅ **Always use HTTPS** (never HTTP for sensitive data)
- ✅ **Validate SSL certificates**
- ✅ **Use proper authentication** (tokens, API keys)
- ✅ **Implement request timeouts**
- ✅ **Validate response status codes**
- ✅ **Sanitize response data**

## Operational security practices

## Device configuration security

**Secure Configuration Management:**

```bash
// Change default settings
AT+UWAPCP="SecureIoTGateway_001",6           // Unique SSID
AT+UWAPSW="ComplexPassword#2024$"            // Strong password

// Enable extended error reporting (development only)
AT+USYEE=1       // Enable during development
AT+USYEE=0       // Disable in production (security through obscurity)

// Store secure configuration
AT&W             // Save to flash
AT+CPWROFF       // Reset to apply stored settings safely

// Test configuration
AT+UWSNST=0      // Verify network status
AT+UWSSC         // List available networks
```

## Power management security

**Secure Power Save Configuration:**

```bash
// Balance security and power efficiency
AT+UPMPSL=1      // Enable moderate power save
AT+UPMPSTO=5000          // 5-second timeout (balance responsiveness/power)
AT&W             // Store settings
AT+CPWROFF       // Reset to apply stored settings safely

// Security consideration: Ensure power save doesn't impact security monitoring
```

## Monitoring and diagnostics

**Security Monitoring Commands:**

```bash
// Regular security health checks
AT+UWSST=4       // Monitor signal strength (detect rogue APs)
AT+UWSNST=0      // Verify network connection status, only IPv4 Address
AT+USECL?        // Check certificate validity
AT+USYEC?        // Check for error conditions
AT+UWSNST?       // Verify network connection status, all parameters
```

## Security incident response

## Connection security issues

**Rapid Response Commands:**

| Security Event | Immediate Action | Command |
|----------------|------------------|---------|
| **Suspicious connection** | Disconnect immediately | `AT+UWSDC` |
| **Authentication failure** | Check credentials, reset if needed | `AT+USYEC?` → reconfigure |
| **Certificate error** | Verify and reload certificates | `AT+USECL?` → `AT+USECR` → reload |
| **Weak signal** | Check for interference/rogue AP | `AT+UWSST=4` |
| **Connection timeout** | Reset network configuration | `AT+UWSDC` → reconfigure |

## Security audit checklist

**Regular Security Review (Monthly):**

- [ ] **Password strength audit** - verify all passwords meet current standards
- [ ] **Certificate expiration check** - ensure all certificates valid for next 30 days
- [ ] **TLS version compliance** - confirm TLS 1.3 usage where possible
- [ ] **Access point security** - verify WPA3 usage and strong passwords
- [ ] **Connection monitoring** - review unusual connection patterns
- [ ] **Firmware currency** - ensure latest security patches applied
- [ ] **Configuration backup** - secure backup of device configurations

**Security Configuration Validation:**
```bash
// Complete security status check
AT+UWSCP=0       // Verify SSID configuration
AT+UWSS=0        // Check security configuration
AT+USECL?        // List all certificates and expiration
AT+USYEC?        // Check for any error conditions
```

This comprehensive security framework ensures NORA-W36 deployments maintain the highest security standards while remaining operationally efficient.

# Wi-Fi Performance Optimization

This chapter provides comprehensive performance optimization guidance for NORA-W36 deployments, covering connection optimization, power efficiency, memory management, and throughput enhancement techniques for maximum system performance.

## Connection performance optimization

## Wi-Fi connection speed enhancement

**Fast Connection Techniques:**

| Optimization | Implementation | Performance Impact | Command Example |
|--------------|----------------|-------------------|-----------------|
| **Pre-scan networks** | Scan before connecting | 2-3 seconds faster | `AT+UWSSC` |
| **Channel optimization** | Use specific SSID only | 1-2 seconds faster | `AT+UWSCP=0,"MyAP"` |
| **Aggressive power save** | Disable during connection | 1-3 seconds faster | `AT+UPMPSL=0` (temporarily) |
| **DHCP timeout tuning** | Reduce DHCP wait time | 2-5 seconds faster | System automatic |

**Optimal Connection Sequence:**
```bash
// Disable power save during connection (faster scanning)
AT+UPMPSL=0

// Scan for target network (get channel info)
AT+UWSSC

// Connect with specific parameters
AT+UWSCP=0,"TargetNetwork"         // Set SSID (channel determined by AP)

// Verify connection quickly
AT+UWSNST=0

// Re-enable power save after connection
AT+UPMPSL=1
```

## Socket performance tuning

**TCP Socket Optimization:**

```bash
// Enable TCP fast recovery
AT+USORS=0,1000          // Read available data (1kB chunks)

// Use larger receive operations for bulk data
AT+USORS=0,1000          // 1kB chunks for file transfers

// Monitor socket status for optimal timing
AT+USYEE=1       // Enable extended error reporting
```

**UDP Performance Configuration:**
```bash
// UDP is inherently faster - optimize for your use case
AT+USORS=0,1000          // Standard read operations
```

## TLS performance enhancement

**TLS Handshake Optimization:**

| TLS Version | Handshake Time | Security Level | Recommended Use |
|-------------|---------------|----------------|-----------------|
| **TLS 1.3** | ~2-3 seconds | Highest | New deployments |
| **TLS 1.2** | ~3-4 seconds | High | Legacy compatibility |
| **TLS 1.2/1.3 Auto** | ~2-4 seconds | High | Mixed environments |

**TLS Performance Commands:**
```bash
// Fastest: TLS 1.3 with session resumption
AT+USOTLS=0,2            // TLS 1.3 for new connections
AT+USETE1=1      // Enable handshake fragmentation (faster on slow networks)
AT+USETE0=1      // Enable SNI (required for many servers)

// Pre-load certificates for faster handshake
AT+USECL?        // Verify certificates are already loaded
```

## Power vs performance trade-offs

## Power save mode optimization

**⚡ Power Management Decision Matrix:**

```
    ┌─────────────    ┌─────────────    ┌─────────────
    │🚀 High Perf │ ── │⚖ Balanced  │ ── │🔋 Low Power │
    │ Mode 0      │    │  Mode 1     │    │  Mode 2     │
    └─────────────┘    └─────────────┘    └─────────────┘
           │                     │                     │
      Max Speed            Good Balance          Max Battery

    ⚡ Performance:         ⚖ Balanced:          🔋 Power Saving:

- • No delays            • Smart trade-offs    • Extended battery
- • Instant response     • Good responsiveness • Ideal for IoT
- • High throughput      • Moderate power      • Periodic updates

```

**Power Save Performance Matrix:**

| Power Mode | Power Consumption | Response Time | Throughput | Best Use Case |
|------------|------------------|---------------|-------------|---------------|
| **🚀 Disabled (0)** | High | Instant | Maximum | High-throughput streaming |
| **⚖ Light (1)** | Medium | Medium | Good | Real-time communications |
| **🔋 Moderate (2)** | Low | Long | Reduced | Periodic data updates |

**Adaptive Power Management:**

> **💡 Timeout Logic**: High-performance mode uses longer timeouts to maintain sustained operation without frequent power state changes. IoT sensors use shorter timeouts for quick wake-up and responsiveness to events.

```bash
// High performance mode (data streaming)
AT+UPMPSL=0      // Disable power save
AT+UPMPSTO=30000         // Long timeout (30 seconds) for sustained performance

// Balanced mode (regular operations)
AT+UPMPSL=1      // Light power save
AT+UPMPSTO=5000          // 5-second timeout

// Power efficient mode (IoT sensors)
AT+UPMPSL=2      // Moderate power save
AT+UPMPSTO=1000          // Short timeout (1 second) for quick responsiveness

// Save configuration
AT&W
AT+CPWROFF       // Reset to apply stored settings safely
```

## Dynamic power scaling

**Context-Aware Power Management:**

```bash
// During active data transfer - maximum performance
AT+UPMPSL=0      // Disable power save

// After transfer complete - enable power save
AT+UPMPSL=1      // Light power save for quick response

// During idle periods - deep power save
AT+UPMPSL=2      // Moderate power save

// Example: Automatic switching based on socket activity
// (implement in host application logic)
```

## Memory management optimization

## Efficient memory usage

**Memory Allocation Best Practices:**

| Resource | Optimal Size | Performance Impact | Command |
|----------|-------------|-------------------|---------|
| **Socket Operations** | 1KB for bulk data | Higher throughput | `AT+USORS=0,1000` |
| **Certificate Storage** | Minimize certificates | Faster boot/connection | `AT+USECL?` |
| **Connection Management** | Regular monitoring | Prevents issues | `AT+UWSNST=0` |

**Memory Monitoring Commands:**
```bash
// Check certificate usage
AT+USECL?        // List certificates and sizes

// Remove unused certificates
AT+USECL?        // List certificates
AT+USECR=0,"old_cert.pem"          // Remove unused certificates

// Remove unused certificates to free storage
AT+USECR=0,"unused.pem"            // Remove unused certificates
```

## Data handling efficiency

**Optimal Data Transfer Guidelines:**

```bash
// For socket operations, use appropriate read/write sizes
// Socket commands will be covered in Wi-Fi Sockets section
// Focus on connection optimization and certificate management
```

## Network performance optimization

## Wi-Fi signal quality management

**Signal Strength Optimization:**

| Signal Strength (RSSI) | Performance Level | Recommended Action |
|------------------------|-------------------|-------------------|
| **-30 to -50 dBm** | Excellent | Maintain current position |
| **-50 to -70 dBm** | Good | Monitor for degradation |
| **-70 to -85 dBm** | Fair | Consider repositioning |
| **Below -85 dBm** | Poor | Reposition or use repeater |

**Signal Monitoring Commands:**
```bash
// Check current signal strength
AT+UWSST=4       // Signal strength in dBm

// Monitor connection quality
AT+UWSNST=0      // Network status and quality

// Scan for alternative networks
AT+UWSSC         // Scan and compare signal levels
```

## Network congestion management

**Channel Optimization Strategy:**

```bash
// Scan all channels to find optimal one
AT+UWSSC

// Example: Choose less congested channel
// If scan shows:

-                // Channel 1: Many APs (congested)
-                // Channel 6: Few APs (better choice)
-                // Channel 11: Few APs (best choice)


// Configure network (channel determined by AP)
AT+UWSCP=0,"MyNetwork"             // Set SSID
```

## Application-level performance

## Protocol selection guidelines

**Performance Comparison by Protocol:**

| Protocol | Latency | Throughput | Overhead | Best Use Case |
|----------|---------|------------|----------|---------------|
| **UDP** | Lowest | Highest | Minimal | Real-time data, streaming |
| **TCP** | Low | High | Low | Reliable data transfer |
| **TLS/TCP** | Medium | Medium | Medium | Secure communications |
| **HTTP/HTTPS** | High | Medium | High | API calls, web services |
| **MQTT** | Medium | Medium | Low | IoT messaging, pub/sub |

## Data format optimization

**Efficient Data Formats:**

```bash
// JSON (human readable, moderate efficiency)
{"temp":23.5,"hum":65,"time":1640995200}

// Compact JSON (remove spaces, shorter keys)
{"t":23.5,"h":65,"ts":1640995200}

// Binary format (highest efficiency)
// Custom binary protocol for maximum performance
// bytes: temperature (float)
// bytes: humidity (float)
// bytes: timestamp (uint32)

// Total: 12 bytes vs 45+ bytes JSON

```

## Real-time performance monitoring

## Performance metrics collection

**Key Performance Indicators:**

```bash
// Connection establishment time
// Measure time between AT+UWSC and +UEWLU event

// Data transfer throughput
// Measure bytes/second during AT+USOWS/AT+USORS operations

// Power consumption monitoring
// Use external current meter with different AT+UPMPSL settings

// Certificate usage tracking
AT+USECL?        // Check certificate storage regularly
```

## Performance benchmarking

**Standardized Performance Tests:**

| Test Type | Measurement | Target Performance | Command Sequence |
|-----------|-------------|-------------------|------------------|
| **Connection Speed** | Time to connect | <10 seconds | `AT+UWSC=0` timing |
| **TCP Throughput** | Bytes per second | >100 KB/s | Large `AT+USOWS` transfers |
| **TLS Handshake** | Handshake time | <5 seconds | `AT+USOTLS` timing |
| **Power Efficiency** | mA consumption | <50mA average | Current measurement |

**Performance Test Sequence:**
```bash
// Baseline connection test
AT+UWSC=0        // Time this command
// Target: <10 seconds to +UEWLU

// Throughput test
AT+USOCR=6       // Create TCP socket
AT+USOC=0,server,port              // Connect
AT+USOWS=0,"data"        // Write data (up to 1000 bytes per command)
// Measure: bytes/second throughput

// Power consumption test
AT+UPMPSL=1      // Enable power save
// Measure current draw over time

// Certificate storage test
AT+USECL?        // Check certificates before/after operations
```

## Performance troubleshooting

## Common performance issues

| Performance Issue | Probable Cause | Solution | Verification |
|-------------------|----------------|----------|-------------|
| **Slow connection** | Weak signal, channel congestion | Reposition, change channel | `AT+UWSST=4` |
| **Low throughput** | Power save mode, small buffers | Disable power save, larger buffers | `AT+UPMPSL=0` |
| **High latency** | Network congestion, DNS delays | Use IP instead of hostnames | `AT+USOC=0,"192.168.1.100",80` |
| **Memory errors** | Certificate/file accumulation | Clean up unused certificates | `AT+USECL?` |

## Performance optimization checklist

**Regular Performance Maintenance:**

| Task | Frequency | Command | Target |
|------|-----------|---------|--------|
| **Signal check** | Weekly | `AT+UWSST=4` | RSSI >-70 dBm |
| **Certificate cleanup** | Monthly | `AT+USECL?` | Remove expired certificates |
| **Power mode verification** | - | - | Confirm appropriate power save settings |
| **Throughput validation** | - | - | Test data transfer speeds match requirements |
| **Certificate monitoring** | Regular | `AT+USECL?` | Check certificate status |
| **Connection timing** | - | - | Verify connection establishment <10 seconds |
| **Error rate monitoring** | Regular | `AT+USYEC?` | Check for increased error rates |

**Optimal Configuration Summary:**
```bash
// High-performance configuration
AT+UPMPSL=0      // Disable power save during operation
AT+USOTLS=0,2            // Use TLS 1.3 for fastest secure connections
AT+USORS=0,1000          // Optimize for 1000-byte MTU limit
AT+USYEE=1       // Enable extended error reporting

// Power-efficient configuration
AT+UPMPSL=1      // Light power save
AT+UPMPSTO=10000         // 10-second timeout
AT+USORS=0,512           // Smaller read operations for efficiency
AT&W             // Save configuration
AT+CPWROFF       // Reset to apply stored settings safely
```

This comprehensive performance framework ensures NORA-W36 implementations achieve optimal speed, efficiency, and reliability across all operating conditions.

# Wi-Fi Sockets use cases

## Wi-Fi TCP client

This use case configures NORA-W36 as a Wi-Fi TCP client device that initiates a TCP connection to a specified server (listener) over a Wi-Fi network. It actively seeks to establish communication by sending a connection request to the server's IP address and port number, which the server is listening on.

The Transmission Control Protocol (TCP) is bidirectional and one socket can both send and receive data:
- `ATE0` turns off the AT command echo to speed up the data transmission in AT mode. The written data is not echoed back to the host, which helps to make the parsing easier.
- It is possible to connect using a host name like `AT+USOC=0,"www.u-blox.com",80` or an IP address `AT+USOC=0,"75.2.60.5",80`
- TCP can both send and receive data between the TCP client and server

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 2 | Connect using TCP port 5003                | `AT+USOC=0,"192.168.0.200",5003`      | `+UESOC:0` |
| 3 | It is now possible to send and receive data using [String](#string-mode) or [Binary](#binary-mode) mode |  |  |
| 4 | Close TCP socket             |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Wi-Fi TCP server (listener)

This use case configures NORA-W36 as a Wi-Fi TCP server (listener) that is configured to accept incoming TCP connections over a Wi-Fi network. It "listens" on a specific IP address and port number for connection requests.
| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 2 | Start TCP server (listener) on port 5003            | `AT+USOL=0,5003`      | `+UESOC:0` |
| 3 | Incoming TCP connection, a new handle 1 to communicate with the connection                |                     | `+UESOIC:0,192.168.1.100,1` |
| 4 | It is now possible to send and receive data using [String](#string-mode) or [Binary](#binary-mode) mode |  |  |
| 5 | TCP connection is closed from remote side          |                   | `+UESOCL:1`  |
| 6 | Close TCP listener            |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Wi-Fi UDP client

Unlike TCP, the User Datagram Protocol (UDP) is not bi-directional. Both an outgoing and incoming socket, `AT+USOCR`, are needed to send and receive data over UDP.
It is possible to connect using the host name, like `AT+USOC=0,"www.u-blox.com",80`, or the IP address `AT+USOC=0,"75.2.60.5",80`


| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a UDP socket                        | `AT+USOCR=17`                        | `+USOCR:0` |
| 2 | Connect using UDP port 5003                | `AT+USOC=0,"192.168.0.200",5003`      |` +UESOC:0` |
| 3 | It is now possible to send data using [String](#string-mode) or [Binary](#binary-mode) mode |  |  |
| 4 | Close UDP socket               |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Wi-Fi UDP server (listener)

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a UDP socket                        | `AT+USOCR=17`                        | `+USOCR:0` |
| 2 | Start UDP server (listener) on port 5003            | `AT+USOL=0,5003`      | `+UESOC:0` |
| 3 | It is now possible to receive data using [String](#string-mode) or [Binary](#binary-mode) mode |  |  |
| 4 | Close UDP listener            |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Wi-Fi TCP using TLS without certificates

TLS Extensions are enabled by default but in some (mostly older) TLS servers they are not supported. See https://www.rfc-editor.org/rfc/rfc6066.html.
The extensions, Server Name, Indication and Maximum Fragment Length Negotiation, are disabled with:
- `AT+USETE0=0` Server Name Indication, 0: Disable - 1: Enable (default)
- `AT+USETE1=0` Maximum Fragment Length Negotiation, 0: Disable - 1: Enable (default)
- All other Extension are disabled and not supported.
- It is possible to use host name like `AT+USOC=0,"www.u-blox.com",80` or using ip address `AT+USOC=0,"75.2.60.5",80` for the connections.

TCP is bidirectional and one socket can both send and receive data.
| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 2 | Add a TLS 1.3 context to a socket                    | `AT+USOTLS=0,2`                         |  |
| 3 | Connect using TCP port 433                | `AT+USOC=0,"www.u-blox.com",433`      | `+UESOC:0` |
| 4 | It is now possible to send data using [String](#string-mode) or [Binary](#binary-mode) mode |  |  |
| 5 | Close TCP socket             |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Wi-Fi TCP using TLS with certificates

TCP is bidirectional and one socket can both send and receive data.
| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Write X.509 certificate and private key using [Binary data](#simple-binary-data-example) | `AT+USECUB=0,"ca.pem"{binary_content}` + `AT+USECUB=1,"client.pem"{binary_content}` + `AT+USECUB=2,"client.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 2 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 3 |Add a TLS 1.3 context to a socket and certificates                        | `AT+USOTLS=0,2,"ca.pem","client.pem","client.key"`                         |  |
| 4 | Connect using TCP on port 433                | `AT+USOC=0,"www.u-blox.com",433`      | `+UESOC:0` |
| 5 | It is now possible to send data using [String](#string-mode) or [Binary](#binary-mode) mode |  |  |
| 6 | Close TCP socket             |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Create own certificates using OpenSSL

This section provides examples for creating your own certificates using OpenSSL (https://www.openssl.org/).
The examples demonstrate how to use **2048-bit** or **4096-bit** key lengths for different security requirements.

**Prerequisites:**
- Use Git Bash (https://git-scm.com/download/win) on Windows
- Or a Linux environment like Ubuntu (https://ubuntu.com/download)
- OpenSSL must be installed and available in PATH

## Certificate authority (CA) creation

**Step 1: Create the root CA private key**

Generate **2048-bit** key size (faster, suitable for most applications):
```bash
openssl genrsa -out ca.key 2048
```

Or generate **4096-bit** key size (higher security, recommended for production):
```bash
openssl genrsa -out ca.key 4096
```

**Step 2: Create the root CA certificate (valid for 1 year)**
```bash
openssl req -x509 -sha256 -new -nodes -key ca.key -days 365 -out ca.pem
```

## Server certificate creation

**Step 3: Create server certificate signing request (CSR)**

For **2048-bit** key:
```bash
openssl req -newkey rsa:2048 -keyout server.key -out server.csr -nodes
```

Or for **4096-bit** key:
```bash
openssl req -newkey rsa:4096 -keyout server.key -out server.csr -nodes
```

**Step 4: Sign server certificate with CA (valid for 1 year)**
```bash
openssl x509 -req -CA ca.pem -CAkey ca.key -in server.csr -out server.pem -days 365 -CAcreateserial
```

## Client certificate creation

**Step 5: Create client certificate signing request (CSR)**

For **2048-bit** key:
```bash
openssl req -newkey rsa:2048 -keyout client.key -out client.csr -nodes
```

Or for **4096-bit** key:
```bash
openssl req -newkey rsa:4096 -keyout client.key -out client.csr -nodes
```

**Step 6: Sign client certificate with CA (valid for 1 years)**
```bash
openssl x509 -req -CA ca.pem -CAkey ca.key -in client.csr -out client.pem -days 365 -CAcreateserial
```

## Testing certificates

**Windows Git Bash Environment:**

Note: `winpty` is required for interactive OpenSSL commands in Git Bash on Windows.

**TLS 1.2 Testing:**
Set up a local TLS 1.2 server:
```bash
winpty openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44330 -tls1_2 -state -Verify 1
```

Connect to the local TLS 1.2 server:
```bash
winpty openssl s_client -connect localhost:44330 -CAfile ca.pem -key client.key -cert client.pem -tls1_2
```

**TLS 1.3 Testing:**
Set up a local TLS 1.3 server:
```bash
winpty openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44331 -tls1_3 -state -Verify 1
```

Connect to the local TLS 1.3 server:
```bash
winpty openssl s_client -connect localhost:44331 -CAfile ca.pem -key client.key -cert client.pem -tls1_3
```

**Linux Environment:**

**TLS 1.2 Testing:**
Set up a local TLS 1.2 server:
```bash
openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44330 -tls1_2 -state -Verify 1
```

Connect to the local TLS 1.2 server:
```bash
openssl s_client -connect localhost:44330 -CAfile ca.pem -key client.key -cert client.pem -tls1_2
```

**TLS 1.3 Testing:**
Set up a local TLS 1.3 server:
```bash
openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44331 -tls1_3 -state -Verify 1
```

Connect to the local TLS 1.3 server:
```bash
openssl s_client -connect localhost:44331 -CAfile ca.pem -key client.key -cert client.pem -tls1_3
```

**Testing Both TLS Versions (Flexible):**
For testing compatibility with both TLS 1.2 and 1.3:
```bash

// Server that accepts both TLS 1.2 and 1.3 (Windows)

winpty openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44332 -state -Verify 1

// Server that accepts both TLS 1.2 and 1.3 (Linux)

openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44332 -state -Verify 1

// Client connecting with version negotiation (will use highest available)

winpty openssl s_client -connect localhost:44332 -CAfile ca.pem -key client.key -cert client.pem    // Windows
openssl s_client -connect localhost:44332 -CAfile ca.pem -key client.key -cert client.pem    // Linux
```

## Certificate verification

**Verify CA certificate key size:**
```bash
openssl x509 -in ca.pem -text -noout | grep "Public-Key"
```
Expected output: `RSA Public-Key: (4096 bit)` or `RSA Public-Key: (2048 bit)`

**Verify client certificate key size:**
```bash
openssl x509 -in client.pem -text -noout | grep "Public-Key"
```
Expected output: `RSA Public-Key: (4096 bit)` or `RSA Public-Key: (2048 bit)`

**Verify client private key size:**
```bash
openssl rsa -in client.key -text -noout | grep "Private-Key"
```
Expected output: `RSA Private-Key: (4096 bit, 2 primes)` or `RSA Private-Key: (2048 bit, 2 primes)`

## Security recommendations

**Key Size Selection:**
- **2048-bit**: Minimum recommended, faster processing, suitable for most IoT applications
- **4096-bit**: Higher security, recommended for production environments with sensitive data

**Certificate Validity:**
- Production certificates should have shorter validity periods (1-2 years)
- Test certificates can use longer periods for convenience

**File Security:**
- Protect private key files (`*.key`) with appropriate file permissions
- Store CA private key securely and offline in production environments
- Consider using hardware security modules (HSM) for critical applications

## Certificate management commands

NORA-W36 provides comprehensive certificate management capabilities for secure storage and administration of X.509 certificates and private keys.

**Certificate Storage Capacity:**
- Maximum 8 certificates (or certificate chains) can be stored simultaneously
- Maximum certificate size: 15,360 bytes per certificate
- Support for PEM format certificates (DER format not supported)

**Certificate Management Commands:**

| Command | Purpose | Example |
|---------|---------|---------|
| `AT+USECL?` | List all stored certificates | Shows all certificate names and types |
| `AT+USECD=<name>` | Show certificate details | `AT+USECD="client.pem"` |
| `AT+USECR=<type>,<name>` | Remove specific certificate | `AT+USECR=1,"client.pem"` |
| `AT+USECR` | Remove all certificates | Clears certificate storage |

**Certificate Types:**
- `0`: Root/CA certificate
- `1`: Client certificate
- `2`: Client private key

**Certificate Operations Examples:**

```bash
// List all stored certificates
AT+USECL?
+USECL:0,"ca-root"
+USECL:1,"device-cert"
+USECL:2,"device-key"

// View certificate details (fingerprint, size, validity dates)
AT+USECD="device-cert"
+USECD:0,A1B2C3D4E5F6...           // Certificate fingerprint (hex)
+USECD:1,2048            // Certificate size in bytes (decimal)
+USECD:2,5F5E1000        // Not valid before: Unix epoch in hex (Jan 1, 2023)
+USECD:3,6586A400        // Not valid after: Unix epoch in hex (Dec 31, 2025)

// Remove specific certificate
AT+USECR=1,"old-client-cert"

// Remove all certificates (factory reset certificates)
AT+USECR
```

**Understanding Certificate Fingerprint:**
The fingerprint (`+USECD:0`) is a SHA-256 hash of the certificate, useful for verification and identification.

**Calculate and Verify Fingerprint with OpenSSL:**
```bash
# Calculate SHA-256 fingerprint using OpenSSL
openssl x509 -noout -fingerprint -sha256 -in ca.pem
```

**Real Example:**
```bash
# NORA-W36 output:
AT+USECD="ca.pem"
+USECD:0,025EF9A024DEF7FCBFD6E3717557C016BCB9C34E6BAA288111D53F9490E06CC2

# OpenSSL verification:
$ openssl x509 -noout -fingerprint -sha256 -in ca.pem
sha256 Fingerprint=02:5E:F9:A0:24:DE:F7:FC:BF:D6:E3:71:75:57:C0:16:BC:B9:C3:4E:6B:AA:28:81:11:D5:3F:94:90:E0:6C:C2
```

**Note:** NORA-W36 returns fingerprint as continuous hex string, while OpenSSL formats with colons.

**Understanding Certificate Date Format:**
- Dates are returned as **hexadecimal Unix epoch timestamps**
- Example: `6586A400` (hex) = `1,703,462,400` (decimal) = `Dec 25, 2023 00:00:00 UTC`
- Conversion: Use online epoch converters or: `date -d @$((0x6586A400))` (Linux/macOS)
- PowerShell: `[DateTimeOffset]::FromUnixTimeSeconds(0x6586A400).DateTime`

**Security Best Practices:**

1. **Regular Certificate Audits**: Use `AT+USECL?` to monitor stored certificates
2. **Certificate Rotation**: Remove expired certificates with `AT+USECR`
3. **Storage Optimization**: Remove unused certificates to free storage space
4. **Validity Monitoring**: Check certificate expiration dates with `AT+USECD`
5. **Backup Strategy**: Keep secure backups of certificates before removal operations

**Certificate Date Format Reference:**

When using `AT+USECD` to check certificate validity dates, the NORA-W36 returns timestamps in **hexadecimal Unix epoch format**:

```bash
AT+USECD="my-certificate"
+USECD:2,61F2D000        // Not valid before: Jan 27, 2022 12:00:00 UTC
+USECD:3,6586A400        // Not valid after:  Dec 25, 2023 00:00:00 UTC
```

**Converting Hex Epoch Timestamps:**

| **Method** | **Command/Code** | **Example** |
|------------|------------------|-------------|
| **Linux/macOS** | `date -d @$((0xHEXVALUE))` | `date -d @$((0x6586A400))` |
| **PowerShell** | `[DateTimeOffset]::FromUnixTimeSeconds(0xHEXVALUE)` | `[DateTimeOffset]::FromUnixTimeSeconds(0x6586A400)` |
| **Python** | `datetime.fromtimestamp(int('HEXVALUE', 16))` | `datetime.fromtimestamp(int('6586A400', 16))` |
| **Online Tools** | Use epoch timestamp converters | Convert `1703462400` to human date |

**Common Epoch Hex Values:**
- `0x61F2D000` = `1,643,289,600` = Jan 27, 2022 12:00:00 UTC
- `0x6586A400` = `1,703,462,400` = Dec 25, 2023 00:00:00 UTC
- `0x677B8000` = `1,736,207,360` = Jan 7, 2025 00:16:00 UTC

**Password-Protected Private Keys:**

NORA-W36 supports AES-encrypted PKCS8 private keys with password protection:

```bash
// Upload encrypted private key with password
AT+USECUB=2,"secure-key","mypassword123"{binary_data}
```

## TLS version configuration

NORA-W36 v3.1.0 introduces comprehensive TLS 1.3 support across all protocols including EAP-TLS, TCP sockets, HTTP clients, and MQTT. This enhanced security capability provides improved encryption algorithms, forward secrecy, and reduced handshake latency.

**TLS Version Parameters:**
All TLS-enabled AT commands support the following version parameters:
- `0`: Disable TLS (not recommended for secure connections)
- `1`: TLS 1.2 only (legacy compatibility)
- `2`: TLS 1.3 only (recommended for new implementations)
- `3`: TLS 1.2 or 1.3 (negotiate highest available - flexible option)

**Protocol-Specific TLS Support:**

| Protocol | AT Command | Example (TLS 1.3) | Security Benefits |
|----------|------------|-------------------|-------------------|
| EAP-TLS | `AT+UWSSE` | `AT+UWSSE=0,2,"ca.pem","client.pem","client.key"` | Enterprise Wi-Fi with latest security |
| PEAP | `AT+UWSSP` | `AT+UWSSP=0,2,"username","password"` | Protected authentication tunnel |
| TCP Socket | `AT+USOTLS` | `AT+USOTLS=0,2,"ca.pem","client.pem","client.key"` | Secure socket connections |
| MQTT | `AT+UMQTLS` | `AT+UMQTLS=0,2,"ca.pem","client.pem","client.key"` | IoT messaging security |
| HTTP | `AT+UHTCTLS` | `AT+UHTCTLS=0,2,"ca.pem","client.pem","client.key"` | Web API secure access |

**TLS 1.3 Security Enhancements:**
- **Forward Secrecy**: Each session uses unique encryption keys
- **Reduced Handshake**: Faster connection establishment (1-RTT vs 2-RTT)
- **Improved Cipher Suites**: Only secure AEAD algorithms supported
- **Certificate Privacy**: Server certificate encrypted during handshake
- **Anti-Downgrade Protection**: Prevents fallback to weaker TLS versions

**Migration Recommendations:**
1. **New Projects**: Use TLS 1.3 (parameter `2`) for maximum security
2. **Legacy Compatibility**: Use flexible mode (parameter `3`) during transition
3. **Testing**: Verify server/broker TLS 1.3 support before deployment
4. **Performance**: Monitor connection times - TLS 1.3 typically reduces latency

## TLS extensions configuration

NORA-W36 supports advanced TLS extensions that enhance security and compatibility with modern TLS implementations.

**Available TLS Extensions:**

| Extension | AT Command | Purpose | Default State |
|-----------|------------|---------|---------------|
| Server Name Indication (SNI) | `AT+USETE0` | Identifies target server hostname | Enabled |
| Handshake Fragmentation | `AT+USETE1` | Fragments large handshake messages | Enabled |

**Server Name Indication (SNI):**
- Enables TLS client to specify hostname during handshake
- Essential for servers hosting multiple domains on same IP
- Required for proper certificate validation in many deployments

```
// Enable SNI (recommended for most applications)
AT+USETE0=1

// Disable SNI (only for legacy servers)
AT+USETE0=0

// Check current SNI setting
AT+USETE0?
```

**Handshake Fragmentation:**
- Splits large TLS handshake messages into smaller fragments
- Prevents issues with MTU limitations and network constraints
- Improves reliability in constrained network environments

```
// Enable handshake fragmentation (recommended)
AT+USETE1=1

// Disable handshake fragmentation
AT+USETE1=0

// Check current fragmentation setting
AT+USETE1?
```

**Configuration Best Practices:**
1. **Keep SNI Enabled**: Required for most modern TLS servers
2. **Enable Fragmentation**: Prevents handshake failures in constrained networks
3. **Store Settings**: Use `AT&W` followed by `AT+CPWROFF` to persist extension settings across reboots
4. **Test Configuration**: Verify TLS handshake success with target servers




# MQTT use cases

**📡 MQTT Communication Overview:**

```
    ┌─────────────     ┌─────────────     ┌─────────────
    │📱 Publisher │────▶│ MQTT      │◄────│📱 Subscriber│
    │  (NORA-W36) │     │   Broker    │     │  (Device)   │
    │             │     │             │     │             │
    │ Sends data  │     │ Routes      │     │ Receives    │
    │ to topics   │     │ messages    │     │ from topics │
    └─────────────┘     └─────────────┘     └─────────────┘
           │                     │                     │
      Publish Msgs          Topic Routing         Subscribe

    🔧 Features:             Broker:             📊 Benefits:

- • Low bandwidth        • Topic management     • Decoupled comm.
- • Reliable delivery    • Message routing      • Scalable design
- • QoS levels (0,1,2)   • Client sessions      • IoT optimized

```

- The MQTT client in NORA-W36 uses version [MQTT v3.1.1](https://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html)
- For more about the Message Queuing Telemetry Transport (MQTT), see the [MQTT beginner's guide](https://www.u-blox.com/en/blogs/insights/mqtt-beginners-guide)
- **TLS 1.3 Security**: NORA-W36 v3.1.0+ supports TLS 1.2 and **TLS 1.3** for secure MQTT communications with enhanced encryption algorithms, forward secrecy, and reduced handshake latency

## MQTT overview

**MQTT (Message Queuing Telemetry Transport)** is a lightweight, publish-subscribe messaging protocol designed for IoT applications with constrained networks and devices. It enables efficient communication between devices and cloud services with minimal bandwidth and power consumption.

**Key MQTT characteristics:**
- **Publish-Subscribe Model**: Decoupled communication through topics
- **Lightweight Protocol**: Minimal overhead for constrained devices
- **Reliable Delivery**: Multiple Quality of Service levels
- **Persistent Sessions**: Maintain connection state across disconnections
- **Last Will Testament**: Automatic notification of unexpected disconnections

**NORA-W36 MQTT Implementation:**
- Uses MQTT v3.1.1 protocol (MQTT v5.0 is not supported)
- TLS 1.2 support for secure connections
- Optimized for IoT device constraints

## MQTT key concepts

## Quality of service (qos) levels

MQTT provides three QoS levels to guarantee message delivery:

**QoS 0 - At Most Once**
- Fire-and-forget delivery
- No acknowledgment required
- Fastest but least reliable
- Use case: Sensor readings where occasional data loss is acceptable
```
AT+UMQPS=0,0,0,"temperature","25.5"          // QoS 0 publish
```

**QoS 1 - At Least Once**
- Guaranteed delivery with possible duplicates
- Requires PUBACK acknowledgment
- Balanced reliability and performance
- Use case: Important notifications that must be delivered
```
AT+UMQPS=0,1,0,"alert","Low battery warning"    // QoS 1 publish
```

**QoS 2 - Exactly Once**
- Guaranteed single delivery
- Requires PUBREC/PUBREL/PUBCOMP handshake
- Highest reliability but slowest
- Use case: Critical commands or financial transactions
```
AT+UMQPS=0,2,0,"command","device_reset"      // QoS 2 publish
```

## Retained messages

Retained messages are stored by the broker and delivered to new subscribers immediately upon subscription:

**Publishing a retained message:**
```
AT+UMQPS=0,0,1,"device/status","online"      // Retain flag = 1
```

**Use cases for retained messages:**
- Device status (online/offline)
- Last known sensor values
- Configuration settings
- System announcements

## Last will and testament (LWT)

LWT allows devices to specify a message that the broker publishes automatically if the device disconnects unexpectedly:

**Configuration example:**
```
// Configure LWT during connection setup
AT+UMQCP=0,"broker.example.com",1883,"device123","user","pass"
```

**LWT use cases:**
- Device health monitoring
- Automatic offline notifications
- System fault detection
- Connection status tracking

## Connection management

**Clean Session Flag:**
- Clean Session = 1: Fresh start, no stored state
- Clean Session = 0: Resume previous session with stored subscriptions

**Keep-Alive Timer:**
- Maintains connection during idle periods
- Broker disconnects if no communication within keep-alive interval
- Recommended: 30-300 seconds depending on application

## Error handling and troubleshooting

**Common MQTT Error Scenarios:**

| Issue | Symptoms | Solution |
|-------|----------|----------|
| Connection timeout | `AT+UMQC=0` returns `ERROR` | Check network connectivity and broker address |
| Authentication failure | Connection rejected | Verify username/password credentials |
| Certificate errors | TLS connection fails | Validate CA certificate and client certificates |
| Keep-alive timeout | Unexpected disconnection | Adjust keep-alive timer or check network stability |
| Invalid client ID | Connection refused | Use unique, valid client identifier |

**MQTT Connection Status:**
- Successful connection: `+UEMQC:0`
- Message received: `+UEMQD:<handle>,<length>`
- Connection lost: Monitor connection events

**Troubleshooting Steps:**

| Step | Command | Purpose |
|------|---------|---------|
| 1 | `AT+UWSNST?` | Check connection status |
| 2 | `AT+UWSNST=0` | Verify Wi-Fi connectivity |
| 3 | `AT+UWSST=0` | Check network interface status |
| 4 | `AT+UWSSC` | Check AP status |
| 5 | - | Check MQTT connection status |
| 6 | - | Validate certificates for TLS connections |
| 7 | - | Monitor keep-alive and adjust if needed |
| 8 | - | Review broker logs for additional error details |

## Performance optimization

**Connection Parameters:**

| Parameter | Optimal Range | Impact |
|-----------|---------------|--------|
| Keep-Alive | 30-300 seconds | Network efficiency vs responsiveness |
| Clean Session | Context-dependent | Memory usage vs session persistence |
| QoS Level | 0-1 for most cases | Reliability vs performance |
| Message Size | < 1KB preferred | Network bandwidth and processing |

**Best Practices:**
- Use QoS 0 for frequent sensor data
- Use QoS 1 for important events
- Keep topic names short and hierarchical
- Implement exponential backoff for reconnections
- Monitor connection stability with keep-alive
- Use retained messages sparingly

**Network Considerations:**
- Choose appropriate keep-alive based on network reliability
- Consider cellular vs Wi-Fi network characteristics
- Implement proper error handling and retry logic
- Monitor battery usage for power-constrained applications

## MQTT client without TLS - Mosquitto

![mqtt](https://content.u-blox.com/sites/default/files/2024-09/mqtt_no_tls.png)
This use case connects NORA-W36 as a Wi-Fi Station and a MQTT Broker on port 1883. In this scenario, the module connects to Mosquitto without a certificate.


**Parameters and values**
- Host: test.mosquitto.org
- Port: 1883 (no TLS connection)
- Client ID: -
- Username: -
- Password: -
- CA Root certificate: -
- Client certificate: -
- Client private key: -

Before connecting to MQTT, set up Wi-Fi Connection, as described in [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3), steps 1-5.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Check MQTT connection parameters          | `AT+UMQCP=0` | `+UMQCP:0,<hostname>,<port>,<client_id>,<username>` |
| 2 | Configure MQTT host and port              | `AT+UMQCP=0,"test.mosquitto.org",1883`| `OK` |
| 3 | Connect to MQTT broker                    | `AT+UMQC=0`                            | `+UEMQC:0` |
| 4 | Publish Message on topic **pubtopic**       | `AT+UMQPS=0,0,0,"pubtopic","Hello from NORA-W36"`                  | `OK` |
| 5 | Subscribe on topic **subtopic**                | `AT+UMQS=0,0,"subtopic"`            | `OK` |
| 6 | Post a Message to the MQTT Broker on **subtopic** the message should be    **Hello from remote device** | -  | - |
| 7 | Receive Message on **subtopic**                |                                   | `+UEMQD:0,24` |
| 8 | Read String Message                                | `AT+UMQRS=0`                         | `+UMQRS:0,0,"subtopic",24,"Hello from remote device"` |
| 9 | Disconnect from MQTT broker                    | `AT+UMQDC=0`                            | `OK` |

**Note:** Use the wildcard "*" to receive messages for all topics. Note that this option may not be supported by all brokers, like Azure.

## MQTT TLS client - Mosquitto

![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mosquitto-text-side.png)
![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mqtt.png)

This use case connects NORA-W36 as a Wi-Fi Station and a MQTT Broker. In this scenario, the module connects to Mosquitto using certificates.


To generate client certificate and client key, follow the procedures described on the Mosquitto web page:  https://test.mosquitto.org/ssl/
- CA certificate can be downloaded here: [mosquitto.org.crt](https://test.mosquitto.org/ssl/mosquitto.org.crt)


**Parameters and values**
- Host: test.mosquitto.org
- Port: 8884 (TLS)
- Client ID: -
- Username: -
- Password: -
- CA Root certificate: mosquitto.org.crt
- Client certificate: client.crt
- Client private key: client.key

**Note**: The parameters given in this scenario use the port **8884** for connections and encryption for security.

To authenticate the client and ensure the following:
- Only authorized devices can establish a connection with the MQTT broker
- Clients provide a valid certificate when making a connection
- 1883 : MQTT, unencrypted, unauthenticated
- 1884 : MQTT, unencrypted, authenticated
- 8883 : MQTT, encrypted, unauthenticated
- **8884 : MQTT, encrypted, client certificate required** (used in this example)
- 8885 : MQTT, encrypted, authenticated
- 8886 : MQTT, encrypted, unauthenticated


Before connecting to MQTT, set up a Wi-Fi Connection like that described in [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3), steps 1-5.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure MQTT host and port              | `AT+UMQCP=0,"test.mosquitto.org",8884`| `OK` |
| 2 | Write X.509 certificate and private key using [Binary data](#simple-binary-data-example) | `AT+USECUB=0,"mosquitto.org.crt"{binary_content}` + `AT+USECUB=1,"client.crt"{binary_content}` + `AT+USECUB=2,"client.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Setup TLS 1.3 connection config          | `AT+UMQTLS=0,2,"mosquitto.org.crt","client.crt","client.key"`| `OK` |
| 4 | Connect to MQTT broker                    | `AT+UMQC=0`                            | `+UEMQC:0` |
| 5 | Publish Message on topic **pubtopic**    | `AT+UMQPS=0,0,0,"pubtopic","Hello from NORA-W36"`                  | `OK` |
| 6 | Subscribe on topic **subtopic**           | `AT+UMQS=0,0,"subtopic"`            | `OK` |
| 7 | Post a Message to the MQTT Broker on **subtopic**. The message should say **Hello from remote device** | -  | - |
| 8 | Receive Message on **subtopic**           |                        | `+UEMQD:0,24` |
| 9 | Read String Message                       | `AT+UMQRS=0`           | `+UMQRS:0,0,"subtopic",24,"Hello from remote device"` |
| 10 | Disconnect from MQTT broker              | `AT+UMQDC=0`                            | `OK` |

## MQTT TLS client - thingstream

![mqtt](https://content.u-blox.com/sites/default/files/2024-04/u-blox-thingstream.png)
![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mqtt.png)

Thingstream is the u-blox service delivery platform for:

- IoT Communication-as-a-Service
- IoT Location-as-a-Service

This use case connects NORA-W36 as a Wi-Fi Station and a MQTT Broker. In this scenario NORA-W36 connects to Thingstream using a CA Root certificate, Client-ID, Username and Password.


[Thingstream](https://www.u-blox.com/en/product/thingstream) uses the AWS Root Certificate found here: https://www.amazontrust.com/repository/AmazonRootCA1.pem

Before connecting to MQTT, set up Wi-Fi Connection, like that described [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3), steps 1-5.
The parameters and values necessary for the use case include:

**Parameters and values**
- Host: mqtt.thingstream.io
- Port: 8883 (TLS)
- Client ID: device:78e3d356-876f-483b-872f-3485853fAAAA
- Username: HMVK8C09FQP245O2BBBB
- Password: ofYyBB/L3GkPvo060J6Dv+t+mfrh0XpGMcf7CCCC
- CA Root certificate: AmazonRootCA1.pem
- Client certificate: -
- Client private key: -

Before connecting to MQTT, set up Wi-Fi Connection like in steps 1-5 in [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3)

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure the MQTT host, port, client-ID, username and password             | `AT+UMQCP=0,"mqtt.thingstream.io",8883,"device:78e3d356-876f-483b-872f-3485853fAAAA","HMVK8C09FQP245O2BBBB","ofYyBB/L3GkPvo060J6Dv+t+mfrh0XpGMcf7CCCC"`| `OK` |
| 2 | Write X.509 CA Root certificate using [Binary data](#simple-binary-data-example) | `AT+USECUB=0,"AmazonRootCA1.pem"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Set up TLS connection config. Thingstream doesn´t use a client certificate or key  - only the root CA.                  | `AT+UMQTLS=0,1,"AmazonRootCA1.pem"`| `OK` |
| 4 | Connect to MQTT broker                    | `AT+UMQC=0`                            | `+UEMQC:0` |
| 5 | Publish a message on **pubtopic**       | `AT+UMQPS=0,0,0,"pubtopic","Hello from NORA-W36"`                  | `OK` |
| 6 | Subscribe on topic **subtopic**                | `AT+UMQS=0,0,"subtopic"`            | `OK` |
| 7 | Post a message to the MQTT broker on **subtopic**. The message should say    **Hello from remote device** | -  | - |
| 8 | Receive a message on **subtopic**                |                        | `+UEMQD:0,24` |
| 9 | Read String Message                                | `AT+UMQRS=0`           | `+UMQRS:0,0,"subtopic",24,"Hello from remote device"` |
| 10 | Disconnect from MQTT broker                    | `AT+UMQDC=0`                            | `OK` |

## MQTT TLS client - AWS IoT core

![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mqtt.png)
Connect as a Wi-Fi Station and a MQTT Broker. In this scenario, NORA-W36 connects to Amazon AWS IoT Core using certificates.

**Parameters and values**
- Host: a3loryode2aaaa-ats.iot.us-east-2.amazonaws.com
- Port: 8883 (TLS)
- Client ID: -
- Username: -
- Password: -
- CA Root certificate: AmazonRootCA1.pem
- Client certificate: aws_client.crt
- Client private key: aws_priv_key.key

Before connecting to MQTT, set up Wi-Fi Connection like in steps 1-5 in [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3)

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure MQTT host and port              | `AT+UMQCP=0,"a3loryode2aaaa-ats.iot.us-east-2.amazonaws.com",8883`| `OK` |
| 2 | Write X.509 certificate and private key using [Binary data](#simple-binary-data-example) | `AT+USECUB=0,"AmazonRootCA1.pem"{binary_content}` + `AT+USECUB=1,"aws_client.crt"{binary_content}` + `AT+USECUB=2,"aws_priv_key.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Setup TLS connection config                  | `AT+UMQTLS=0,1,"AmazonRootCA1.pem","aws_client.crt","aws_priv_key.key"`| `OK` |
| 4 | Connect to MQTT broker                    | `AT+UMQC=0`                            | `+UEMQC:0` |
| 5 | Publish Message on topic **pubtopic**       | `AT+UMQPS=0,0,0,"pubtopic","Hello from NORA-W36"`                  | `OK` |
| 6 | Subscribe on topic **subtopic**                | `AT+UMQS=0,0,"subtopic"`            | `OK` |
| 7 | Post a Message to the MQTT Broker on **subtopic** the message should be    **Hello from remote device** | -  | - |
| 8 | Receive Message on **subtopic**                |                        | `+UEMQD:0,24` |
| 9 | Read String Message                                | `AT+UMQRS=0`           | `+UMQRS:0,0,"subtopic",24,"Hello from remote device"` |
| 10 | Disconnect from MQTT broker                    | `AT+UMQDC=0`                            | `OK` |

## MQTT TLS client - Azure IoT hub

Connect as a Wi-Fi Station and an Access Point and a MQTT Broker. In this scenario, NORA-W36 connects to Microsoft Azure using certificates.

![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mqtt.png)

**Important Note**: Azure IoT Hub isn't a full-featured MQTT broker and doesn't support all the behaviors specified in the MQTT v3.1.1 standard.

**Parameters and values**
- Host: iothub-test-sw.azure-devices
- Port: 8883 (TLS)
- Client ID: device1
- Username: iothub-test-sw.azure-devices.net/device1/
- Password: -
- CA Root certificate: AzureCa.pem
- Client certificate: azure_client.crt
- Client private key: azure_priv_key.key

Before connecting to MQTT, set up Wi-Fi Connection like in steps 1-5 in [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3)

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure MQTT Host, Port, Client ID and Username   | `AT+UMQCP=0,"iothub-test-sw.azure-devices.net",8883,"device1","iothub-test-sw.azure-devices.net/device1/"`| `OK` |
| 2 | Write X.509 certificate and private key using [Binary data](#simple-binary-data-example) | `AT+USECUB=0,"AzureCa.pem"{binary_content}` + `AT+USECUB=1,"azure_client.crt"{binary_content}` + `AT+USECUB=2,"azure_priv_key.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Setup TLS connection config                  | `AT+UMQTLS=0,1,"AzureCa.pem","azure_client.crt","azure_priv_key.key"`| `OK` |
| 4 | Connect to MQTT broker                    | `AT+UMQC=0`                            | `+UEMQC:0` |
| 5 | Publish Message on topic **pubtopic**       | `AT+UMQPS=0,0,0,"pubtopic","Hello from NORA-W36"`                  | `OK` |
| 6 | Subscribe on topic **subtopic**                | `AT+UMQS=0,0,"subtopic"`            | `OK` |
| 7 | Post a Message to the MQTT Broker on **subtopic** the message should be    **Hello from remote device** | -  | - |
| 8 | Receive Message on **subtopic**                |                        | `+UEMQD:0,24` |
| 9 | Read String Message                                | `AT+UMQRS=0`           | `+UMQRS:0,0,"subtopic",24,"Hello from remote device"` |
| 10 | Disconnect from MQTT broker                    | `AT+UMQDC=0`                            | `OK` |

# HTTP and HTTPS use cases

NORA-W36 includes a comprehensive HTTP client supporting HTTP/1.1 protocol with features including GET, POST, PUT, DELETE operations. When combined with TLS, it provides secure HTTPS communication. The HTTP client simplifies web communication without requiring deep protocol knowledge.

**Important Note**: HTTP requests have a Maximum Transmission Unit (MTU) of 1000 bytes. This applies to both request data and response data. For larger data transfers, consider splitting the data into multiple requests or using chunked transfer encoding.

## HTTP client features

- **HTTP Methods**: GET, POST, PUT, DELETE, HEAD
- **TLS/SSL Support**: HTTPS with server certificate validation
- **Authentication**: Basic authentication, custom headers
- **Content Types**: JSON, XML, binary data, form data
- **Connection Management**: Keep-alive and connection reuse
- **Error Handling**: HTTP status codes and error reporting

## Available HTTP commands

| Command | Description |
|---------|-------------|
| `AT+UHTCCP` | HTTP Client Connection Parameters |
| `AT+UHTCTLS` | HTTP Client TLS Configuration |
| `AT+UHTCDC` | HTTP Client Disconnect |
| `AT+UHTCGH` | HTTP Client Get Header |
| `AT+UHTCGBB` | HTTP Client Get Body Binary |
| `AT+UHTCGBS` | HTTP Client Get Body String |
| `AT+UHTCRHAF` | HTTP Client Request Header Add Field |
| `AT+UHTCRHCS` | HTTP Client Request Header Custom String |
| `AT+UHTCRHC` | HTTP Client Request Header Clear |
| `AT+UHTCRP` | HTTP Client Request Path |
| `AT+UHTCRG` | HTTP Client Request GET |
| `AT+UHTCRGH` | HTTP Client Request GET Header |
| `AT+UHTCRD` | HTTP Client Request DELETE |
| `AT+UHTCRDH` | HTTP Client Request DELETE Header |
| `AT+UHTCRPOS` | HTTP Client Request POST String |
| `AT+UHTCRPOB` | HTTP Client Request POST Binary |
| `AT+UHTCRPOH` | HTTP Client Request POST Header |
| `AT+UHTCRPUS` | HTTP Client Request PUT String |
| `AT+UHTCRPUB` | HTTP Client Request PUT Binary |
| `AT+UHTCRPUH` | HTTP Client Request PUT Header |

## Simple HTTP get request

This example demonstrates a basic HTTP GET request to retrieve data from a web server.

**Target**: `http://httpbin.org/get` (HTTP test service)

Before connecting, ensure Wi-Fi is connected as shown in [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3).

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure HTTP client for target server | `AT+UHTCCP=0,"httpbin.org",80` | `OK` |
| 2 | Set request path | `AT+UHTCRP=0,"/get"` | `OK` |
| 3 | Send GET request | `AT+UHTCRG=0` | `OK` |
| 4 | Wait for response | | `+UEHTCRS:0,200,"OK"` |
| 5 | Get response headers | `AT+UHTCGH=0` | `+UHTCGH:0,0,"HTTP/1.1 200 OK..."` |
| 6 | Get response body (string) | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,0,<len>,"{"args":{}..."` |
| 7 | Disconnect client | `AT+UHTCDC=0` | `OK` |

## HTTPS get with certificate validation

This example shows secure HTTPS communication with server certificate validation.

**Target**: `https://api.github.com/repos/octocat/Hello-World` (GitHub API)

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Upload CA certificate for GitHub | `AT+USECUB=0,"github-ca.pem"{binary certificate data}` | `OK` |
| 2 | Configure HTTPS client | `AT+UHTCCP=0,"api.github.com",443` | `OK` |
| 3 | Configure TLS 1.3 with certificate validation | `AT+UHTCTLS=0,2,"github-ca.pem"` | `OK` |
| 4 | Set request path | `AT+UHTCRP=0,"/repos/octocat/Hello-World"` | `OK` |
| 5 | Add User-Agent header | `AT+UHTCRHAF=0,"User-Agent","NORA-W36/1.0"` | `OK` |
| 6 | Send HTTPS GET request | `AT+UHTCRG=0` | `OK` |
| 7 | Wait for response | | `+UEHTCRS:0,200,"OK"` |
| 8 | Get JSON response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,0,<len>,"{"id":123456..."` |
| 9 | Disconnect client | `AT+UHTCDC=0` | `OK` |

## HTTP post with JSON data

This example demonstrates sending JSON data via HTTP POST request.

**Target**: `https://httpbin.org/post` (HTTP test service)
**Payload**: `{"temperature": 25.6, "humidity": 60.2, "device": "NORA-W36"}`

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure HTTPS client | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Configure TLS | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set request path | `AT+UHTCRP=0,"/post"` | `OK` |
| 4 | Set Content-Type header | `AT+UHTCRHAF=0,"Content-Type","application/json"` | `OK` |
| 5 | Send POST request with JSON body | `AT+UHTCRPOS=0,"{"temperature": 25.6, "humidity": 60.2, "device": "NORA-W36"}"` | `OK` |
| 6 | Wait for response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Get response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,0,<len>,"{"args":{}..."` |
| 8 | Disconnect client | `AT+UHTCDC=0` | `OK` |

## HTTP post with binary file upload

This example shows how to upload binary files using HTTP POST.

**Target**: `https://httpbin.org/post`
**File**: `sensor_data.bin` (256 bytes)

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure HTTPS client | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Configure TLS | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set request path | `AT+UHTCRP=0,"/post"` | `OK` |
| 4 | Set Content-Type for binary | `AT+UHTCRHAF=0,"Content-Type","application/octet-stream"` | `OK` |
| 5 | Send POST with binary data | `AT+UHTCRPOB=0{256 bytes of binary data}` | `+UHTCRPOB:0,256` |
| 6 | Wait for response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Get server response | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,0,<len>,"{"data":..."` |
| 8 | Disconnect client | `AT+UHTCDC=0` | `OK` |

## HTTP post request for data updates

This example demonstrates updating data on a server using HTTP POST method.

**Target**: `https://httpbin.org/post`
**Data**: Configuration update JSON

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure HTTPS client | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Configure TLS | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set request path | `AT+UHTCRP=0,"/post"` | `OK` |
| 4 | Add authorization header | `AT+UHTCRHAF=0,"Authorization","Bearer xyz123"` | `OK` |
| 5 | Set Content-Type | `AT+UHTCRHAF=0,"Content-Type","application/json"` | `OK` |
| 6 | Send POST request with data | `AT+UHTCRPOS=0,"{"config":{"interval":30,"enabled":true}}"` | `OK` |
| 7 | Wait for response | | `+UEHTCRS:0,200,"OK"` |
| 8 | Get confirmation response | `AT+UHTCGBS=0,800` | `+UHTCGBS:0,0,<len>,"{"json":..."` |
| 9 | Disconnect client | `AT+UHTCDC=0` | `OK` |

## HTTP delete request

This example shows how to delete resources using HTTP DELETE method.

**Target**: `https://httpbin.org/delete`

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure HTTPS client | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Configure TLS | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set request path | `AT+UHTCRP=0,"/delete"` | `OK` |
| 4 | Add authentication header | `AT+UHTCRHAF=0,"Authorization","ApiKey abc123"` | `OK` |
| 5 | Send DELETE request | `AT+UHTCRD=0` | `OK` |
| 6 | Wait for deletion response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Get deletion confirmation | `AT+UHTCGBS=0,500` | `+UHTCGBS:0,0,<len>,"{"url":"..."` |
| 8 | Disconnect client | `AT+UHTCDC=0` | `OK` |

## Advanced TLS configuration

This example demonstrates advanced TLS settings including client certificates for mutual authentication.

**Target**: Secure API with mutual TLS authentication
**Certificates**: CA certificate, client certificate, and private key

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Upload CA certificate | `AT+USECUB=0,"server-ca.pem"{binary data}` | `OK` |
| 2 | Upload client certificate | `AT+USECUB=1,"client.crt"{binary data}` | `OK` |
| 3 | Upload client private key | `AT+USECUB=2,"client.key"{binary data}` | `OK` |
| 4 | Configure HTTPS client | `AT+UHTCCP=0,"secure-api.example.com",443` | `OK` |
| 5 | Configure mutual TLS 1.3 | `AT+UHTCTLS=0,2,"server-ca.pem","client.crt","client.key"` | `OK` |
| 6 | Set request path | `AT+UHTCRP=0,"GET","/api/secure-data"` | `OK` |
| 7 | Send authenticated request | `AT+UHTCRG=0` | `OK` |
| 8 | Wait for response | | `+UEHTCRS:0,200,"OK"` |
| 9 | Get secure data | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,1000,"{"secure"..."` |
| 10 | Disconnect client | `AT+UHTCDC=0` | `+UEHTCDC:0` |

## HTTP response status codes

The HTTP client returns standard HTTP status codes to indicate request results:

| Status Code | Meaning | Description |
|-------------|---------|-------------|
| 200 | OK | Request successful |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Invalid request format |
| 401 | Unauthorized | Authentication required |
| 403 | Forbidden | Access denied |
| 404 | Not Found | Resource not found |
| 500 | Server Error | Internal server error |
| 503 | Service Unavailable | Server temporarily unavailable |

## Troubleshooting HTTP requests

## Common issues and solutions

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| Connection timeout | Network unreachable | Check Wi-Fi connection and DNS resolution |
| Certificate error | Invalid/expired certificate | Update CA certificate or disable validation |
| 401 Unauthorized | Missing/invalid authentication | Check API key, username/password, or tokens |
| 413 Payload Too Large | Request body too large | Split large requests or use chunked transfer |
| SSL handshake failed | TLS version mismatch | Update TLS settings or certificate chain |

## Debugging steps

1. **Check connection status**: `AT+UWSNST?` (connection info)
2. **Verify DNS resolution**: Check if domain name resolves correctly
3. **Test without TLS**: Try HTTP instead of HTTPS to isolate TLS issues
4. **Check certificate chain**: Ensure complete certificate chain is uploaded
5. **Validate headers**: Confirm Content-Type, Content-Length, and Authorization headers

## HTTP client best practices

## Performance optimization

- **Connection Reuse**: Keep HTTP client connected for multiple requests to same server
- **Compression**: Use `Accept-Encoding: gzip` header when supported
- **Chunked Transfer**: For large uploads, consider chunked transfer encoding
- **Timeout Settings**: Configure appropriate timeout values for your use case

## Security recommendations

- **Always use HTTPS** for sensitive data transmission
- **Validate server certificates** using proper CA certificates
- **Use strong authentication** (API keys, OAuth tokens) instead of basic auth
- **Implement rate limiting** to avoid overwhelming servers
- **Sanitize response data** before processing in your application

## Memory management

- **Read response data incrementally** using appropriate buffer sizes
- **Disconnect unused clients** to free resources: `AT+UHTCDC=0`
- **Monitor memory usage** with large file transfers
- **Use binary mode** for non-text data to avoid encoding overhead

## Example: complete IoT sensor data upload

```text
// Connect to secure IoT platform
AT+UHTCCP=0,"iot.example.com",443
AT+UHTCTLS=0,1,"iot-ca.pem","device.crt","device.key"
AT+UHTCRP=0,"POST","/api/v1/sensors/data"
AT+UHTCRHAF=0,"Content-Type","application/json"
AT+UHTCRHAF=0,"Authorization","Bearer eyJhbGciOiJIUzI1..."
AT+UHTCRHAF=0,"X-Device-ID","NORA-W36-001"

// Send sensor reading
AT+UHTCRPOS=0,85
{"timestamp":"2025-09-25T10:30:00Z","temperature":23.5,"humidity":65,"pressure":1013}

// Expected response: HTTP 201 Created
+UEHTCRS:0,201,"Created"
AT+UHTCGBS=0,200
+UHTCGBS:0,0,45,"{"status":"success","id":"sensor_12345"}"
AT+UHTCDC=0
```

# Network Time Protocol (NTP) use cases

![wi-fi-ntp](https://content.u-blox.com/sites/default/files/2024-04/u-blox-wifi.png)

NORA-W36 supports Network Time Protocol (NTP) client functionality to synchronize the system clock with time servers on the internet. This ensures accurate timekeeping for applications that require time-stamped data, secure communications, or scheduled operations.

## Basic NTP configuration

Connect as a Wi-Fi station and configure NTP to synchronize system time automatically.

This use case demonstrates how to set up NTP with multiple time servers for redundancy and verify time synchronization.


**Prerequisites:**
- Module must be connected to a Wi-Fi network with internet access
- Network must allow UDP traffic on port 123 (NTP)

| Nr| Instructions                              | AT command                        | AT event/Response              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Connect to Wi-Fi network first           | See [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3) example |  |
| 2 | Configure primary NTP server             | `AT+UNTSC=0,"pool.ntp.org"`      | `OK` |
| 3 | Configure secondary NTP server           | `AT+UNTSC=1,"time.google.com"`   | `OK` |
| 4 | Configure third NTP server               | `AT+UNTSC=2,"time.nist.gov"`     | `OK` |
| 5 | Check current system time (before sync)  | `AT+USYTU?`                       | `+USYTU:00000001` |
| 6 | Enable NTP client                        | `AT+UNTE=1`                       | `OK` |
| 7 | Wait for synchronization (5-30 seconds)  |                                   |  |
| 8 | Verify NTP server status                 | `AT+UNTSC?`                       | `+UNTSC:0,"pool.ntp.org","185.255.55.20",1` + `+UNTSC:1,"time.google.com","216.239.35.12",1` + `+UNTSC:2,"time.nist.gov","129.6.15.28",1` |
| 9 | Check synchronized time                   | `AT+USYTU?`                       | `+USYTU:66E7B2A4` |
| 10| Save NTP configuration                    | `AT&W`                            | `OK` |
| 11| Reset to apply stored settings safely     | `AT+CPWROFF`                      | `OK` |

**Note:** The unix time `66E7B2A4` (hex) equals `1726468772` (decimal), which corresponds to a human-readable time like "Mon, 16 Sep 2024 10:12:52 GMT".

## NTP with DHCP fallback

Configure NTP to use DHCP-provided time servers with manual fallback.

This configuration first attempts to use NTP servers provided by the network's DHCP server, falling back to manually configured servers if DHCP servers are unavailable.


| Nr| Instructions                              | AT command                        | AT event/Response              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Connect to Wi-Fi network first           | See [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3) example |  |
| 2 | Configure fallback NTP servers           | `AT+UNTSC=0,"time.google.com"`   | `OK` |
| 3 | Configure additional fallback server     | `AT+UNTSC=1,"pool.ntp.org"`      | `OK` |
| 4 | Enable NTP with DHCP + manual fallback   | `AT+UNTE=2`                       | `OK` |
| 5 | Verify NTP configuration                 | `AT+UNTE?`                        | `+UNTE:2` |
| 6 | Check which servers are being used       | `AT+UNTSC?`                       | Shows DHCP or manual servers depending on availability |
| 7 | Save configuration                        | `AT&W`                            | `OK` |
| 8 | Reset to apply stored settings safely     | `AT+CPWROFF`                      | `OK` |

## NTP server management

Manage and troubleshoot NTP server configuration.


| Nr| Instructions                              | AT command                        | AT event/Response              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Check current NTP client status          | `AT+UNTE?`                        | `+UNTE:1` (enabled) or `+UNTE:0` (disabled) |
| 2 | View all configured servers              | `AT+UNTSC?`                       | Shows all 5 server slots (0-4) with status |
| 3 | Remove a specific NTP server             | `AT+UNTSC=2,""`                   | Removes server from slot 2 |
| 4 | Add new NTP server                       | `AT+UNTSC=2,"time.cloudflare.com"` | `OK` |
| 5 | Disable NTP client                       | `AT+UNTE=0`                       | `OK` |
| 6 | Re-enable NTP client                     | `AT+UNTE=1`                       | `OK` |

**Popular NTP Servers:**
- `pool.ntp.org` - Global NTP pool project
- `time.google.com` - Google Public NTP
- `time.nist.gov` - US National Institute of Standards
- `time.cloudflare.com` - Cloudflare Public NTP
- Regional pools: `0.europe.pool.ntp.org`, `0.asia.pool.ntp.org`, etc.

**Troubleshooting Tips:**
- If servers show `reachable=0`, check network connectivity and firewall settings
- NTP synchronization may take 30-60 seconds on first connection
- Use multiple servers from different sources for redundancy
- Regional NTP servers typically provide better performance than global ones

# Roaming use cases

## Wi-Fi roaming overview

Wi-Fi roaming allows devices to maintain seamless connectivity while moving between access points (APs) in the same network. This is essential for mobile applications, large coverage areas, and enterprise environments where multiple APs provide overlapping coverage using the same Service Set Identifier (SSID).

## IEEE 802.11 roaming standards

Modern Wi-Fi networks implement several roaming standards to optimize the handoff process:

**IEEE 802.11r (Fast BSS Transition - FT)**
- Reduces roaming time from ~1000ms to ~50ms
- Pre-authenticates with target AP before handoff
- Maintains security associations during transition
- Critical for real-time applications like VoIP

**IEEE 802.11k (Radio Resource Management - RRM)**
- Provides neighbor AP reports to clients
- Enables intelligent roaming decisions
- Reduces scanning time by providing AP candidate lists
- Includes signal strength and load information

**IEEE 802.11v (Wireless Network Management - WNM)**
- Allows network-assisted roaming decisions
- APs can suggest better connection targets
- Enables Band Steering (2.4GHz ↔ 5GHz)
- Supports load balancing across APs

**IEEE 802.11w (Protected Management Frames - PMF)**
- Secures management frames during roaming
- Prevents deauthentication attacks
- Required for WPA3 networks

## NORA-W36 roaming implementation

NORA-W36 supports client-initiated roaming based on RSSI thresholds and scanning algorithms. Roaming is **disabled by default** and must be enabled before connecting to Wi-Fi.

## Roaming process

1. **Monitoring Phase**: Continuously monitors current AP's RSSI
2. **Trigger Phase**: When RSSI drops below threshold, initiates background scanning
3. **Discovery Phase**: Scans for APs with same SSID and better signal strength
4. **Decision Phase**: Evaluates candidate APs based on configured criteria
5. **Handoff Phase**: Disconnects from current AP and connects to target AP

## Roaming configuration

NORA-W36 supports roaming, it is disabled by default and needs to be enabled before connecting Wi-Fi with `AT+UWSROE=1`

The most important settings are the following, see AT manual for more settings:

| Command | Default | Valid values | Description |
|---------|---------|--------------|-------------|
| `AT+UWSROE=<roaming>` | 0 | 0: Disable roaming 1: Enable roaming | Master roaming enable/disable |
|`AT+UWSROS0=<roaming_scanning_threshold>` | -70 | Valid values: -95..0 | RSSI threshold to trigger scanning (dBm) |
|`AT+UWSROS1=<roaming_switch_limit>` | 10 | Valid values: 1..50 | Minimum RSSI improvement needed (dB) |
|`AT+UWSROS2=<roaming_scan_interval>` | 5000 | Valid values: 100..3600000 | Background scan interval (ms) |
| `AT+UWSROS3=<roaming_current_rssi>` | 0 | 0: Disable current RSSI roaming 1: Enable current RSSI roaming | Roaming calculation mode |
|`AT+UWSROS4=<roaming_delay_time>` | 0 | Valid values: 0..30000 | Handover delay time (ms) |
| `AT+UWSROS5=<roaming_all_channels>` | 1 | 0: Scan current channel only 1: Scan all channels | Channel scanning scope |

## Standard roaming mode (AT+uwsros3=0)

With the default configuration, roaming will start when RSSI drops to -70 dBm or below. A background scan will start to find a better AP with the same SSID. It will perform roaming if an Access Point with `-70 + 10 = -60 dBm` or better is found.

**Example configuration:**
```
AT+UWSROE=1      // Enable roaming
AT+UWSROS0=-70           // Start scanning at -70 dBm
AT+UWSROS1=10            // Require 10 dB improvement
AT+UWSROS3=0     // Use fixed threshold mode
```

## Adaptive roaming mode (AT+uwsros3=1)

In some situations you want to roam based on your current RSSI instead of a fixed value. This "aggressive roaming" mode uses `AT+UWSROS3=1` and typically requires lowering the switch limit to 3 dBm `AT+UWSROS1=3`.

**Calculation:** If current RSSI is -78 dBm, the target threshold becomes `-78 + 3 = -75 dBm`. Roaming will occur if an AP with -75 dBm or better signal is found.

**Example configuration:**
```
AT+UWSROE=1      // Enable roaming
AT+UWSROS0=-70           // Start scanning at -70 dBm
AT+UWSROS1=3     // Require only 3 dB improvement
AT+UWSROS3=1     // Use current RSSI mode
```

## Roaming optimization guidelines

**Roaming Configuration Strategies:**

| Strategy | Use Case | Configuration | Commands |
|----------|----------|--------------|----------|
| **Stable connections** | Minimal roaming, consistent connection | Higher threshold, significant improvement required | `AT+UWSROS0=-80` + `AT+UWSROS1=15` + `AT+UWSROS3=0` |
| **Aggressive roaming** | Maximum signal quality | Moderate threshold, lower improvement requirement | `AT+UWSROS0=-65` + `AT+UWSROS1=3` + `AT+UWSROS3=1` |
| **Enterprise environments** | High AP density | Custom based on deployment | Test and monitor for optimal settings |

**For enterprise environments:**
- Consider AP density and coverage overlap
- Test roaming behavior in actual deployment
- Monitor for excessive roaming (ping-ponging)

## Current roaming capabilities and roadmap

**Current implementation:**
- NORA-W36 performs client-initiated roaming only
- Roaming decision based on RSSI only (no load balancing)
- Brief connectivity interruption during AP handoff
- Both APs must use identical security configuration

**Future roadmap:**
- **802.11r (Fast BSS Transition)** support planned for future releases
- **802.11k (Radio Resource Management)** support planned for future releases
- **802.11v (Wireless Network Management)** support planned for future releases
- These standards will enable faster, more intelligent roaming with minimal service interruption

# Power save use cases


## Auto sleep

By default no lower power mode is enabled in NORA-W36 to have maximal performance and response time.
In some applications power consumption is important and data throughput and latency is not that important. By enabling the low power mode this will slightly change. More power save means more latency can be expected.
Power level 0 (default, no power save) and power level 1 (moderate power save) is supported, more levels may be added in future releases.

The low power level 1 is set using the command `AT+UPMPSL=1` see NORA-W36 SIM and AT command manual for more details. There is a limitation that the first AT command after the timeout (default 1 second) can't be longer than 16 bytes.

**Important Note**: In power level 1 only 115200 baud rate or lower is allowed.

**Power Management Commands:**

| Command | Purpose | Example | Default |
|---------|---------|---------|---------|
| `AT+UPMPSL=<level>` | Set power save level | `AT+UPMPSL=1` | Level 0 (no power save) |
| `AT+UPMPSTO=<timeout_ms>` | Set active state timeout | `AT+UPMPSTO=2000` | 1000ms (1 second) |
| `AT+UPMPSL?` | Read current power level | Shows current setting | N/A |
| `AT+UPMPSTO?` | Read current timeout | Shows timeout in ms | N/A |

**Power Save Configuration Examples:**

```bash
// Enable moderate power save with 2-second timeout
AT+UPMPSL=1
AT+UPMPSTO=2000
AT&W             // Store settings
AT+CPWROFF       // Reset to apply stored settings safely

// Check current power save configuration
AT+UPMPSL?
+UPMPSL:1        // Power save level 1 enabled

AT+UPMPSTO?
+UPMPSTO:2000            // 2000ms timeout

// Disable power save (maximum performance)
AT+UPMPSL=0
```

**Power Save Behavior:**
- **Level 0**: No power save, maximum performance and responsiveness
- **Level 1**: Moderate power save, slight increase in latency after timeout period
- Module enters low-power state after specified timeout of inactivity
- Any AT command or data activity resets the timeout timer

All low power modes save power automatically and will adjust this depending on the level.
When enabled, no further action is required by the host.


## Deep sleep

The most efficient power level is Deep sleep which is almost like a power off, no radio communication is possible in this mode.

- To initiate Deep sleep mode, the host uses the AT command `AT+UPMDS`
- To wake up the module from Deep sleep mode, the host sets `GPIO_J9 to GND`
- After wake up, the module assumes the same state as it does after a reset


# Send and receive data

## Quick mode selection guide

**Not sure which mode to use?** Answer these questions:

1. **What type of data are you sending?**
   - Text/JSON → **String Mode** (human readable, easy debugging)
   - Images/Files → **Binary Mode** (preserves exact bytes)
   - Real-time streams → **Transparent Mode** (lowest latency)

2. **Do you need to process each message separately?**
   - Yes → **Buffered Mode** (message boundaries preserved)
   - No → **Direct Mode** (stream of bytes)

3. **How important is speed vs reliability?**
   - Speed critical → **Direct Mode** (faster)
   - Reliability critical → **Buffered Mode** (event-driven)

**👉 Most Common Choice**: String Buffered Mode - Perfect for most IoT applications

---

NORA-W36 provides multiple data transmission modes optimized for different use cases and performance requirements. Understanding when to use each mode is crucial for optimal application performance and reliability.

## Data mode overview

## Data format modes

| Mode | Data Types | Character Range | Best For | Performance |
|------|------------|----------------|----------|-------------|
| **String Mode** | Text, JSON, XML, HTML | ASCII printable (`0x21-0x7E`, `0xA1-0xFF`) | Web APIs, sensor data, configuration | Good |
| **Binary Mode** | All data types | Full byte range (`0x00-0xFF`) | File transfers, certificates, images | Better |
| **Transparent Mode** | All data types | Full byte range (`0x00-0xFF`) | Legacy applications, streaming | Best |

## Receive buffer modes

| Mode | Behavior | Event Notification | Best For | Latency |
|------|----------|-------------------|----------|---------|
| **Buffered Mode** | Data stored until read | `+UESODA` event triggered | Applications with event-driven processing | Higher |
| **Direct Mode** | Data delivered immediately | Immediate data delivery events | Real-time applications, streaming | Lower |

## When to use each data mode

## String mode - text and structured data

**✅ Use string mode when:**
- Sending/receiving **JSON, XML, HTML, or plain text**
- Working with **REST APIs** and web services
- Transmitting **sensor readings** in text format
- Handling **configuration data** or commands
- Data contains only **printable ASCII characters**

**Avoid string mode when:**
- Working with **binary files** (images, certificates, executables)
- Data contains **null bytes** (`0x00`) or control characters
- Maximum **performance is critical**
- Handling **encrypted data** or raw binary protocols

**Example use cases:**
- IoT sensor data: `{"temperature":25.6,"humidity":60.2}`
- HTTP responses: `HTTP/1.1 200 OK\r\nContent-Type: application/json`
- MQTT messages with text payloads
- Configuration files in JSON/XML format

## Binary mode - all data types

**✅ Use binary mode when:**
- Transferring **files** (images, documents, firmware)
- Uploading **TLS certificates** and private keys
- Working with **binary protocols** (custom, proprietary)
- Data contains **null bytes** or control characters
- Need **full byte range** support (`0x00-0xFF`)
- **Data integrity** is critical

**Avoid binary mode when:**
- Only working with **simple text data**
- **Ease of debugging** is more important than functionality
- Working with **text-only protocols** (HTTP headers, SMTP)

**Example use cases:**
- Certificate uploads: `AT+USECUB=0,"ca.pem"{binary certificate data}`
- File transfers: Images, PDFs, firmware updates
- Encrypted data transmission
- Custom binary protocols

## Transparent mode - maximum performance

**✅ Use transparent mode when:**
- **Maximum throughput** is required
- Implementing **legacy applications** (similar to old data mode)
- **Streaming data** continuously
- Want **direct UART-to-network** bridge functionality
- Minimal **protocol overhead** needed

**Avoid transparent mode when:**
- Need **multiple concurrent connections**
- Require **AT command access** during data transfer
- Application needs **flow control** or data validation
- Working with **complex protocols** requiring parsing

**Example use cases:**
- Legacy terminal applications
- High-speed data streaming
- Simple bridge applications

---

## Basic data mode configuration

NORA-W36 supports several modes for sending and receiving data:
* **String mode**
  * All readable ASCII characters (`0x21-0x7E`, `0xA1-0xFF`)
  * Use when sending data in plain text format. For example, when using JSON, HTML, or NMEA.
* **Binary mode**
  * All types of characters (`0x00-0xFF`)
  * Use when all types of data is needed. For example, in binary content using file upload and download.
* **Transparent mode**
  * All types of characters (`0x00-0xFF`)

Performance notes:
-    Transparent mode has best performance, due to no wait states
-    Direct mode is faster than Buffered mode
-    Binary mode is faster than String mode

To receive data without an event and read it out, the read mode can be changed to direct mode `AT+USORM=1`

## String mode

**Socket receive mode**

**Syntax**
`AT+USORM=<receive_mode>`
* 0: **Buffered mode**
  * `+UESODA` - Socket Data Available Event, default mode
* 1: **Direct string mode**
  * `+UESODS` - Socket Data Binary Event: Incoming on TCP socket data represented as a string
  * `+UESODSF` - Socket Data Binary From Event: Incoming on UDP socket data represented as a string

**SPS Receive data mode**

**Syntax**
`AT+USPSRM=<receive_mode>`
* 0: **Buffered mode**
  * `+UESPSDA` SPS Data Available event, default mode
* 1: **Direct string mode**
  * `+UESPSDS` - SPS Data String event

## Socket write string

**Syntax**
`AT+USOWS=<socket_handle>,<string_data>`

Example to write socket data
| Nr| Instructions                          | AT command | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write Socket data in string format size |    `AT+USOWS=0,"Hello from NORA-W36"` | `OK` |

## Socket read string

**Syntax**
`AT+USORS=<socket_handle>,<length>`
`+USORS:<socket_handle>,<length>,<string_data>`

Example to read socket data
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming Socket data     | | `+UESODA:0,19` |
| 2 | Reads incoming Socket data in string format |`AT+USORS=0,19` |   `+USORS:0,19,"Hello from NORA-W36"` |

## SPS write string

**Syntax**
`AT+USPSWS=<conn_handle>,<string_data>`

Example to write SPS data
| Nr| Instructions                          | AT command | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write SPS data in string format size |    `AT+USPSWS=0,"Hello from NORA-W36"` | `OK` |


## SPS read string

**Syntax**
`AT+USPSRS=<socket_handle>,<length>`
`+USPSRS:<socket_handle>,<length>,<string_data>`

Example to read SPS data
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming SPS data     | | `+UESPSDA:0,19` |
| 2 | Reads incoming SPS data in string format |`AT+USPSRS=0,19` |   `+USPSRS:0,19,"Hello from NORA-W36"` |

## Binary mode

The binary mode should be used when binary content is transmitted, like files and binary protocols.

See [Binary data](#simple-binary-data-example) for more information about the format of the data.

**Socket receive mode**

**Syntax**
`AT+USORM=<receive_mode>`
* 0: **Buffered mode**
  * `+UESODA` - Socket Data Available Event, default mode
* 2: **Direct binary mode**
  * `+UESODB` - Socket Data Binary Event: Incoming on TCP socket data represented as binary data
  * `+UESODBF` - Socket Data Binary From: Incoming on UDP socket data represented as binary data

**SPS receive mode**

**Syntax**
`AT+USPSRM=<receive_mode>`
* 0: **Buffered mode**
  * `+UESPSDA` SPS Data Available event, default mode
* 2: **Direct binary mode**
  * `+UESPSDB` - SPS Data Binary event

See more information about [Binary Data](#simple-binary-data-example).

## Socket write binary

`AT+USOWB=<socket_handle>{binary_data}`


Example to write socket data
| Nr| Instructions                          | AT command | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write Socket data in binary format size |    `AT+USOWB=0\x01\x00\x13Hello from NORA-W36` | `OK` |

## Socket read binary

**Syntax**
`AT+USORB=<socket_handle>,<length>`

`+USORS:<socket_handle>{binary_data}`


**Example to read socket data**
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming Socket data     | | `+UESODA:0,19` |
| 2 | Reads incoming Socket data in binary format |`AT+USORB=0,19` |   `+USORB:0\x01\x00\x13Hello from NORA-W36` |

## SPS write binary

**Syntax**
`AT+USPSWS=<conn_handle>{binary_data}`


**Example to write SPS data**
| Nr| Instructions                          | AT command | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write SPS data in binary format size |    `AT+USPSWB=0\x01\x00\x13Hello from NORA-W36` | `OK` |

## SPS read binary

**Syntax**
`AT+USPSRB=<conn_handle>,<length>`

`+USPSRB:<conn_handle>{binary_data}`


**Example to read SPS data**
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming SPS data     | | `+UESPSDA:0,19` |
| 2 | Reads incoming SPS data in binary format |`AT+USPSRB=0,19` |   `+USPSRB:0\x01\x00\x13Hello from NORA-W36` |

## Transparent mode overview

Transparent mode (TM) allows the NORA-W36 to act as a transparent bridge, forwarding all UART data directly to a remote device without AT command processing. This works similarly to Data mode in legacy u-blox short range products.

**Key Features:**
- Direct UART-to-remote data forwarding
- No AT command processing during transparent mode
- Escape sequence `+++` to return to AT command mode
- Support for TCP, UDP (Wi-Fi), and SPS (Bluetooth LE) connections

**Important Limitations:**
- Only **one active connection** allowed at a time
- Must establish connection before entering transparent mode
- All UART data is sent unmodified (no flow control indicators)

## Basic transparent mode

The `AT+UTM` command enters transparent mode on an existing connection.

### Command syntax
```
AT+UTM=<link_type>,<handle>
```

**Parameters:**
- `<link_type>`: Connection type
  - `0` = SPS (Bluetooth LE Serial Port Service)
  - `1` = TCP socket
  - `2` = UDP socket
- `<handle>`: Connection handle/socket ID (0-255)

**Return Values:**
- `OK` = Transparent mode activated successfully
- `ERROR` = Invalid parameters or no active connection

### SPS (Bluetooth LE) example
```
// Prerequisites: BLE connection established with SPS service
AT+UTM=0,0
OK
[Transparent mode started - all UART data forwarded to BLE device]
Hello from NORA-W36!
[Data sent transparently to remote BLE device]
+++
OK
[Back in AT command mode]
```

### TCP socket example
```
// Prerequisites: Wi-Fi connected, TCP socket created and connected
AT+USOCR=6       // Create TCP socket
+USOCR:0         // Socket ID 0 created
AT+USOC=0,"192.168.1.100",8080              // Connect to server
OK
AT+UTM=1,0       // Enter transparent mode on socket 0
OK
[Transparent mode started - all UART data sent to TCP server]
GET / HTTP/1.1\r\nHost: example.com\r\n\r\n
[HTTP request sent transparently]
+++
OK
[Back in AT command mode]
```

### UDP socket example
```
// Prerequisites: Wi-Fi connected, UDP socket created
AT+USOCR=17      // Create UDP socket
+USOCR:1         // Socket ID 1 created
AT+USOST=1,"192.168.1.200",9000,4,"test"     // Send initial data to establish endpoint
+USOST:1,4       // 4 bytes sent
AT+UTM=2,1       // Enter transparent mode on UDP socket 1
OK
[Transparent mode started - all UART data sent as UDP packets]
Hello UDP Server!
[UDP packet sent transparently]
+++
OK
[Back in AT command mode]
```

### UDP bidirectional transparent mode

This example demonstrates UDP transparent mode with bidirectional communication - sending and receiving data using a single UDP socket.

**Use Case:** Real-time data exchange where you need immediate transparent mode without persistence.

```bash
// Prerequisites: Wi-Fi connected
AT+USOCR=17      // Create UDP socket
+USOCR:1         // Socket ID 1 created

// Bind to local port for receiving data
AT+USOB=1,5005           // Bind socket 1 to local port 5005
OK

// Set remote endpoint for outgoing data
AT+USOP=1,"192.168.1.174",5003     // Configure remote server for outgoing data
OK

// Send test data to establish connection
AT+USOST=1,"192.168.1.174",5003,4,"test"     // Send initial packet
+USOST:1,4       // 4 bytes sent

// Enter transparent mode immediately  
AT+UTM=2,1       // Enter transparent mode on UDP socket 1
OK
[Transparent mode active - bidirectional UDP communication]
Hello Server!            // UART data → UDP packet to 192.168.1.174:5003
[Any UDP data to port 5005 → forwarded to UART]
+++              // Exit transparent mode
OK
[Back in AT command mode]
```

**Network Configuration:**
- **Local Port**: 5005 (receives UDP data from any source)
- **Remote Target**: 192.168.1.174:5003 (receives outgoing data)
- **Mode**: Transparent mode (not persistent)

**Traffic Flow:**
- **Outgoing**: UART data → UDP packets to 192.168.1.174:5003
- **Incoming**: Any UDP data to NORA-W36:5005 → UART output

### Escape sequence timing
- Send `+++` with **no line ending** (no CR/LF)
- Wait **1 second** before and after sending `+++`
- Module responds with `OK` when returning to AT mode

## Persistent transparent mode

Persistent Transparent Mode (TMP) automatically enters transparent mode on startup after module reset. The connection configuration is stored in flash memory and restored on boot.

**Key Differences from Basic Transparent Mode:**
- Configuration stored in flash memory (`AT&W` command)
- Automatic connection and transparent mode entry on startup
- Ideal for applications requiring immediate data forwarding after power-on
- Same single-connection limitation applies

### Command syntax
```
AT+UTMP=<link_type>,<config_id>
```

**Parameters:**
- `<link_type>`: Connection type
  - `0` = BLE SPS Link
  - `1` = Socket (TCP or UDP)
- `<config_id>`: Configuration ID
  - For SPS: config_id returned by `AT+UBTP`
  - For sockets: config_id returned by `AT+USOP`

**⚠️ Important Note:** `AT+UTMP` uses different link_type values than `AT+UTM`:
- `AT+UTM`: 0=SPS, 1=TCP, 2=UDP (specific socket types)
- `AT+UTMP`: 0=SPS, 1=Socket (covers both TCP and UDP)

### SPS persistent mode setup

**Prerequisites:** Bluetooth LE must be enabled and target device address known.

| Step | Description | AT Command | Expected Response |
|------|-------------|------------|-------------------|
| 1 | Configure remote BLE device address | `AT+UBTP=BBBBBBBBBBBB,1` | `+UBTP:200` |
| 2 | Enable persistent transparent mode | `AT+UTMP=0,200` | `OK` |
| 3 | Store configuration to flash | `AT&W` | `OK` |
| 4 | Reset module | `AT+CPWROFF` | `OK` |
| 5 | Wait for startup | *(automatic)* | `+STARTUP` |
| 6 | *Persistent transparent mode active* | *(automatic)* | *(data forwarding starts)* |
| 7 | Exit to AT mode when needed | `+++` | `OK` |

### TCP persistent mode setup

**Prerequisites:** Wi-Fi credentials configured and target server accessible.

| Step | Description | AT Command | Expected Response |
|------|-------------|------------|-------------------|
| 1 | Create persistent TCP socket | `AT+USOPCR=6` | `+USOPCR:100` |
| 2 | Configure server IP and port | `AT+USOP=100,"192.168.0.26",5003` | `OK` |
| 3 | Enable persistent transparent mode | `AT+UTMP=1,100` | `OK` |
| 4 | Configure Wi-Fi connection | *See [Wi-Fi Station Setup](#wi-fi-station-wpa2-and-wpa3)* | `OK` |
| 5 | Store all settings to flash | `AT&W` | `OK` |
| 6 | Reset module | `AT+CPWROFF` | `OK` |
| 7 | Wait for startup and Wi-Fi connection | *(automatic)* | `+STARTUP` |
| 8 | *TCP connection and transparent mode active* | *(automatic)* | *(data forwarding starts)* |
| 9 | Exit to AT mode when needed | `+++` | `OK` |

### UDP persistent mode setup

**Prerequisites:** Wi-Fi credentials configured and target server accessible.

| Step | Description | AT Command | Expected Response |
|------|-------------|------------|-------------------|
| 1 | Create persistent UDP socket | `AT+USOPCR=17` | `+USOPCR:101` |
| 2 | Configure server IP and port | `AT+USOP=101,"192.168.0.50",8080` | `OK` |
| 3 | Enable persistent transparent mode | `AT+UTMP=1,101` | `OK` |
| 4 | Configure Wi-Fi connection | *See [Wi-Fi Station Setup](#wi-fi-station-wpa2-and-wpa3)* | `OK` |
| 5 | Store all settings to flash | `AT&W` | `OK` |
| 6 | Reset module | `AT+CPWROFF` | `OK` |
| 7 | Wait for startup and Wi-Fi connection | *(automatic)* | `+STARTUP` |
| 8 | *UDP socket and transparent mode active* | *(automatic)* | *(data forwarding starts)* |
| 9 | Exit to AT mode when needed | `+++` | `OK` |

### UDP bidirectional persistent transparent mode

This example demonstrates persistent UDP transparent mode with bidirectional communication - the NORA-W36 automatically establishes transparent mode on startup for both sending and receiving UDP data.

**Use Case:** IoT sensor that needs both telemetry data transmission and remote configuration commands with automatic reconnection after power cycles.

```bash
// Prerequisites: Wi-Fi credentials configured
AT+USOPCR=17     // Create persistent UDP socket
+USOPCR:100      // Persistent socket ID 100 created

// Configure local port for receiving data
AT+USOB=100,5005         // Bind to local port 5005 for incoming data
OK

// Configure remote server for outgoing data  
AT+USOP=100,"192.168.1.174",5003             // Send data to server at 192.168.1.174:5003
OK

// Enable persistent transparent mode
AT+UTMP=1,100            // Socket persistent transparent mode on socket 100
OK

// Save configuration and restart
AT&W             // Save settings to flash
OK
AT+CPWROFF       // Power off and restart
OK

// After restart: NORA-W36 automatically enters transparent mode
// - All UART data is sent to 192.168.1.174:5003
// - All UDP data received on port 5005 is forwarded to UART
// - Bidirectional communication established automatically
```

**Network Configuration:**
- **Local Port**: 5005 (receives data from any source)
- **Remote Server**: 192.168.1.174:5003 (receives outgoing data)
- **Mode**: Persistent transparent mode (survives power cycles)

**Example Traffic Flow:**
1. **Outgoing**: UART → NORA-W36 → UDP packet to 192.168.1.174:5003
2. **Incoming**: Any device → UDP packet to NORA-W36:5005 → UART

**To Exit Transparent Mode:**
```bash
+++              // Send escape sequence (no CR/LF)
OK               // Back in AT command mode
```

### Important notes

**Data Flow:**
- Until the escape sequence `+++` is sent, all UART data is forwarded unmodified to the remote device
- No AT command processing occurs during transparent mode
- Binary data is supported (including null bytes)

**Error Handling:**
- If connection fails during startup, module remains in AT command mode
- Connection timeout errors will terminate transparent mode

**Disabling Persistent Mode:**
```
AT+UTMPC         // Clear persistent transparent mode configuration
AT&W             // Save to flash
AT+CPWROFF       // Reset to apply changes
```
   // gatt_client

# Binary data

## What is binary data?

Binary data allows you to send raw bytes (like images, certificates, or any non-text data) through AT commands. This is useful when you need to transfer files, certificates, or binary content that cannot be represented as regular text.

## How binary data works

When sending binary data with NORA-W36, you need to follow a specific format that tells the module exactly how many bytes to expect.

## Binary data structure

Every binary transmission consists of two parts:
1. **Binary Header** (3 bytes total)
2. **Your actual data** (the content you want to send)

## The binary header (3 bytes)

The header always contains exactly 3 bytes in this order:

| Byte Position | Value | Description  |
|---------------|-------|------------- |
| Byte 1 | `0x01` | Start marker (always `0x01`) |
| Byte 2 | MSB | Most Significant Byte of data length |
| Byte 3 | LSB | Least Significant Byte of data length |

**Example:** If your data is 2 bytes long, the header would be: `0x01, 0x00, 0x02`

## Important rules

- ✅ **DO**: Send binary data immediately after the AT command and parameters
-  **DON'T**: Add comma (`,`) before binary data
-  **DON'T**: Add carriage return (`\r`) before binary data
-  **DON'T**: Add any spaces or other characters before binary data

## Simple binary data example

Let's send 2 bytes of data (`0xFF, 0xEE`) to socket 0.

## Step-by-step breakdown:

1. **Your data**: `0xFF, 0xEE` (2 bytes)
2. **Calculate length**: 2 bytes = `0x0002` in hexadecimal
3. **Create header**: `0x01, 0x00, 0x02` (start marker + length)
4. **Complete command**: `AT+USOWB=0` + header + data

## What you actually send:

```
AT+USOWB=0\x01\x00\x02\xFF\xEE
```

**Explanation:**
- `AT+USOWB=0` = Write to socket 0
- `\x01` = Start marker
- `\x00` = Length high byte (0)
- `\x02` = Length low byte (2)
- `\xFF\xEE` = Your 2 bytes of actual data

⚠ **Note**: The curly braces `{ }` in documentation are just for clarity - **never include them in actual commands**.

## Text message example

Let's send the text `Hello from NORA-W36` as binary data.

## Step-by-step calculation:

1. **Count characters**: `Hello from NORA-W36` = 19 characters = 19 bytes
2. **Convert to hex**: 19 = `0x0013` in hexadecimal
3. **Split into bytes**: `0x00` (high byte) and `0x13` (low byte)
4. **Create header**: `0x01, 0x00, 0x13`

## Complete command:

```
AT+USOWB=0\x01\x00\x13Hello from NORA-W36
```

**When you receive data back, it includes the same header:**
```
+USORB:0\x01\x00\x13Hello from NORA-W36
```

## Certificate upload example

Uploading certificates is more complex but follows the same binary data principles.

## Example scenario

You want to upload a certificate file named `ca.pem` that contains 1342 bytes of certificate data.

## Step-by-step process

1. **Count the certificate bytes**: Your certificate file = 1342 bytes
2. **Convert to hexadecimal**: 1342 = `0x053E` in hex
3. **Split into header bytes**: `0x05` (high byte) and `0x3E` (low byte)
4. **Create header**: `0x01, 0x05, 0x3E`

## Length calculation helper

| Decimal Bytes | Hexadecimal | High Byte | Low Byte |
|---------------|-------------|-----------|----------|
| 256 | 0x0100 | 0x01 | 0x00 |
| 512 | 0x0200 | 0x02 | 0x00 |
| 1024 | 0x0400 | 0x04 | 0x00 |
| 1342 | 0x053E | 0x05 | 0x3E |

## Complete certificate command structure

```text
AT+USECUB=0,"ca.pem"\x01\x05\x3E[certificate content here]
```

**Breakdown:**
- `AT+USECUB=0,"ca.pem"` = Upload to slot 0, name it "ca.pem"
- `\x01` = Binary data start marker
- `\x05` = High byte of length (1342)
- `\x3E` = Low byte of length (1342)
- `[certificate content]` = The actual 1342 bytes of certificate data

## Expected response

```text
+USECUB:1342
OK
```

This confirms that 1342 bytes were successfully received and stored.

```AT+USECUB=0,"ca.pem"\x01\x05\x3E-----BEGIN CERTIFICATE-----\n
ABCDojCCAoqgAwIBAgIBADANBgkqhkiG9w0BAQsFADCBkDELMAkGA1UEBhMCR0Ix\n
FzAVBgNVBAgMDlVuaXRlZCBLaW5nZG9tMQ4wDAYDVQQHDAVEZXJieTESMBAGA1UE\n
CgwJTW9zcXVpdHRvMQswCQYDVQQLDAJDQTEWMBQGA1UEAwwNbW9zcXVpdHRvLm9y\n
ZzEfMB0GCSqGSIb3DQEJARYQcm9nZXJAYXRjaG9vLm9yZzAeFw0yMzEwMDQxMDEw\n
MzJaFw0yNDAxMDIxMDEwMzJaMHwxCzAJBgNVBAYTAlNFMQ4wDAYDVQQIDAVNYWxt\n
bzEOMAwGA1UEBwwFTWFsbW8xDzANBgNVBAoMBnUtYmxveDEPMA0GA1UECwwGQUUt\n
U0hPMQ0wCwYDVQQDDARjbWFnMRwwGgYJKoZIhvcNAQkBFg10ZXN0QHRlc3Qub3Jn\n
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3PZc1E7uSBiB/Es1V0pU\n
XeSayY3f6vrIbnSGTb+/PERSPgPz6UoZumJjcOWbCMq7T+/dvvxox/ZU/t/XdGMq\n
MJRgN+aWRG6I4QmqYgkiAZGMuaMa+TLLEEPvL1IDKSxeVjHRNDx4yZM4zgvl6ZX7\n
oRaBqZBooNTHOtAGjlydyyz55HCZfLsE8Z3iaH7uW+/n9+2nWusfUXoJmI0STmEH\n
pJ+ZF7M+o53UilW2NKdv/R+wCzXxmKWX6PFVg4NdKspTDUOpPcxlphMQGi24E2uz\n
2k7raCQvGt32LxZc/vic4W6rNDGGNSSDVJTSx6egzfRrcCKw3T88TN87nasjc+KV\n
CQIDAQABoxowGDAJBgNVHRMEAjAAMAsGA1UdDwQEAwIF4DANBgkqhkiG9w0BAQsF\n
AAOCAQEAjRyNWHGtcwLT21IzJ2         // I8YL611iTUitRGkA0gF+7l0DuPtfSLPVhoyB\n
Te3FThYsn2OYfF+LrbSMlWO38Am2fqE8lTGe9EX/HZj95Wj+RnQApc9CkxGJkCb8\n
6aecuz8Vhyl2zWA5kqNrq978uMmsyX3FNRcS3mB7Vo+65R/XwThzHjSXyCyHzRMd\n
zOlrJZMuNWV2bI7vyIIp9/AdHNO6Hwnj+I5hBDvyV+T9RT2jLUTRZldGUJQBlDVj\n
QUKa8NSwzVrvoVTPAT6gcPCn4VQkwxLE/LWaNw2X8mxtyo3nXVoo291TzB8mKHUQ\n
ubOA1iBEcKtAFjqOlZSLanVNvrn5KwXY\n
-----END CERTIFICATE-----\n
+USECUB:1342
OK
```

## Programming examples

Here are code examples showing how to implement binary data transmission in different programming languages.

## Python example

```python
def send_binary_data(at_command, binary_data):

  # Start with the AT command (without \r)
  message = at_command.encode('ascii')


  # Add binary header
  message += b'\x01'             # Start marker
  message += len(binary_data).to_bytes(2, 'big')    # Length (2 bytes, big-endian)

  # Add the actual binary data
  message += binary_data

  # Send to NORA-W36
  serial_port.write(message)

# Example usage:

certificate_data = open('ca.pem', 'rb').read()
send_binary_data('AT+USECUB=0,"ca.pem"', certificate_data)

```

## C# example

```csharp
public void SendBinaryData(string atCommand, byte[] binaryData)
{
    // Convert AT command to bytes
    byte[] cmdBytes = System.Text.Encoding.ASCII.GetBytes(atCommand);

    // Create binary header (3 bytes)
    byte[] header = new byte[3];
    header[0] = 0x01;              // Start marker
    header[1] = (byte)(binaryData.Length >> 8);    // High byte of length
    header[2] = (byte)(binaryData.Length & 0xFF);    // Low byte of length

    // Combine all parts
    byte[] fullMessage = new byte[cmdBytes.Length + header.Length + binaryData.Length];
    Array.Copy(cmdBytes, 0, fullMessage, 0, cmdBytes.Length);
    Array.Copy(header, 0, fullMessage, cmdBytes.Length, header.Length);
    Array.Copy(binaryData, 0, fullMessage, cmdBytes.Length + header.Length, binaryData.Length);

    // Send to NORA-W36
    serialPort.Write(fullMessage, 0, fullMessage.Length);
}

// Example usage:

byte[] certData = File.ReadAllBytes("ca.pem");
SendBinaryData("AT+USECUB=0,\"ca.pem\"", certData);

```

## Common use cases

Binary data is used in these NORA-W36 functions:

- **Socket Communication**: `AT+USOWB` - Send binary data over network sockets
- **Certificate Upload**: `AT+USECUB` - Upload SSL/TLS certificates and keys
- **Serial Port Service**: Transfer binary data over Bluetooth SPS
- **File Transfer**: Send images, documents, or any binary files

## Troubleshooting tips

## Common issues:

1. **Wrong Length**: Make sure your length calculation matches the actual data size
2. **Missing Header**: Always include the 3-byte header (`0x01` + length)
3. **Extra Characters**: Don't add commas, spaces, or `\r` before binary data
4. **Endianness**: Length must be big-endian (MSB first, then LSB)

## Length calculation check:

```text
Your data size: _____ bytes
Convert to hex: 0x____
High byte (MSB): 0x__
Low byte (LSB): 0x__
Header: 0x01 0x__ 0x__
```

## Quick reference:

| Data Size | Hex | Header Bytes |
|-----------|-----|-------------- |
| 1 byte | 0x0001 | `0x01 0x00 0x01` |
| 10 bytes | 0x000A | `0x01 0x00 0x0A` |
| 256 bytes | 0x0100 | `0x01 0x01 0x00` |
| 1024 bytes | 0x0400 | `0x01 0x04 0x00` |

# Diagnostic tools

Network diagnostic tools are essential for troubleshooting connectivity issues and optimizing network performance. NORA-W36 provides built-in diagnostic capabilities including network status monitoring, connectivity testing, and performance measurement tools.

## Quick diagnostic checklist

Before diving into specific tools, run this quick health check:

| Step | Command | Expected Result | Issue Indicator |
|------|---------|----------------|----------------|
| 1 | `AT` | `OK` | No response = UART/power issue |
| 2 | `ATI` | Module info | Wrong info = firmware issue |
| 3 | `AT+UWSNST=0` | `+UWSNST:0,<IP>` | No IP = connectivity issue |
| 4 | `AT+UWSST=4` | Signal strength | Low RSSI = signal issue |

## Network status and connectivity testing

## Network status check

**Purpose:** Show current status of Wi-Fi station network interface.

**Syntax:**

```
AT+UWSNST=<status_id>              // Query specific status parameter
AT+UWSNST?       // Query all network parameters
```

**Parameters:**

- `status_id`: Status parameter identifier (0-5)
  - `0`: Station IP address
  - `1`: Network subnet mask
  - `2`: Default gateway address
  - `3`: Primary DNS server
  - `4`: Secondary DNS server
  - `5`: IPv6 link-local address

**Examples:**

| Nr | AT command | AT event | Description |
|----|------------|----------|-------------|
| 1  | `AT+UWSNST=0` | `+UWSNST:0,192.168.1.179` | Query station IP address |
| 2  | `AT+UWSNST=1` | `+UWSNST:1,255.255.255.0` | Query subnet mask |
| 3  | `AT+UWSNST=2` | `+UWSNST:2,192.168.1.1` | Query gateway address |
| 4  | `AT+UWSNST?` | Multiple responses (see below) | Query all network parameters |

**Response Format for `AT+UWSNST?`:**

```
+UWSNST:0,192.168.1.179            // Station IP address
+UWSNST:1,255.255.255.0            // Network subnet mask
+UWSNST:2,192.168.1.1              // Default gateway address
+UWSNST:3,192.168.1.1              // Primary DNS server
+UWSNST:4,0.0.0.0        // Secondary DNS server
+UWSNST:5,[fe80::56f8:2aff:fe13:6310]        // IPv6 link-local address
```

**Parameter Descriptions:**

- `+UWSNST:0,<ip_address>` - Station IP address
- `+UWSNST:1,<subnet_mask>` - Network subnet mask
- `+UWSNST:2,<gateway>` - Default gateway address
- `+UWSNST:3,<dns_primary>` - Primary DNS server
- `+UWSNST:4,<dns_secondary>` - Secondary DNS server
- `+UWSNST:5,<ipv6_address>` - IPv6 link-local address

**Troubleshooting Network Status:**

| Response | Meaning | Next Steps |
|----------|---------|------------|
| `+UWSNST:0,192.168.1.179` | Connected with valid IP | Network is working |
| `ERROR` | Interface not available | Check Wi-Fi connection with `AT+UWSC=0` |
| No response | Command timeout | Check AT command interface |

## Signal strength testing

**Purpose:** Measure Wi-Fi signal quality for connection optimization.

**Signal Quality Assessment:**

| RSSI Range | Quality | Recommendation |
|------------|---------|----------------|
| > -50 dBm | Excellent | Optimal performance |
| -50 to -60 dBm | Good | Stable connection expected |
| -60 to -70 dBm | Fair | May experience occasional drops |
| < -70 dBm | Poor | Move closer to access point |

**Example:**

```bash
AT+UWSST=4
+UWSST:-45
OK

Signal strength: -45 dBm (Excellent)
```

## Basic connectivity testing using TCP sockets

**Purpose:** Test internet connectivity using a simple TCP connection.

**Basic Internet Connectivity Test:**

| Nr| AT command | AT event| Description |
|---|------------|---------|-------------|
| 1 | `AT+USOCR=6` | `+USOCR:0` | Create TCP socket |
| 2 | `AT+USOC=0,"8.8.8.8",53` | `+UESOC:0` | Connect to Google DNS |
| 3 | `AT+USOCL=0` | `OK` | Close socket |

**Result Interpretation:**

- **Success:** Internet connectivity is working
- **`ERROR` on step 2:** Internet access blocked or DNS issues

## Connectivity troubleshooting guide

**Step-by-Step Diagnosis:**

1. **Check Physical Connection**

   ```bash
   AT+UWSNST=0

   Expected: +UWSNST:0,<IP_ADDRESS>
   If ERROR: Wi-Fi not connected
   ```

2. **Verify Signal Quality**

   ```bash
   AT+UWSST=4

   Expected: Signal strength > -70 dBm
   If weaker: Move closer to access point
   ```

3. **Test Local Network Access**

   ```bash
   AT+USOCR=6
   AT+USOC=0,"192.168.1.1",80      // Router IP

   Expected: +UESOC:0
   Tests local network connectivity
   ```

4. **Test Internet Access**

   ```bash
   AT+USOC=0,"8.8.8.8",53          // Google DNS

   Expected: +UESOC:0
   Tests internet connectivity
   ```

## Iperf performance testing

## Overview

Iperf is a network performance measurement tool that can measure maximum TCP and UDP bandwidth performance. NORA-W36 supports Iperf version 2 protocol as both client and server.

**Key Capabilities:**

- **TCP Performance Testing:** Measure maximum throughput
- **UDP Performance Testing:** Test packet loss and jitter
- **Bidirectional Testing:** Simultaneous upload/download measurement
- **Customizable Parameters:** Port, duration, reporting intervals

**Download Iperf 2:**

- Windows: [Iperf2 Sourceforge](https://sourceforge.net/projects/iperf2/files/)
- Manual: [Iperf2 Documentation](https://iperf2.sourceforge.io/iperf-manpage.html)

**Important Note:** The Iperf implementation is experimental and may change between releases.

## Iperf command syntax

**Syntax:** `AT+UDGI=<iperf_action>,<protocol_type>[,<role>,<port>,<report_interval>[,<time_boundary>,<ip_addr>[,<bidirectional>]]]`

**Parameters:**

| Parameter | Type | Values | Description |
|-----------|------|--------|-------------|
| `iperf_action` | Integer | `1` = Start, `0` = Stop | Control iperf operation |
| `protocol_type` | Integer | `1` = TCP, `2` = UDP | Protocol selection |
| `role` | Integer | `1` = Server, `2` = Client | Operating mode |
| `port` | Integer | 1-65535 | Port number (default: 5001) |
| `report_interval` | Integer | 1-60 seconds | Reporting frequency |
| `time_boundary` | Integer | 1-300 seconds | Test duration |
| `ip_addr` | String | IP address | Target server IP (client mode only) |
| `bidirectional` | Integer | `0` = Off, `1` = On | Simultaneous bidirectional test |

## Iperf server mode

**Purpose:** Run NORA-W36 as an Iperf server to receive performance tests from external clients.

## PC iperf client setup

#### Setting up PC iperf client

**TCP Client:**

```bash
From PC command line (iperf 2.0):

iperf -c <NORA-W36_IP> -p 5001 -t 10
```

**UDP Client:**

```bash
From PC command line:

iperf -c <NORA-W36_IP> -p 5001 -u -t 10 -b 10M
```

#### NORA-W36 server examples

**TCP Server:**

| Nr| AT command | AT event| Description |
|---|------------|---------|-------------|
| 1 |`AT+UDGI=1,1,1,5001,1`| | Start TCP server on port 5001 |
| 2 |`+UEDGI:"TCP: Start TCP server!"` | | Server started |
| 3 |`+UEDGI:"tcp_server_func: Create socket fd = 0"` | | Socket created |
| 4 |`+UEDGI:"tcp_server_func: Bind socket successfully"` | | Port bound |
| 5 |`+UEDGI:"tcp_server_func: Listen port 5001"` | | Server listening |

**UDP Server:**

| Nr| AT command | AT event| Description |
|---|------------|---------|-------------|
| 1 |`AT+UDGI=1,2,1,5002,1`| | Start UDP server on port 5002 |
| 2 |`+UEDGI:"UDP: Start UDP server!"` | | UDP server started |

## Iperf client mode

**Purpose:** Use NORA-W36 as an Iperf client to test performance against external servers.

## PC iperf server setup

#### Setting up PC iperf server

**TCP Server:**

```bash
// From PC command line:
iperf -s -p 5001
```

**UDP Server:**

```bash
// From PC command line:
iperf -s -u -p 5001
```

#### NORA-W36 client examples

**TCP Client Test:**

| Nr| AT command | AT event| Description |
|---|------------|---------|-------------|
| 1 |`AT+UDGI=1,1,2,5001,1,20,"192.168.0.41"`| | Connect to TCP server |
| 2 |`+UEDGI:"tcp_client_func: Create socket fd = 1"` | | Socket created |
| 3 |`+UEDGI:"tcp_client_func: Connect to server successfully"` | | Connected |
| 4 |`+UEDGI:"tcp_client_func: Send 1435 KBytes in 1000 ms, 11761 Kbits/sec"` | | Throughput report |
| 5 |`+UEDGI:"tcp_client_func: Send 1418 KBytes in 1000 ms, 11621 Kbits/sec"` | | Continued testing |

**UDP Client Test:**

| Nr| AT command | AT event| Description |
|---|------------|---------|-------------|
| 1 |`AT+UDGI=1,2,2,5001,1,10,"192.168.0.41"`| | UDP performance test |
| 2 |`+UEDGI:"udp_client_func: Create socket fd = 2"` | | UDP socket created |
| 3 |`+UEDGI:"udp_client_func: Send 1024 KBytes in 1000 ms, 8388 Kbits/sec"` | | UDP throughput |

## Performance interpretation

**TCP Performance Benchmarks:**

| Throughput | Quality | Typical Use Cases |
|------------|---------|-------------------|
| > 10 Mbps | Excellent | Video streaming, large file transfers |
| 5-10 Mbps | Good | Web browsing, medium file transfers |
| 1-5 Mbps | Fair | IoT data, small file transfers |
| < 1 Mbps | Poor | Sensor data only |

**UDP Performance Metrics:**

- **Throughput:** Data transfer rate
- **Packet Loss:** Should be < 1% for good performance
- **Jitter:** Should be < 10ms for real-time applications

## Iperf troubleshooting

**Common Issues and Solutions:**

| Issue | Symptoms | Solution |
|-------|----------|----------|
| **Connection Failed** | `"Connect failed"` error | Check IP address and port; Verify server is running; Check firewall settings |
| **Low Throughput** | < 1 Mbps performance | Check Wi-Fi signal strength (`AT+UWSST=4`); Move closer to access point; Check for network congestion |
| **Test Timeout** | No performance data | Increase `time_boundary` parameter; Check network stability; Verify server response |
| **Socket Creation Failed** | `"Create socket failed"` | Close existing sockets; Check available memory; Restart if necessary |

**Debug Steps:**

1. **Verify Network Connection:**

   ```bash
   AT+UWSNST=0           // Check IP address
   AT+UWSST=4            // Check signal strength
   ```

2. **Test Basic Connectivity:**

   ```bash
   AT+USOCR=6
   AT+USOC=0,"<server_ip>",<port>            // Test TCP connection
   ```

3. **Check Server Availability:**
   - Ensure PC Iperf server is running
   - Verify firewall allows connections
   - Test with different ports if needed

## Advanced iperf usage

**Bidirectional Testing:**

```bash
// Test both upload and download simultaneously
AT+UDGI=1,1,2,5001,1,30,"192.168.0.41",1
```

**Custom Duration Testing:**

```bash
// -second test with 5-second intervals
AT+UDGI=1,1,2,5001,5,60,"192.168.0.41"
```

**Stopping Iperf Tests:**

```bash
// Stop current iperf operation
AT+UDGI=0
```

## Performance monitoring best practices

1. **Baseline Testing:** Establish performance baselines under optimal conditions
2. **Regular Monitoring:** Schedule periodic performance tests
3. **Environmental Factors:** Consider time of day, network traffic, interference
4. **Documentation:** Keep records of performance measurements for trend analysis

## Integration with application monitoring

**Automated Performance Checks:**

```bash
// Quick performance validation script
AT+UWSNST=0      // Check connection
AT+UWSST=4       // Check signal
AT+UDGI=1,1,2,5001,1,10,"<server_ip>"        // Quick iperf test
```

This diagnostic approach ensures reliable network performance and helps quickly identify connectivity issues in production deployments.

## Crash information

**Purpose:** Retrieve system crash information for troubleshooting hardware and firmware issues.

**Note:** `AT+USYCI?` is a non-official debug command intended for diagnostic purposes.

**Syntax:**
```
AT+USYCI?
```

**Response:**
```
+USYCI:"<crash_type>","<crash_reason>","<firmware_version>"
```

**Parameters:**
- `crash_type`: Type of system fault (e.g., "HwFault", "SwFault", "WatchdogReset")
- `crash_reason`: Specific reason for the crash (e.g., "timerEvent", "memoryError")
- `firmware_version`: Firmware version when crash occurred

**Example:**
```
AT+USYCI?
+USYCI:"HwFault","timerEvent","3.1.0-150"
OK
```

**Troubleshooting Steps:**
1. **Record crash information** for support analysis
2. **Check for pattern** - does crash occur repeatedly?
3. **Verify power supply** stability and voltage levels
4. **Update firmware** to latest version if available
5. **Contact support** if problem persists

**Important:** If crashes continue after firmware updates and power supply verification, contact **support@u-blox.com** with the complete crash information output for further analysis.




# Error codes

The Extended error codes provide essential debugging information to understand the reason for errors received during AT command execution. This section provides comprehensive error code documentation for immediate troubleshooting without requiring external references.

**Important Note**: Error codes should only be used for information and might change between versions in the future.

## Error code overview

NORA-W36 uses a structured error code system organized by functional categories:

| Category | Code Range | Description | Common Scenarios |
|----------|------------|-------------|------------------|
| **Common** | 1-22 | General system errors | Parameter validation, memory, timeouts |
| **AT Command** | 31-51 | AT command parsing errors | Invalid syntax, arguments, formatting |
| **Wi-Fi** | 60-71 | Wi-Fi specific errors | Connection issues, configuration problems |
| **GATT/Bluetooth** | 91-114 | Bluetooth GATT errors | Authentication, permissions, resources |
| **HTTP** | 160+ | HTTP protocol errors | Header issues, response problems |
| **Socket** | 180+ | Socket communication errors | Binding, connection state issues |

## Error code commands

## Query last error code

**Purpose:** Retrieve the error code from the last failed AT command

**Syntax:**
```bash
AT+USYEC?
```

**Response:**
```bash
+USYEC:<error_code>
OK
```

**Example:**
```bash
AT+USYEC?
+USYEC:5
OK
```

The error code `5` indicates `U_ERROR_COMMON_INVALID_PARAMETER` - the parameter in the last AT command was invalid.

## Enable extended error reporting

**Purpose:** Enable automatic error code reporting for all failed commands

**Syntax:**
```bash
AT+USYEE=<extended_errors>
```

**Parameters:**
- `extended_errors`: 0 = disabled, 1 = enabled

**Example:**
```bash
AT+USYEE=1
OK
AT+UWSSC
ERROR:32
```

The error code `32` indicates `U_AT_STATUS_INVALID_COMMAND` - the AT command syntax is incorrect.

## Socket error query

**Purpose:** Get the last error code for socket operations

**Syntax:**
```bash
AT+USOE?
```

**Response:**
```bash
+USOE:<error_code>
OK
```

**Example:**
```bash
AT+USOE?
+USOE:16
OK
```

The error code `16` indicates `U_ERROR_COMMON_NOT_CONNECTED` - the socket connection is not established.

## Complete error code reference

## Common error codes (1-22)

These are fundamental system errors that can occur across all functions:

| Code | Error Name | Description | Troubleshooting |
|------|------------|-------------|-----------------|
| **1** | `U_ERROR_COMMON_BSD_ERROR` | BSD system error | Check system resources and permissions |
| **2** | `U_ERROR_COMMON_NOT_INITIALISED` | System not initialized | Ensure proper module initialization |
| **3** | `U_ERROR_COMMON_NOT_IMPLEMENTED` | Feature not implemented | Use alternative commands or update firmware |
| **4** | `U_ERROR_COMMON_NOT_SUPPORTED` | Operation not supported | Check module capabilities and configuration |
| **5** | `U_ERROR_COMMON_INVALID_PARAMETER` | Invalid parameter value | Verify parameter values and ranges |
| **6** | `U_ERROR_COMMON_NO_MEMORY` | Insufficient memory | Free memory, reduce concurrent operations |
| **7** | `U_ERROR_COMMON_NOT_RESPONDING` | Module not responding | Check power supply, reset module |
| **8** | `U_ERROR_COMMON_PLATFORM` | Platform-specific error | Check hardware configuration |
| **9** | `U_ERROR_COMMON_TIMEOUT` | Operation timed out | Increase timeout, check network connectivity |
| **10** | `U_ERROR_COMMON_DEVICE_ERROR` | Device hardware error | Check hardware connections, reset device |
| **11** | `U_ERROR_COMMON_NOT_FOUND` | Resource not found | Verify resource existence and spelling |
| **12** | `U_ERROR_COMMON_INVALID_ADDRESS` | Invalid address format | Check IP address, MAC address format |
| **13** | `U_ERROR_COMMON_TEMPORARY_FAILURE` | Temporary operation failure | Retry operation after delay |
| **14** | `U_ERROR_COMMON_AUTHENTICATION_FAILURE` | Authentication failed | Check credentials, certificates |
| **15** | `U_ERROR_COMMON_OPERATION_IN_PROGRESS` | Operation already in progress | Wait for completion or cancel current operation |
| **16** | `U_ERROR_COMMON_NOT_CONNECTED` | Not connected to network/service | Establish connection first |
| **17** | `U_ERROR_COMMON_LIMIT_REACHED` | Resource limit reached | Check concurrent connections, memory usage |
| **18** | `U_ERROR_COMMON_ALREADY_CREATED` | Resource already exists | Use existing resource or delete first |
| **19** | `U_ERROR_COMMON_END_OF_TRANSMISSION` | End of data transmission | Normal completion indication |
| **19** | `U_ERROR_COMMON_REMOTE_CANCELLED_TRANSMISSION` | Remote cancelled transmission | Check remote peer status |
| **20** | `U_ERROR_COMMON_NOT_CONFIGURED` | Feature not configured | Configure feature before use |
| **21** | `U_ERROR_COMMON_INVALID_RESPONSE` | Invalid response received | Check protocol compliance, retry |
| **22** | `U_ERROR_COMMON_UNKNOWN` | Unknown error occurred | Enable extended error reporting for details |

## AT command error codes (31-51)

These errors relate to AT command parsing and syntax validation:

| Code | Error Name | Description | Troubleshooting |
|------|------------|-------------|-----------------|
| **31** | `U_AT_STATUS_NOT_IMPLEMENTED` | AT command not implemented | Use alternative command or update firmware |
| **32** | `U_AT_STATUS_INVALID_COMMAND` | Invalid AT command syntax | Check command spelling and format |
| **33** | `U_AT_STATUS_INVALID_ARGUMENTS` | Invalid command arguments | Verify argument types and values |
| **34** | `U_AT_STATUS_INVALID_ARGUMENT_COUNT` | Wrong number of arguments | Check required vs provided parameters |
| **35** | `U_AT_STATUS_INVALID_INT_ARG` | Invalid integer argument | Ensure numeric values are integers |
| **36** | `U_AT_STATUS_INVALID_INT_RANGE` | Integer argument out of range | Check min/max parameter limits |
| **37** | `U_AT_STATUS_INVALID_STR_ARG` | Invalid string argument | Check string format and encoding |
| **38** | `U_AT_STATUS_INVALID_STR_LENGTH` | String argument too long/short | Verify string length requirements |
| **39** | `U_AT_STATUS_INVALID_ENUM_ARG` | Invalid enumeration value | Use only supported enumeration values |
| **40** | `U_AT_STATUS_INVALID_IP_ADDR_ARG` | Invalid IP address format | Use proper IPv4 format (x.x.x.x) |
| **41** | `U_AT_STATUS_INVALID_MAC_ADDR_ARG` | Invalid MAC address format | Use proper MAC format (xx:xx:xx:xx:xx:xx) |
| **42** | `U_AT_STATUS_INVALID_BD_ADDR_ARG` | Invalid Bluetooth address | Check Bluetooth address format |
| **43** | `U_AT_STATUS_INVALID_BYTE_ARRAY_ARG` | Invalid byte array | Check hexadecimal format |
| **44** | `U_AT_STATUS_INVALID_BYTE_ARRAY_LENGTH` | Byte array length mismatch | Verify expected vs actual data length |
| **45** | `U_AT_STATUS_UNMATCHED_QUOTE` | Unmatched quotation marks | Balance opening and closing quotes |
| **46** | `U_AT_STATUS_TIMEOUT` | AT command timeout | Increase timeout or check module response |
| **47** | `U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD` | Binary command executed as standard | Use proper binary command format |
| **48** | `U_AT_STATUS_INVALID_ESCAPE_CODE` | Invalid escape sequence | Use proper escape characters |
| **49** | `U_AT_STATUS_INVALID_CHARACTER` | Invalid character in command | Remove unsupported characters |
| **50** | `U_AT_STATUS_INVALID_INT_LIST_ARG` | Invalid integer list format | Check list syntax and separators |
| **51** | `U_AT_STATUS_INVALID_INT_LIST_LENGTH` | Integer list length incorrect | Verify expected vs actual list size |

## Wi-Fi error codes (60-71)

These errors are specific to Wi-Fi operations:

| Code | Error Name | Description | Troubleshooting |
|------|------------|-------------|-----------------|
| **60** | `U_ERROR_WIFI_AT` | Wi-Fi AT command error | Check Wi-Fi specific command syntax |
| **61** | `U_ERROR_WIFI_NOT_CONFIGURED` | Wi-Fi not configured | Configure Wi-Fi settings first with `AT+UWSCP` |
| **62** | `U_ERROR_WIFI_NOT_FOUND` | Wi-Fi network not found | Check SSID, scan networks with `AT+UWSSC` |
| **63** | `U_ERROR_WIFI_INVALID_MODE` | Invalid Wi-Fi mode | Use supported modes (station/AP) |
| **64** | `U_ERROR_WIFI_TEMPORARY_FAILURE` | Temporary Wi-Fi failure | Retry connection after delay |
| **65** | `U_ERROR_WIFI_ALREADY_CONNECTED` | Already connected to Wi-Fi | Disconnect first with `AT+UWSDC` if needed |
| **66** | `U_ERROR_WIFI_ALREADY_CONNECTED_TO_SSID` | Already connected to this SSID | Connection already established |
| **67** | `U_ERROR_WIFI_DISCONNECTED` | Wi-Fi disconnected | Re-establish connection with `AT+UWSC=0` |
| **68** | `U_ERROR_WIFI_ALREADY_UP` | Wi-Fi interface already up | Interface already active |
| **69** | `U_ERROR_WIFI_AP_NOT_STARTED` | Access Point not started | Start AP mode with `AT+UWAPS` |
| **70** | `U_ERROR_WIFI_IS_DOWN` | Wi-Fi interface is down | Bring interface up first |
| **71** | `U_ERROR_WIFI_ALREADY_STARTED` | Wi-Fi service already started | Service already running |

## Bluetooth GATT error codes (91-114)

These errors occur during Bluetooth GATT operations:

| Code | Error Name | Description | Troubleshooting |
|------|------------|-------------|-----------------|
| **91** | `U_PORT_GATT_STATUS_INVALID_HANDLE` | Invalid GATT handle | Use valid characteristic/service handles |
| **92** | `U_PORT_GATT_STATUS_READ_NOT_PERMITTED` | Read operation not allowed | Check characteristic permissions |
| **93** | `U_PORT_GATT_STATUS_WRITE_NOT_PERMITTED` | Write operation not allowed | Check characteristic permissions |
| **94** | `U_PORT_GATT_STATUS_INVALID_PDU` | Invalid Protocol Data Unit | Check data format and length |
| **95** | `U_PORT_GATT_STATUS_AUTHENTICATION` | Authentication required | Complete authentication process |
| **96** | `U_PORT_GATT_STATUS_NOT_SUPPORTED` | Operation not supported | Use supported GATT operations |
| **97** | `U_PORT_GATT_STATUS_INVALID_OFFSET` | Invalid data offset | Check read/write offset parameters |
| **98** | `U_PORT_GATT_STATUS_AUTHORIZATION` | Authorization required | Complete authorization process |
| **99** | `U_PORT_GATT_STATUS_PREPARE_QUEUE_FULL` | Prepare write queue full | Complete pending writes first |
| **100** | `U_PORT_GATT_STATUS_ATTRIBUTE_NOT_FOUND` | GATT attribute not found | Use valid attribute handles |
| **101** | `U_PORT_GATT_STATUS_ATTRIBUTE_NOT_LONG` | Attribute not long enough | Check attribute length requirements |
| **102** | `U_PORT_GATT_STATUS_ENCRYPTION_KEY_SIZE` | Insufficient encryption key size | Use stronger encryption |
| **103** | `U_PORT_GATT_STATUS_INVALID_ATTRIBUTE_LEN` | Invalid attribute length | Check length constraints |
| **104** | `U_PORT_GATT_STATUS_UNLIKELY` | Unlikely error condition | Retry operation |
| **105** | `U_PORT_GATT_STATUS_INSUFFICIENT_ENCRYPTION` | Insufficient encryption level | Enable proper encryption |
| **106** | `U_PORT_GATT_STATUS_UNSUPPORTED_GROUP_TYPE` | Unsupported group type | Use supported GATT group types |
| **107** | `U_PORT_GATT_STATUS_INSUFFICIENT_RESOURCES` | Insufficient system resources | Free resources, reduce load |
| **108** | `U_PORT_GATT_STATUS_DB_OUT_OF_SYNC` | Database out of sync | Refresh GATT database |
| **109** | `U_PORT_GATT_STATUS_VALUE_NOT_ALLOWED` | Value not allowed | Use permitted values only |
| **110** | `U_PORT_GATT_STATUS_WRITE_REQ_REJECTED` | Write request rejected | Check write permissions and format |
| **111** | `U_PORT_GATT_STATUS_CCC_IMPROPER_CONF` | Improper CCC configuration | Configure Client Characteristic Config properly |
| **112** | `U_PORT_GATT_STATUS_PROCEDURE_IN_PROGRESS` | GATT procedure in progress | Wait for completion |
| **113** | `U_PORT_GATT_STATUS_OUT_OF_RANGE` | Value out of range | Use values within permitted range |
| **114** | `U_PORT_GATT_STATUS_UNKNOWN` | Unknown GATT error | Enable extended debugging |

## HTTP error codes (160+)

These errors relate to HTTP protocol operations:

| Code | Error Name | Description | Troubleshooting |
|------|------------|-------------|-----------------|
| **160** | `U_ERROR_HTTP_HEADER_NOT_READ` | HTTP header not read | Ensure headers are read before accessing body |

*Note: Additional HTTP error codes may be present. Use `AT+USYEC?` after HTTP operations for specific codes.*

## Socket error codes (180+)

These errors occur during socket operations:

| Code | Error Name | Description | Troubleshooting |
|------|------------|-------------|-----------------|
| **180** | `U_ERROR_SOCKET_ALREADY_BOUND` | Socket already bound | Close socket first with `AT+USOCL` |

*Note: Additional socket error codes may be present. Use `AT+USOE?` for socket-specific error information.*

## Error code troubleshooting workflow

## Basic error diagnosis

**Step 1: Enable Extended Error Reporting**
```bash
AT+USYEE=1
OK
```

**Step 2: Execute Command and Observe Error**
```bash
AT+UWSCP=0,"InvalidSSID"
ERROR:62
```

**Step 3: Look Up Error Code**
- Error 62 = `U_ERROR_WIFI_NOT_FOUND`
- Action: Check SSID spelling, scan networks

**Step 4: Apply Solution**
```bash
AT+UWSSC         // Scan for networks
AT+UWSCP=0,"CorrectSSID"
OK
```

## Advanced error analysis

**For Connection Issues:**
```bash
// Check last error
AT+USYEC?
+USYEC:14
OK

// Error 14 = Authentication Failure
// Check credentials and security settings
AT+UWSCP=0       // Verify SSID
AT+UWSS=0        // Check security configuration
AT+UWSS?         // Verify security mode
```

**For Socket Issues:**
```bash
// Check socket-specific error
AT+USOE?
+USOE:16
OK

// Error 16 = Not Connected
// Re-establish connection
AT+UWSNST=0      // Check network status
AT+USOC=0,server,port              // Reconnect socket
```

## Common error resolution patterns

| Error Pattern | Quick Resolution | Prevention |
|---------------|------------------|------------ |
| **Parameter Errors (5, 35-39)** | Check parameter format and ranges | Validate inputs before sending commands |
| **Connection Errors (16, 62, 67)** | Verify network status and reconnect | Monitor connection status regularly |
| **Memory Errors (6, 107)** | Free resources, reduce concurrent operations | Implement resource management |
| **Authentication Errors (14, 95, 98)** | Verify credentials and certificates | Use secure credential storage |
| **Timeout Errors (9, 46)** | Increase timeouts, check network conditions | Monitor signal strength and latency |

## Error code integration with monitoring

## Automated error monitoring

**Enable Comprehensive Error Reporting:**
```bash
// Enable comprehensive error reporting for all commands
AT+USYEE=1

// Monitor connection events
AT+UWSNST=0      // Check connection status regularly

// Check errors periodically
AT+USYEC?        // Last general error
AT+USOE?         // Last socket error
```

## Error code integration examples

**Wi-Fi Connection with Error Handling:**
```bash
AT+UWSC
ERROR:62
AT+USYEC?
+USYEC:62
// Error 62 = Network not found, scan first
AT+UWSSC
AT+UWSC
OK
```

**Socket Operation with Error Handling:**
```bash
AT+USOC=0,"192.168.1.100",80
ERROR
AT+USOE?
+USOE:180
// Error 180 = Socket already bound, close first
AT+USOCL=0
AT+USOC=0,"192.168.1.100",80
OK
```

This comprehensive error code reference provides immediate debugging support without requiring external documentation, significantly enhancing the troubleshooting experience for NORA-W36 users.




# Software update

This use case shows what AT commands to send to start a software update.
There are two ways to start the software update:

- See more about the XMODEM protocol [here](https://en.wikipedia.org/wiki/XMODEM)

![firmware](https://content.u-blox.com/sites/default/files/2024-02/firmware.png)

## Update software by AT command

- Enter XMODEM mode for u-connect software update using serial port
- XMODEM-1K and baud rate up to 3 Mbps is supported.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 |  Start XMODEM protocol with AT command  | `AT+USYFWUS=3000000` | |
| 2 | Now NORA-W36 is ready to receive the software using the XMODEM or XMODEM-1K protocol | `CCCCCCCCCCC...`  | |
| 3 | When the software has been downloaded the module will restart |  `+STARTUP`   | |
| 4 | Check the version of the software | `AT+GMR`| `"4.0.0-041"` |

## Update software by bootloader

Consider the following points when updating the software using the bootloader:
- Enter the bootloader command line mode using serial port by AT command
- Press `SWITCH_1` and `SWITCH_2` during startup (or after reset)
- A command must be sent within 10 seconds when in bootloader command line mode. Otherwise, the device reboots in normal mode
- For the complete list of available commands, enter `?`
- An XMODEM protocol timeout is invoked after 10 seconds if nothing is received
- XMODEM-1K and baud rate up to 3 Mbps is supported

| Nr| Instructions                              | AT command                        | Event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1a |  Enter the bootloader  | `AT+USYBL=115200` | |
| 1b |  Alternatively, press `SWITCH_1` and `SWITCH_2` during startup or reset to enter the bootloader reset|  | |
| 2 |  Wait for the `>` prompt  | |`>`|
| 3 |  Change baud rate to up to 3 Mbit/s (optional)  | `r 3000000` | |
| 4 |  Start XMODEM protocol with the command `x`  | `x`  | |
| 5 | Now NORA-W36 is ready to receive the software using the XMODEM or XMODEM-1K protocol|  | `CCCCCCCCCCC...` |
| 6    | Wait for the prompt to indicate that the software has been downloaded successfully | |  `>` |
| 7    | Enter the `q` command to restart the module|  `q`  | |
| 8 | Wait for the prompt to display that the module has restarted in AT mode |  `+STARTUP`   | |
| 9 | Check the version of the software | `AT+GMR`| `"3.0.0-041"` |

## XMODEM protocol deep dive

XMODEM is a file transfer protocol used for reliable data transmission over serial connections. NORA-W36 supports both standard XMODEM (128-byte blocks) and XMODEM-1K (1024-byte blocks) for firmware updates.

### XMODEM protocol overview

XMODEM uses a simple acknowledgment-based protocol where the receiver controls the transfer by requesting blocks from the sender. Each block includes error detection to ensure data integrity.

**Key Features:**
- **Block-based transfer**: Data sent in fixed-size blocks
- **Error detection**: Checksum or CRC for data integrity
- **Flow control**: Receiver controls transfer pace
- **Retry mechanism**: Automatic retransmission on errors
- **Timeout handling**: Built-in timeouts prevent hanging

### Standard XMODEM (128-byte blocks)

**Block Structure:**
```
[SOH][Block#][~Block#][128 bytes data][Checksum]
  1     1        1         128            1     = 132 bytes total
```

**Control Characters:**
- `SOH` (0x01): Start of Header - begins each block
- `EOT` (0x04): End of Transmission - signals transfer complete
- `ACK` (0x06): Acknowledge - receiver accepts block
- `NAK` (0x15): Negative Acknowledge - receiver rejects block
- `CAN` (0x18): Cancel - abort transfer
- `C` (0x43): Request CRC mode instead of checksum

### XMODEM-1k (1024-byte blocks)

**Block Structure:**
```
[STX][Block#][~Block#][1024 bytes data][CRC-16]
  1     1        1          1024            2    = 1029 bytes total
```

**Key Differences from Standard XMODEM:**
- Uses `STX` (0x02) instead of `SOH`
- 1024-byte data blocks instead of 128 bytes
- Always uses CRC-16 instead of simple checksum
- 8x faster transfer rate for large files

### XMODEM transfer sequence

**1. Handshake Phase:**
```
Receiver → Sender: NAK or 'C' (requests transfer start)
Sender   → Receiver: First data block
```

**2. Data Transfer Phase:**
```
For each block:
  Sender   → Receiver: [Block data]
  Receiver → Sender:   ACK (good) or NAK (retry)
```

**3. Completion Phase:**
```
Sender   → Receiver: EOT (end of transmission)
Receiver → Sender:   ACK (confirms completion)
```

### Error handling and recovery

**Timeout Conditions:**
- **10 seconds**: Initial handshake timeout
- **10 seconds**: Block transmission timeout
- **Maximum 10 retries**: Before aborting transfer

**Error Recovery:**
- **Checksum/CRC mismatch**: Receiver sends NAK, sender retransmits
- **Block number error**: Receiver sends NAK for retransmission
- **Timeout**: Receiver sends NAK to request retransmission
- **Too many errors**: Either side sends CAN to abort

### Implementation examples

Complete working XMODEM implementations for NORA-W36 firmware updates are provided in the appendices:

- **[Appendix C.1: Python XMODEM Implementation](#c1-python-xmodem-implementation)** - Complete Python implementation with cross-platform support
- **[Appendix C.2: C XMODEM Implementation](#c2-c-xmodem-implementation)** - Native Windows C implementation with COM port handling

**Key Features of Both Implementations:**
- **Hardware Validated**: Tested with real NORA-W36 modules for firmware updates
- **XMODEM-1K Protocol**: 1024-byte blocks with CRC-16 error detection
- **Robust Error Handling**: Automatic retries, timeout management, and recovery
- **Progress Tracking**: Real-time feedback during file transfers
- **NORA-W36 Integration**: Automated AT command sequence for firmware mode
- **High-Speed Support**: Up to 3Mbps baud rate for fast transfers

**Usage Examples:**
```bash
# Python implementation
python xmodem.py COM3 NORA-W36X-SW-3.1.0-150.bin 115200

# C implementation  
xmodem.exe COM3 NORA-W36X-SW-3.1.0-150.bin 115200
```

Both implementations use identical command-line interfaces and have been proven to work reliably with NORA-W36 hardware.

### Performance comparison

**Standard XMODEM vs XMODEM-1K:**

| Parameter | XMODEM | XMODEM-1K |
|-----------|--------|-----------|
| Block Size | 128 bytes | 1024 bytes |
| Header Size | 3 bytes | 3 bytes |
| Error Check | 1 byte checksum | 2 bytes CRC-16 |
| Total Overhead | 4 bytes (3.1%) | 5 bytes (0.5%) |
| Blocks per MB | 8,192 | 1,024 |
| ACK/NAK per MB | 8,192 | 1,024 |
| **Efficiency** | **96.9%** | **99.5%** |

**Transfer Time Example (1MB firmware at 3Mbps):**
- **XMODEM**: ~3.5 seconds
- **XMODEM-1K**: ~2.8 seconds (20% faster)

### NORA-W36 specific implementation

**Firmware Update Process:**
1. **AT Command Mode**: Send `AT+USYFWUS=3000000` to enter XMODEM mode
2. **Protocol Detection**: NORA-W36 sends 'C' characters requesting CRC mode
3. **Auto-Detection**: Module automatically detects XMODEM vs XMODEM-1K from first block
4. **High-Speed Transfer**: Supports up to 3Mbps baud rate for fast updates
5. **Verification**: Module verifies firmware integrity before activation
6. **Restart**: Automatic restart with new firmware after successful update

**Bootloader Mode Features:**
- **Manual Entry**: Press SWITCH_1 + SWITCH_2 during startup
- **Command Interface**: Interactive commands (`x` for XMODEM, `r` for baud rate)
- **Recovery Mode**: Always available even if firmware is corrupted
- **Safety Features**: 10-second timeout prevents accidental activation

# Related Information

## Documentation & resources

- **[NORA-W36 Product Page](https://www.u-blox.com/en/product/NORA-W36-series)**
  Complete product information, specifications, and ordering details

- **[s-center 2 Webpage](https://www.u-blox.com/en/product/s-center)**
  Configuration and development tool for u-blox modules

- **[NORA-W36 AT Command Manual](https://www.u-blox.com/en/sho-online-documentation/NORA-W36/at-manual)**
  Comprehensive AT command reference and syntax guide

# Contacts

u-blox AG
Address: Zürcherstrasse 68
8800 Thalwil
Switzerland
For further support and contact information, visit us at **[u-blox Support](https://www.u-blox.com/support)**.

---

# Appendix

## Wi-Fi commands

### Station connection commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UWSCP` | Wi-Fi Station Connection Parameters (SSID) | [](#wi-fi-station-command-reference) |
| `AT+UWSSW` | Wi-Fi Station Security/Password (WPA2/WPA3) | [](#wi-fi-station-command-reference) |
| `AT+UWSSO` | Wi-Fi Station Security Open | [](#wi-fi-station-wpa2-and-wpa3) |
| `AT+UWSC` | Wi-Fi Station Connect | [](#wi-fi-station-command-reference) |
| `AT+UWSDC` | Wi-Fi Station Disconnect | [](#wi-fi-station-command-reference) |
| `AT+UWSNST` | Wi-Fi Station Network Status | [](#wi-fi-station-wpa2-and-wpa3) |
| `AT+UWSST` | Wi-Fi Station Signal Strength (RSSI) | [](#wi-fi-station-wpa2-and-wpa3) |

### Station enterprise security commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UWSSP` | Wi-Fi Station PEAP Security | [](#wi-fi-peap-enterprise-security) |
| `AT+UWSSE` | Wi-Fi Station Enterprise Security (EAP-TLS) | [](#wi-fi-eap-tls-enterprise-security) |

### Station IP configuration commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UWSIPS` | Wi-Fi Station IP Static Configuration | [](#wi-fi-station-wpa2-and-wpa3) |
| `AT+UWSIPD` | Wi-Fi Station IP DHCP | [](#wi-fi-station-wpa2-and-wpa3) |

### Access point commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UWAPCP` | Wi-Fi Access Point Connection Parameters | [](#wi-fi-access-point-wpa2) |
| `AT+UWAPSW` | Wi-Fi Access Point Security/Password | [](#wi-fi-access-point-wpa2) |
| `AT+UWAPA` | Wi-Fi Access Point Activate | [](#wi-fi-access-point-wpa2) |
| `AT+UWAPD` | Wi-Fi Access Point Deactivate | [](#wi-fi-access-point-wpa2) |
| `AT+UWAPNST` | Wi-Fi Access Point Network Status | [](#wi-fi-access-point-wpa2) |

### Roaming commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UWSROS0` | Wi-Fi Roaming RSSI Threshold Low | [](#http-and-https-use-cases) |
| `AT+UWSROS1` | Wi-Fi Roaming RSSI Threshold High | [](#http-and-https-use-cases) |
| `AT+UWSROS2` | Wi-Fi Roaming Scan Interval | [](#http-and-https-use-cases) |
| `AT+UWSROS3` | Wi-Fi Roaming Scan Duration | [](#http-and-https-use-cases) |
| `AT+UWSROS4` | Wi-Fi Roaming Channel Time | [](#http-and-https-use-cases) |
| `AT+UWSROS5` | Wi-Fi Roaming Home Channel Time | [](#http-and-https-use-cases) |

## Socket commands

### Socket management

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USOCR` | Create Socket (TCP/UDP) | [](#wi-fi-tcp-client) |
| `AT+USOC` | Socket Connect | [](#wi-fi-tcp-client) |
| `AT+USOL` | Socket Listen (Server) | [](#wi-fi-tcp-server-listener) |
| `AT+USOCL` | Socket Close | [](#wi-fi-tcp-client) |

### Socket data transfer

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USOWS` | Socket Write String | [](#string-mode) |
| `AT+USOWB` | Socket Write Binary | [](#binary-mode) |
| `AT+USORS` | Socket Read String | [](#string-mode) |
| `AT+USORB` | Socket Read Binary | [](#binary-mode) |

### TLS/SSL commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USOTLS` | Socket TLS Configuration | [](#wi-fi-tcp-using-tls-without-certificates) |
| `AT+USETE0` | TLS Extension - Server Name Indication | [](#tls-extensions-configuration) |
| `AT+USETE1` | TLS Extension - Handshake Fragmentation | [](#tls-extensions-configuration) |

## Certificate management commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USECUB` | Certificate Upload Binary | [](#create-own-certificates-using-openssl) |
| `AT+USECL` | Certificate List | [](#a23-certificate-management-commands) |
| `AT+USECD` | Certificate Details/Show | [](#a23-certificate-management-commands) |
| `AT+USECR` | Certificate Remove | [](#a23-certificate-management-commands) |

## MQTT commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UMQCP` | MQTT Client Parameters (Host/Port) | [](#mqtt-overview) |
| `AT+UMQC` | MQTT Client Connect | [](#mqtt-overview) |
| `AT+UMQDC` | MQTT Client Disconnect | [](#mqtt-overview) |
| `AT+UMQS` | MQTT Subscribe | [](#mqtt-overview) |
| `AT+UMQS` | MQTT Unsubscribe (with action=1) | [](#mqtt-overview) |
| `AT+UMQPS` | MQTT Publish String | [](#mqtt-overview) |
| `AT+UMQCP` | MQTT Connection Parameters (includes username/password) | [](#mqtt-tls-client---aws-iot-core) |
| `AT+UMQTLS` | MQTT TLS Configuration | [](#mqtt-tls-client---azure-iot-hub) |

## HTTP/HTTPS commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UHTCCP` | HTTP Client Connection Parameters | [](#simple-http-get-request) |
| `AT+UHTCTLS` | HTTP Client TLS Configuration | [](#https-get-with-certificate-validation) |
| `AT+UHTCRG` | HTTP Client Request GET | [](#simple-http-get-request) |
| `AT+UHTCRP` | HTTP Client Request POST | [](#http-post-with-json-data) |
| `AT+UHTCRPUS` | HTTP Client Request PUT String | [](#http-post-request-for-data-updates) |
| `AT+UHTCRD` | HTTP Client Request DELETE | [](#http-delete-request) |
| `AT+UHTCGBS` | HTTP Client Get Body String | [](#simple-http-get-request) |
| `AT+UHTCGBB` | HTTP Client Get Body Binary | [](#http-post-with-binary-file-upload) |
| `AT+UHTCRHAF` | HTTP Client Request Header Add Field | [](#http-post-with-json-data) |
| `AT+UHTCDC` | HTTP Client Disconnect | [](#simple-http-get-request) |

## Bluetooth commands

### BLE advertising commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UBTALS` | BLE Advertising Parameters | [](#bluetooth-advertise) |
| `AT+UBTAL` | BLE Advertising Start | [](#bluetooth-advertise) |
| `AT+UBTALD` | BLE Advertising Stop | [](#bluetooth-advertise) |

### BLE connection commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UBTC` | BLE Connect (Central) | [](#bluetooth-gatt-client) |
| `AT+UBTDC` | BLE Disconnect | [](#bluetooth-gatt-client) |
| `AT+UBTD` | BLE Discovery/Scan Start | [](#bluetooth-gatt-client) |
| `AT+UBTSS` | BLE Scan Settings | [](#bluetooth-gatt-client) |

### BLE SPS commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UBTP` | Bluetooth Pairing | [](#bluetooth-sps-central) |
| `AT+USPSWS` | SPS Write String | [](#string-mode) |
| `AT+USPSWB` | SPS Write Binary | [](#binary-mode) |
| `AT+USPSRS` | SPS Read String | [](#string-mode) |
| `AT+USPSRB` | SPS Read Binary | [](#binary-mode) |

### BLE GATT commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UBTGW` | GATT Characteristic Write | [](#bluetooth-gatt-client) |
| `AT+UBTGR` | GATT Characteristic Read | [](#bluetooth-gatt-client) |
| `AT+UBTGCCW` | GATT Client Configuration Write (for notifications) | [](#bluetooth-gatt-client) |

## System and diagnostic commands

### Power management

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UPMPSL` | Power Management Sleep Level | [](#auto-sleep) |
| `AT+UPMPSTO` | Power Management Sleep Timeout | [](#auto-sleep) |
| `AT+CPWROFF` | Module Reset/Power Off | Multiple sections |

### Network time protocol (NTP)

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UNTE` | NTP Enable/Disable and Status | [](#a72-network-time-protocol-ntp) |
| `AT+UNTSC` | NTP Server Configuration | [](#ntp-with-dhcp-fallback) |

###  Diagnostic commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UWSNST?` | Check Connection Status | [](#network-status-check) |
| `AT+UDGI` | Diagnostic Iperf Client | [](#iperf-client-mode) |

### Error handling

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USYEC` | System Extended Error Code | [](#query-last-error-code) |
| `AT+USYEE` | System Extended Errors Enable | [](#socket-error-codes-180) |
| `AT+USOE` | Socket Error | [](#socket-error-query) |

### Data mode commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UTM` | Transparent Mode | [](#basic-transparent-mode) |
| `AT+UTMP` | Transparent Mode Persistent | [](#persistent-transparent-mode) |
| `ATE0/ATE1` | Command Echo Control | [](#wi-fi-tcp-client) |
| `AT&W` | Store Configuration (use with AT+CPWROFF) | Multiple sections |
| `+++` | Escape Sequence (Exit Transparent Mode) | [](#basic-transparent-mode) |

## Quick command lookup by use case

### Quick getting started

```
AT+UWSCP=0,"YourSSID"              // Set network name
AT+UWSSW=0,"YourPass",0            // Set password
AT+UWSC=0        // Connect
```

### Quick MQTT setup

```
AT+UMQCP=0,"broker.hivemq.com",1883          // Set broker
AT+UMQC=0        // Connect
AT+UMQS=0,"test/topic"             // Subscribe
```

### Quick HTTP request

```
AT+UHTCCP=0,"httpbin.org",80       // Set server
AT+UHTCRG=0,"/"          // GET request
AT+UHTCGBS=0,500         // Read response
```

### Debug commands chain

```
AT+USYEE=1       // Enable extended errors
AT+UWSST=4       // Check signal strength
AT+UWSSC         // List available networks
AT+USYEC?        // Check last error
```

// Appendix B: Enhanced Debugging and Visual Reference Guide

This appendix provides visual troubleshooting aids, standardized code examples, and enhanced debugging techniques for optimal NORA-W36 implementation and troubleshooting.

## Visual status indicators and LED patterns

### NORA-W36 LED status indicators

**Official LED Patterns (from NORA-W36 Datasheet):**

| LED Combination | Color | State | Description |
|-----------------|-------|-------|-------------|
| LED_BLUE = Low (0) | 🔵 Blue | Connected | Wi-Fi or Bluetooth connection established |
| LED_RED + LED_BLUE = Low (0) | 🟣 Magenta | Connecting | Attempting Wi-Fi or Bluetooth connection |
| LED_RED + LED_GREEN = Low (0) | 🟡 Yellow | Not Connected | No active connections |
| LED_RED = Low (0) | 🔴 Red | Not used | Reserved for future versions |
| LED_GREEN = Low (0) | 🟢 Green | Not used | Reserved for future versions |

**Quick Status Reference:**
- **🔵 Blue**: Connection successful - ready for data transfer
- **🟣 Magenta**: Connection in progress - wait for completion
- **🟡 Yellow**: No connection - initiate connection sequence

**Note**: LED behavior may change in future firmware versions. Refer to latest datasheet for updates.

### Connection status workflow

**Visual Connection Flow:**
```
🟡 Yellow (Disconnected)
        ↓
   AT+UWSC=0 (Start connection)
        ↓
🟣 Magenta (Connecting)
        ↓
🔵 Blue (Connected)
```

**Troubleshooting with LEDs:**
- **Stuck in Magenta**: Check signal strength, credentials, or network availability
- **Returns to Yellow**: Connection failed - check error codes with `AT+USYEC?`
- **Blue achieved**: Connection successful - proceed with data operations

## Standardized code example format

### Command documentation standard

**Standardized AT Command Format Template:**

```markdown
### Command name

**Purpose:** Brief description of what the command does

**Syntax:**
```

```bash
AT+UWSCP=<interface_id>,<ssid>
```

**Parameters:**
- `interface_id`: Wi-Fi interface (0 = station)
- `ssid`: Network SSID name (quoted string)

**Response:**
```bash
OK
```

**Examples:**
```bash
// Basic usage
AT+UWSCP=0,"MyNetwork"
OK

// Error case
AT+UWSCP=0,invalid_ssid
ERROR:5          // U_ERROR_COMMON_INVALID_PARAMETER
```

**Notes:** SSID must be provided as quoted string for proper parsing

### Standardized connection examples

**Wi-Fi Connection Template:**
```bash
// Step 1: Configure network
AT+UWSCP="NetworkName",<channel>
OK

// Step 2: Set security (WPA2/WPA3)
AT+UWSSW=0,"password",<wpa_mode>
OK

// Step 3: Connect
AT+UWSC
+UEWLU:0,123456789ABC,6            // Wi-Fi Link Up
OK

// Step 4: Verify Netork connection
+UEWSNU
AT+UWSNST=0
+UWSNST:0,"192.168.1.100"
OK
```

**Socket Connection Template:**
```bash
// Step 1: Create socket
AT+USOCR=<protocol>      // 6=TCP, 17=UDP
+USOCR:<socket_id>
OK

// Step 2: Connect to server
AT+USOC=<socket_id>,<server_ip>,<port>
+UESOC:<socket_id>
OK

// Step 3: Send/receive data
AT+USOWS=<socket_id>,"<data_payload>"
+USOWS:<socket_id>,<bytes_sent>
OK

// Step 4: Close socket
AT+USOCL=<socket_id>
OK
```

## Enhanced debugging workflows

### Progressive debugging approach

**Level 1: Basic Status Check**
```bash
// Quick health check (30 seconds)
AT               // Module responsiveness
AT+UWSNST=0      // Network status
AT+USYEC?        // Last error code
```

**Level 2: Connection Diagnostics**
```bash
// Connection analysis (2 minutes)
AT+UWSSC         // Network scan
AT+UWSST=4       // Signal strength
AT+UWSCP=0       // Current configuration
AT+UWSS=0        // Security settings
AT+UWSNST?       // Check connection status
```

**Level 3: Advanced Troubleshooting**
```bash
// Deep diagnostics (5 minutes)
AT+USYEE=1       // Enable extended errors
AT+UWSSC         // Detailed network scan
AT+USECL?        // Certificate validation
AT+UWSST=4       // Signal strength check
AT+USYEC?        // Check for system errors
```

### Visual troubleshooting decision tree

```
                    ⚠  AT Command Fails?
                           │
                    ┌──────▼──────
                    │ AT+USYEC?   │
                    │ Check Error │
                    └──────┬──────┘
                           │
              ┌────────────▼────────────
              │     Error Code Range?   │
              └─┬─────────┬─────────┬───┘
                │         │         │
           ┌────▼───  ┌───▼───  ┌───▼────
           │ 1-22   │ │ 31-51 │ │ 60-71  │
           │Common  │ │AT Synt│ │ Wi-Fi  │
           │Errors  │ │ax Err │ │Errors  │
           └────┬───┘ └───┬───┘ └───┬────┘
                │         │         │
                ▼         ▼         ▼
         ┌─────────────  ┌─────────────  ┌─────────────
         │🔧 Check     │ │ Check      │  │  📶 Check  │
         │System       │ │Command      │ │Wi-Fi        │
         │Resources    │ │Format &     │ │Connection   │
         │& Hardware   │ │Parameters   │ │& Settings   │
         └─────────────┘ └─────────────┘ └─────────────┘
                │         │         │
                ▼         ▼         ▼
         ┌─────────────  ┌─────────────  ┌─────────────
         │• Power      │ │• Syntax     │ │• Network    │
         │• Memory     │ │• Arguments  │ │• Auth       │
         │• Sensors    │ │• Quotes     │ │• Signal     │
         └─────────────┘ └─────────────┘ └─────────────┘
       │   │
       ▼   ▼
   ┌──────────────
   │AT+UWSSC      │
   │Check Networks│
   └──────────────┘
```

## Performance monitoring visual dashboard

### Automated health check script template

**Health Check Sequence (Copy-paste ready):**
```bash

=== NORA-W36 Health Check ===

echo "Starting health check..."

// Basic responsiveness
AT

// Network status
AT+UWSNST=0
echo "Network Status: Check response above"

// Signal quality
AT+UWSST=4
echo "Signal Strength: Check RSSI value above"

// Error status
AT+USYEC?
echo "Last Error: 0 = No errors"

// Certificate status
AT+USECL?
echo "Certificates: Check expiration dates"

echo "Health check complete!"
```

## Quick reference cards

### Emergency recovery commands

**🆘 Module Not Responding:**
```bash
// Hardware reset sequence
1. Power cycle module (3.3V off → on)
2. Wait 5 seconds
3. AT            // Test basic response
4. AT+USYFR      // Factory reset
5. AT+CPWROFF    // Restart with factory default settings
```

**🆘 Connection Issues:**
```bash
// Connection recovery sequence
AT+UWSDC         // Disconnect from network
AT+USYEE=1       // Enable error reporting
AT+UWSSC         // Scan available networks
AT+UWSC          // Reconnect
AT+UWSNST=0      // Verify connection
```

### Power user quick commands

**⚡ Speed Test Commands:**
```bash
// Connection speed test
AT+UWSNST?       // Check connection
AT+UWSSC         // List networks for signal strength
AT+UWSST=4       // Signal strength verification
```

**⚡ Bulk Configuration:**
```bash
// Fast setup sequence for development
AT+USYEE=1       // Extended errors
AT+UWSNST=0      // Connection status check
AT+UPMPSL=0      // Disable power save
```

**⚡ Security Validation:**
```bash
// Security health check
AT+UWSCP=0       // Network config
AT+UWSS=0        // Security configuration
AT+USECL?        // Certificate validity
AT+UWSST=4       // Signal strength (security)
```

This enhanced visual reference guide provides immediate troubleshooting support with visual indicators, standardized examples, and copy-paste ready command sequences for efficient NORA-W36 development and deployment.

## C.1 Python XMODEM implementation

This Python XMODEM sender implementation has been tested with real NORA-W36 hardware for firmware updates.

The complete implementation is provided in the accompanying `xmodem/xmodem.py` file.

**Key Features:**
- **Cross-platform**: Works on Windows, Linux, and macOS with pyserial
- **XMODEM-1K Protocol**: 1024-byte blocks with CRC-16 error detection
- **Robust Error Handling**: Automatic retries, timeout management, and recovery
- **Progress Tracking**: Real-time feedback during file transfers
- **NORA-W36 Integration**: Automated AT command sequence for firmware mode

**Requirements:**
```bash
pip install pyserial
```

**Usage:**
```bash
python xmodem.py <port> <firmware_file> [baud_rate]

# Examples:
python xmodem.py COM3 NORA-W36X-SW-3.1.0-150.bin
python xmodem.py COM3 NORA-W36X-SW-3.1.0-150.bin 115200
python xmodem.py /dev/ttyUSB0 NORA-W36X-SW-3.1.0-150.bin  # Linux
```

**Integration Example:**
```python
from xmodem import ublox_firmware_update

# Update firmware with default baud rate
success = ublox_firmware_update("COM3", "NORA-W36X-SW-3.1.0-150.bin")

# Update firmware with custom baud rate
success = ublox_firmware_update("COM3", "NORA-W36X-SW-3.1.0-150.bin", 3000000)
```

See the `xmodem/README_xmodem_python.md` file for detailed documentation.

## C.2 C XMODEM implementation

This simplified C XMODEM sender provides the same functionality as the Python version with Windows-native serial port handling.

The complete implementation is provided in the accompanying `xmodem/xmodem.c` file.

**Key Features:**
- **Native Windows API**: Direct serial port handling using kernel32
- **XMODEM-1K Protocol**: 1024-byte blocks with CRC-16 error detection
- **COM10+ Support**: Automatic handling of high-numbered COM ports
- **Robust Error Handling**: Automatic retries and timeout management
- **NORA-W36 Integration**: Automated AT command sequence for firmware mode

**Compilation:**
```bash
# GCC/MinGW
gcc -o xmodem xmodem.c -lkernel32

# Visual Studio
cl /Fe:xmodem.exe xmodem.c kernel32.lib
```

**Usage:**
```bash
xmodem.exe <port> <firmware_file> [baud_rate]

# Examples:
xmodem.exe COM3 NORA-W36X-SW-3.1.0-150.bin
xmodem.exe COM3 NORA-W36X-SW-3.1.0-150.bin 115200
xmodem.exe COM15 NORA-W36X-SW-3.1.0-150.bin 3000000  # High COM port
```

See the `xmodem/README_xmodem_c.md` file for detailed documentation.
