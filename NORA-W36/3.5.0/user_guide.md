# **NORA-W36 u-connectXpress**

## Stand-alone multiradio modules

## <span style="color: gray;">User guide</span>

![short range](https://content.u-blox.com/sites/default/files/2024-02/shortrange.png)

This document provides an overview of the u-connectXpress software for u-blox short range modules
and describes how the products can be configured for Wi-Fi and Bluetooth Low Energy use cases.

![NORA-W36](https://content.u-blox.com/sites/default/files/2026-01/NORA-W36.png)

## Document information

| Title | NORA-W36 series u-connectXpress |
| :------------ | ---------------- |
| Subtitle    |  Stand-alone multiradio modules             |
| Document type | User guide |
| Version and date | 3.5.0 19-Oct-2026 |
| Disclosure restriction    |C1-Public |

**This document applies to the following products**
| Product name    |  Software version |
| :------------ | ---------------- |
| NORA-W36 series    |  3.5.0|

**Disclaimer**
u-blox or third parties may hold intellectual property rights in the products, names, logos, and designs included in this document. Copying, reproduction, or modification of this document or any part thereof is only permitted with the express written permission of u-blox. Disclosure to third parties is permitted for clearly public documents only.
The information contained herein is provided "as is" and u-blox assumes no liability for its use. No warranty, either express or implied, is given, including but not limited to, with respect to the accuracy, correctness, reliability, and fitness for a particular purpose of the information. This document may be revised by u-blox at any time without notice. For the most recent documents, visit [www.u-blox.com](https://www.u-blox.com).
Copyright © u-blox AG

# Overview

This document describes how to set up and use u-blox short range stand-alone modules with u-connectXpress software for NORA-W36. It includes AT command examples for the supported use cases. The document is applicable for Bluetooth® Low Energy (LE), multiradio and Wi-Fi modules.
Several u-blox short range stand-alone modules support open software variants; see the system integration manuals for the available options.
For older generation modules like ODIN-W2, NINA-W15 and ANNA-B1, the [u-connectXpress user guide](https://www.u-blox.com/docs/UBX-16024251) describes the functionality of these modules.

## What's new in 3.5.0

For the complete list of fixes and known limitations see the
[CHANGELOG-NORA-W36.md](https://github.com/u-blox/u-connectXpress/blob/main/NORA-W36/CHANGELOG-NORA-W36.md).

- **HTTP downloads** — `AT+UHTCGBB` reads up to 2048 bytes per call, which greatly improves HTTP download throughput. `AT+UHTCTLS` alone now decides whether TLS is used for an HTTP session. See [HTTP and HTTPS use cases](#http-and-https-use-cases).
- **Light sleep** — `AT+UPMS` keeps Wi-Fi connections and supports baud rates above 115200. Wake up with the `WAKE_UP` pin or the UART. Bluetooth must be disabled (`AT+UBTM=0`). See [Light sleep](#light-sleep).
- **Host Wakeup pin** — `AT+USYHWP` configures the Host Wakeup pin to indicate the transparent mode connection status. See [Transparent mode](#transparent-mode-overview).
- **mDNS name conflicts** — A conflicting hostname or service name is renamed automatically and reported with `+UEMDCD:<conflict_type>,<previous_name>,<new_name>`. See [mDNS use cases](#mdns-use-cases).
- **Binary socket data events** — The erroneous comma before the binary header in `+UESODB` and `+UESODBF` is removed.
- **Stability fixes** — Socket close deadlock under heavy load, hang on a failed non-blocking connect, stall of a TLS transparent read, retry instead of data loss when UDP buffers run out, URCs cut in half at high socket throughput (for example `+UESODS`), UDP port 5353 bound at startup when unused, NTP mode behavior and system time preserved across reboot.
- **HTTP fixes** — Large response headers (for example a large Content-Security-Policy) ran on into the body, a custom request header was not null-terminated, and a remote socket close could make the next request in a completed session fail.
- **SPS and Bluetooth fixes** — An SPS client with flow control waits for the server credit notification, an assert on disconnect while the credit timer runs and a credit calculation overflow are fixed, an early MTU exchange no longer leaves SPS at MTU 23, and a race while ATT is torn down is fixed.
- **UART** — Rare data corruption at baud rates up to 115200 is fixed.

## Product description

u-blox modules are developed for integration into a vast range of devices that demand a high level of reliability, such as those that are typically used in industrial and medical applications.
These professional grade modules operate over an extended temperature range and are approved for radio type application products in many countries.

| Concept             | Definition |
| ------------------ | :------------ |
|**Host**                |In this document, a host refers to the device connected to a u-blox short range stand-alone module through any of the available physical interfaces. In a real application, the host is typically a microcontroller Unit (MCU) running a customer specific application. |
|**Module**               | In this document, module refers to a u-blox stand-alone module running the u-connectXpress software. |
|**Remote device**    | A remote device in a wireless network connecting over the Bluetooth Low Energy or Wi-Fi interfaces supported in the module.|

NORA-W36 modules include an embedded Bluetooth stack, Wi-Fi driver, IP stack and an application for wireless data transfer. The wireless support includes Bluetooth Low Energy 5.3 Wi-Fi 4 dual band 2,4 and 5 GHz.
The modules can run Bluetooth and Wi-Fi connections concurrently and, for example, act as a micro Access Point.
u-connectXpress provides the u-blox Bluetooth LE Serial Port Service (SPS), Generic Attribute Profile (GATT) client and server and Bluetooth beacons, with simultaneous Peripheral and Central roles. All features are configured from a host with AT commands.

# Quick start guide

## Initial setup checklist

### Hardware setup

- **Power and ground** — connect power as described in the NORA-W36 system integration manual.
- **UART** — connect TX/RX/GND between NORA-W36 and the host. Add CTS/RTS for hardware flow control at higher baud rates.
- **Reset and bootloader switches** (recommended) — wire the reset pin and `SWITCH_1`/`SWITCH_2` for hardware reset and bootloader access, see [Update software by bootloader](#update-software-by-bootloader).

### Software setup

Install [s-center 2](https://www.u-blox.com/en/product/s-center) or any serial terminal and open the module's COM port. The UART defaults are 115200 bps, 8 data bits, no parity, 1 stop bit (8N1), and hardware flow control **disabled**.

### Initial verification commands

| Step | Command | Expected Response |
|------|---------|------------------|
| 1 | `AT` | `OK` |
| 2 | `ATI` | Module information |
| 3 | `AT+GMI` | `u-blox` |
| 4 | `AT+GMM` | `NORA-W36` |
| 5 | `AT+GMR` | Software version |

## First connection examples

### Quick Wi-Fi connection

> **⚠ Migration note (since 3.4.0):** Security parameters must be configured **before** calling `AT+UWSC`. The default authentication is now WPA2 (was OPEN), and the default SSID has been removed. Scripts that called `AT+UWSC` without a prior `AT+UWSSW` against an open network now fail — set the password first, or explicitly select OPEN mode with `AT+UWSSW=0,"",1`.

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UWSCP=0,"YourSSID"` | Set network name |
| 2 | `AT+UWSSW=0,"YourPassword",0` | Set password (WPA2/WPA3 compatible) |
| 3 | `AT+UWSC=0` | Connect to network |
| 4 | Wait for `+UEWLU:0,BBBBBBBBBBB,6` | Wi-Fi link up |
| 5 | Wait for `+UEWSNU` | Network interface up |
| 6 | `AT+UWSNST?` | Read the network configuration |

```text
AT+UWSNST?
+UWSNST:0,192.168.1.59                        // IPv4 address
+UWSNST:1,255.255.255.0                       // Subnet mask
+UWSNST:2,192.168.1.1                         // Gateway
+UWSNST:3,192.168.1.1                         // Primary DNS
+UWSNST:4,0.0.0.0                             // Secondary DNS
+UWSNST:5,[fe80::56f8:2aff:fe10:aad4]         // IPv6 address
OK
```

### Quick Bluetooth advertising

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UBTALS=160,160` | Set legacy advertising interval (160 × 0.625 ms = 100 ms) |
| 2 | `AT+UBTAL` | Start legacy advertising |

The module is now discoverable as "NORA-W36" in a Bluetooth scanner.

# u-connectXpress software

## Operating modes

NORA-W36 operates in the following modes:

- **AT mode (default)**: AT commands and data can be sent at the same time. Data is sent and received in AT commands and events, in string or binary mode.
- **Transparent Mode (TM)**: All data sent and received on the UART is connected to the remote device.
- **Transparent Mode Persistent (TMP)**: Same as TM, but the connection is established at startup or when the connection is dropped.

The low power modes are independent of the operating mode, see [Power save use cases](#power-save-use-cases).

## Changing operating modes

The module starts in AT (command) mode. Switch to transparent mode with an AT command (`AT+UTM`) and back to command mode with the escape sequence `+++`, see [Transparent mode](#transparent-mode-overview).

## NORA-W36 capabilities

|u-connectXpress Features |Capability in 3.5.0 |
|:-----------------|:------------------|
|Chipset | Realtek RTL8720DF |
|Multiradio | Bluetooth Low Energy 5.3 Wi-Fi 4 dual band 2,4 and 5 GHz |
|Wi-Fi capabilities | 802.11a/b/g/n WPA2 Personal (Station & AP) and WPA3 Personal (Station only) Wi-Fi Multimedia WMM/WME/QoS (802.11e) Protected Management Frames (802.11w) RSSI-based client roaming. Fast BSS Transition (802.11r), Radio Measurement (802.11k) and Wireless Network Management (802.11v) are planned |
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
|SPS MTU size | 244 bytes link MTU; up to 1000 bytes per AT string call (`AT+USPSWS`), 1000 bytes per AT binary call (`AT+USPSWB`) |
|TCP MTU size | 1460 bytes link MTU; up to 1000 bytes per AT string call (`AT+USOWS`), 1460 bytes per AT binary call (`AT+USOWB`) |
|UDP MTU size | 1460 bytes link MTU; up to 1000 bytes per AT string call, 1460 bytes per AT binary call |
|HTTP body size | Rides on TCP (1460 bytes link MTU); up to 1000 bytes per AT string call (`AT+UHTCRPOS`, `AT+UHTCGBS`), 2048 bytes per AT binary read (`AT+UHTCGBB`). Binary POST/PUT (`AT+UHTCRPOB`, `AT+UHTCRPUB`) is streamed in successive calls up to the configured Content-Length |
|MQTT message size | Rides on TCP (1460 bytes link MTU); up to 1000 bytes per AT string call (`AT+UMQPS`), 5000 bytes per AT binary call (`AT+UMQPB`, `AT+UMQRB`) |

The table below summarises the major third-party components built into the firmware. The authoritative Software Bill of Materials is the CycloneDX `NORA-W36X-SBOM.json` shipped alongside the binary in each release archive.

|u-connectXpress software components |Versions in 3.5.0|
|:-----------------|:------------------|
|FreeRTOS kernel | 10.2.0 — [github.com/FreeRTOS/FreeRTOS-Kernel](https://github.com/FreeRTOS/FreeRTOS-Kernel) |
|lwIP TCP/IP stack | 2.2.0 — [github.com/lwip-tcpip/lwip](https://github.com/lwip-tcpip/lwip) |
|Mbed TLS | 3.6.4 — [github.com/Mbed-TLS/mbedtls](https://github.com/Mbed-TLS/mbedtls) |
|coreMQTT client | 2.1.0 — [github.com/FreeRTOS/coreMQTT](https://github.com/FreeRTOS/coreMQTT) |

|u-connectXpress MQTT client |Versions in 3.5.0|
|:----------------|:------------------|
|MQTT version | 3.1.1 |
|MQTT capabilities | Publish, Subscribe, TLS, QoS, Testament and Last will |
|MQTT maximum packets size | 5k (5000) bytes for Publish and Subscribe packets |

|u-connectXpress Enterprise security | Capability in 3.5.0|
|:-----------------|:------------------|
|PEAP Authentication method | PEAPv0 with EAP-MSCHAPv2 |
|EAP Authentication method | EAP Transport Layer Security (EAP-TLS) |
|EAP-TLS certificate key size supported | 2048 and 4096 bits |

|u-connectXpress TLS feature | TLS capability in 3.5.0|
|:-----------------|:------------------|
|TLS version | TLS 1.2 and TLS 1.3 |
|TLS max number of connections | 1 |
|TLS extensions enabled by default| Server Name Indication (SNI), Maximum Fragment Length Negotiation |
|TLS Encryption keys | Advanced Encryption Standard (AES).  Data Encryption Standard (DES), Rivest Cipher 4 (RC4), and the Camellia cipher are not supported. |
|X.509 security certificate formats supported | PEM (DER not supported) |
|TLS over TCP certificate key size supported | 4096 bits |
|TLS certificates | Up to 8 certifications (or certificate chains) can be stored. Certificates can be maximum 15360 bytes. |
|TLS Extensions | Server name (SNI) Max fragment length: 4096 (4) |

For the AT command syntax see the [NORA-W36 AT command manual](https://github.com/u-blox/u-connectXpress/blob/main/NORA-W36/3.5.0/at_commands.md).

# AT command interface

## Responses and error codes

Every AT command ends with `OK` or `ERROR`. Enable extended error reporting with `AT+USYEE=1` to receive `ERROR:<code>`, or read the code of the last failed command with `AT+USYEC?`, see [Error codes](#error-codes).

Commands that end in `B` (for example `AT+USPSWB`) are binary commands and use the framing described in [Binary data](#binary-data).

## Unsolicited result codes (URCs)

URCs are sent by the module without a preceding command and can arrive at any time, also between a command and its response. The host parser must handle them in the same stream as command responses.

| Area | URCs |
|------|------|
| System | `+STARTUP` |
| Bluetooth | `+UEBTC` (connected), `+UEBTDC` (disconnected), `+UEBTB` (bond), `+UEBTUC` (user confirmation) |
| SPS | `+UESPSC`, `+UESPSDC`, `+UESPSDA` (data available), `+UESPSDS` (string data), `+UESPSDB` (binary data) |
| Wi-Fi | `+UEWLU`, `+UEWLD` (link up/down), `+UEWSNU`, `+UEWSND` (station network up/down), `+UEWAPU`, `+UEWAPNU` (access point) |
| Sockets | `+UESOC`, `+UESOCL`, `+UESODA`, `+UESODS`, `+UESODB` |
| MQTT | `+UEMQC`, `+UEMQDC`, `+UEMQDA` |
| HTTP | `+UEHTCRS` |

# Bluetooth use cases

The default Bluetooth configuration of NORA-W36 (3.5.0):

|u-connectXpress BLE default values | 3.5.0 |
|:----------------|:-----------------|
|BLE Mode default |**ON**, Central and Peripheral (Mode = 3) |
|BLE Legacy Advertising default    |**OFF**, enable with `AT+UBTAL` |

The examples use these placeholder addresses; replace them with the real Bluetooth addresses of your devices.

- Peripheral address: AAAAAAAAAAAA
- Central address: BBBBBBBBBBBB

## Selecting the Bluetooth role

The use cases below assume that the required role is enabled. Check it first and change it if needed.

| Nr| Instructions | AT command | AT event |
|---|--------------|------------|----------|
| 1 | Read the Bluetooth mode | `AT+UBTM?` | `+UBTM:<mode>` |
| 2 | If needed, set the mode: `1` Central, `2` Peripheral or `3` Central and Peripheral | `AT+UBTM=<mode>` | `OK` |
| 3 | Store the setting | `AT&W` | `OK` |
| 4 | Restart | `AT+CPWROFF` | `+STARTUP` |

## Bluetooth GATT use cases

### Bluetooth GATT client

![bt-gatt-client](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-client.png)

NORA-W36 operates as a Central and GATT client that receives data from a remote GATT server, see [Bluetooth GATT server](#bluetooth-gatt-server). The Central role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                              | AT command                        | AT event              |
|:---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Connect to the remote device    |          `AT+UBTC=AAAAAAAAAAAAp` | `+UEBTC:0,AAAAAAAAAAAAp` |
| 2 | Discover the services and look for **180D** (Heart Rate service) | `AT+UBTGPSD=0` | `+UBTGPSD:0,12,65535,180D` |
| 3 | Discover the characteristics and look for **2A37** (Heart Rate Measurement) | `AT+UBTGSCD=0,12,65535`                  | `+UBTGSCD:0,13,10,14,2A37` |
| 4 | Use the value handle (here 14, it can vary) to find **2902**, the notification descriptor | `AT+UBTGCDD=0,14,15`            | `+UBTGCDD:0,13,15,2902` |
| 5 | Enable notifications on the descriptor handle | `AT+UBTGCCW=0,15,1` | `OK` |
| 6 | Notifications are received |                              | `+UEBTGCN:0,14,60` `+UEBTGCN:0,14,61` `+UEBTGCN:0,14,62` |

### Bluetooth GATT server

![bt-gatt-server](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-server.png)

NORA-W36 operates as a Peripheral and GATT server that sends notifications. It works with [Bluetooth GATT client](#bluetooth-gatt-client). The Peripheral role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                              | AT command                        | AT event              |
|---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Enable legacy advertising    | `AT+UBTAL` | `OK` |
| 2 | Write the Heart Rate service | `AT+UBTGS=180D` | `+UBTGS:21` |
| 3 | Write the GATT characteristic | `AT+UBTGC=2A37,3A,01,01,00`  | `+UBTGC:30,31` |
| 4 | Activate the GATT service           | `AT+UBTGSA`  | `OK` |
| 5 | Wait for an incoming connection                |  | `+UEBTC:0,BBBBBBBBBBBBp` |
| 6 | Read the MTU of the connection (optional) | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 7 | Read the role of the connection (optional)| `AT+UBTCST=0,7` | `+UBTCST:7,1` |
| 8 | Send notifications using the value handle | `AT+UBTGNS=0,14,60` `AT+UBTGNS=0,14,61` `AT+UBTGNS=0,14,62` | `OK` |

## Bluetooth SPS use cases

The u-blox [Serial Port Service (SPS)](https://content.u-blox.com/sites/default/files/u-connectXpress-LowEnergySerialPortService_ProtocolSpec_UBX-16011192.pdf) replaces a serial cable with a Bluetooth LE link between two devices. Once the SPS link is up, exchange data with `AT+USPSWS` / `AT+USPSWB` (write) and `AT+USPSRS` / `AT+USPSRB` (read), see [string vs binary modes](#string-mode).

### Bluetooth SPS central

![bt-sps-central](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-central.png)

NORA-W36 operates as a Central that connects to an SPS peripheral, for example another NORA-W36. It works with [Bluetooth SPS peripheral](#bluetooth-sps-peripheral). The Central role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                          | AT command  | AT event|
|:---|:---------------------------------------|:---------------------|:---|
| 1 | Discover advertising peripherals | `AT+UBTD` |`+UBTD:AAAAAAAAAAAAp,-52,"NORA-W36-AAAAAA",0,10094E4F52412D5733362D414141414141` |
| 2 | Connect Bluetooth | `AT+UBTC=AAAAAAAAAAAAp` | `+UEBTC:0,AAAAAAAAAAAAp` |
| 3 | Read the MTU | `AT+UBTCST=0,3` |  `+UBTCST:3,247` |
| 4 | Read the RSSI (optional)   | `AT+UBTRSS=0`     |  `+UBTRSS:-52` |
| 5 | Connect SPS using the Bluetooth connection handle       | `AT+USPSC=0`  | `OK` |
| 6 | SPS connection is up  |  | `+UESPSC:0` |
| 7 | Disconnect SPS and Bluetooth |`AT+UBTDC=0` |`+UESPSDC:0` `+UEBTDC:0` |

### Bluetooth SPS peripheral

![bt-sps-peripheral](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-peripheral.png)

NORA-W36 operates as a Peripheral that accepts an SPS connection. It works with [Bluetooth SPS central](#bluetooth-sps-central). The Peripheral role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                          | AT command  |  AT events |
|---|:---------------------------------------|:--------------------------------------|:--------------------|
| 1 | Enable SPS              | `AT+USPS=1`        | `OK` |
| 2 | Enable legacy advertising    | `AT+UBTAL` | `OK` |
| 3 | Wait for an incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 4 | Read the MTU | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 5 | Read the RSSI (optional)   | `AT+UBTRSS=0`     | `+UBTRSS:-52` |
| 6 | The Central connects SPS (`AT+USPSC=0` on the Central) |   | `+UESPSC:0` |
| 7 | SPS and Bluetooth link are down | | `+UESPSDC:0` `+UEBTDC:0` |

### SPS host tools and protocol documentation

The [u-blox/sps](https://github.com/u-blox/sps) repository documents the SPS GATT protocol and provides a Python reference implementation for hosts that talk SPS directly over Bluetooth LE, for example a PC or Raspberry Pi connecting to NORA-W36.

| Resource | Content |
|----------|---------|
| [SPS_PROTOCOL.md](https://github.com/u-blox/sps/blob/main/SPS_PROTOCOL.md) | Service and characteristic UUIDs, credit-based flow control, connection procedure |
| [SPS_UBLOX_CONFIG.md](https://github.com/u-blox/sps/blob/main/SPS_UBLOX_CONFIG.md) | Configuring u-blox modules for SPS with AT commands |
| [SPS_CLIENT_PYTHON.md](https://github.com/u-blox/sps/blob/main/SPS_CLIENT_PYTHON.md), [SPS_SERVER_PYTHON.md](https://github.com/u-blox/sps/blob/main/SPS_SERVER_PYTHON.md) | Python client ([bleak](https://pypi.org/project/bleak/)) and server ([bless](https://pypi.org/project/bless/)) |
| [SPS_CLIENT_C.md](https://github.com/u-blox/sps/blob/main/SPS_CLIENT_C.md), [SPS_SERVER_C.md](https://github.com/u-blox/sps/blob/main/SPS_SERVER_C.md) | C implementation outline for any BLE stack |
| [sps.py](https://github.com/u-blox/sps/blob/main/sps.py) | Command line tool and library |

```bash
pip install bleak bless
python sps.py scan --sps-only                  # find SPS devices
python sps.py client -a AA:BB:CC:DD:EE:FF      # connect as SPS client (central)
python sps.py server -n "My-Device"            # run as SPS server (peripheral)
```

## Bluetooth advertise

NORA-W36 operates as a Peripheral and GATT client towards an Apple iPhone using the Apple Notification Center Service (ANCS). The Peripheral role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                              | AT command                        | AT event              |
|---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Set the Apple ANCS advertise data packet  | `AT+UBTADL=1115D0002D121E4B0FA4994ECEB531F40579`     | `OK` |
| 2 | Enable legacy advertising    | `AT+UBTAL` | `OK` |
| 3 | Wait for an incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 4 | Discover the services and look for **180A** (Device Information) | `AT+UBTGPSD=0` | `+UBTGPSD:0,1,5,1800` `+UBTGPSD:0,6,9,1801` `+UBTGPSD:0,10,14,180A` `+UBTGPSD:0,15,19,D0611E78BBB44591A5F8487910AE4366` `+UBTGPSD:0,20,24,9FA480E0496745429390D343DC5D04AE` `+UBTGPSD:0,25,28,180F` `+UBTGPSD:0,29,34,1805` `+UBTGPSD:0,35,44,7905F431B5CE4E99A40F4B1E122D00D0` `+UBTGPSD:0,45,56,89D3502B0F36433A8EF4C502AD55F8DC` |
| 5 | Discover the characteristics and look for **2A29** (Manufacturer Name String) | `AT+UBTGSCD=0,10,14` | `+UBTGSCD:0,11,02,12,2A29` `+UBTGSCD:0,13,02,14,2A24` |
| 6 | Read the Manufacturer Name String (**Apple Inc.**) on handle 12  | `AT+UBTGR=0,12`  | `+UBTGR:0,12,4170706C6520496E632E` |

## Advertising options

| Feature | Command | Description |
|---------|---------|-------------|
| Non-connectable legacy advertising | `AT+UBTADL=<adv_data>,<adv_type>` | `<adv_type>` `0` connectable and scannable (default), `1` non-connectable scannable, `2` non-connectable non-scannable. Custom data is up to 28 bytes for connectable and 31 bytes for non-connectable advertising |
| Discovery data filter | `AT+UBTDFD=<index>,<ad_type>,<data_filter>` | Up to 10 filters (index 0..9, pattern up to 10 bytes). Used when discovery is started with discovery type `data_filter` |

## Bluetooth security

Pairing establishes an encrypted link between two devices. Bonding stores the exchanged keys so that the peers can reconnect securely.

- `AT+UBTPM=1` — allow incoming pairing requests
- `AT+UBTIOC=<cap>` — set the I/O capabilities used during pairing
- `AT+UBTBSM=<mode>` — set the minimum security mode required for bonding
- `AT+UBTBDL` — list bonded devices
- `AT+UBTUB=<bd_addr>` — delete a stored bond

Bluetooth security is disabled by default and must be configured before use.

> **⚠ Behavior change in 3.4.0:** Pairing and bonding are stricter to defend against MITM attacks. The module now always bonds at the highest available security mode (even if `AT+UBTBSM` requests a lower minimum), sends a Security Request from the peripheral when reconnecting to a bonded central, and rejects unauthenticated pairing when a bond already exists for the peer.

For peers using Resolvable Private Addresses (RPA), the resolved identity address is returned as soon as it is available.

### Bluetooth security initiator

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set I/O capabilities to Display Yes/No (2)   |          `AT+UBTIOC=2` | `OK` |
| 2 | Only allow authenticated bonding with encrypted link (3)| `AT+UBTBSM=3` | `OK` |
| 3 | Allow pairing| `AT+UBTPM=1` | `OK` |
| 4 | Bond with the remote device | `AT+UBTB=BBBBBBBBBBBBp` | `OK` |
| 5 | Connected |  | `+UEBTC:0,BBBBBBBBBBBBp` |
| 6 | User confirmation request: check that the number is the same on both devices | | `+UEBTUC:BBBBBBBBBBBBp,786920` |
| 7 | Confirm with yes | `AT+UBTUC=BBBBBBBBBBBBp,1` | `OK` |
| 8 | Bond success | | `+UEBTB:BBBBBBBBBBBBp,0` |
| 9 | List bonded devices (optional) | `AT+UBTBDL` | `+UBTBDL:BBBBBBBBBBBBp` |

### Bluetooth security responder

The Peripheral role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Enable legacy advertising    | `AT+UBTAL` | `OK` |
| 2 | Set I/O capabilities to Display Yes/No (2)   |          `AT+UBTIOC=2` | `OK` |
| 3 | Only allow authenticated bonding with encrypted link (3)| `AT+UBTBSM=3` | `OK` |
| 4 | Allow pairing| `AT+UBTPM=1` | `OK` |
| 5 | Connected |  | `+UEBTC:0,AAAAAAAAAAAAp` |
| 6 | User confirmation request: check that the number is the same on both devices | | `+UEBTUC:AAAAAAAAAAAAp,786920` |
| 7 | Confirm with yes | `AT+UBTUC=AAAAAAAAAAAAp,1` | `OK` |
| 8 | Bond success | | `+UEBTB:AAAAAAAAAAAAp,0` |
| 9 | List bonded devices (optional) | `AT+UBTBDL` | `+UBTBDL:AAAAAAAAAAAAp` |

# Wi-Fi connection use cases

The examples use these placeholder MAC addresses; replace them with the real addresses of your devices.

- Station MAC address: AAAAAAAAAAAA
- Access Point MAC address: BBBBBBBBBBBB

## Wi-Fi station WPA2 and WPA3

![wi-fi-station](https://content.u-blox.com/sites/default/files/2024-02/wi-fi-station.png)

NORA-W36 connects as a Wi-Fi station to an Access Point. The connection is set to **DHCP client** by default. To use a static IP, set the IP address, subnet mask, gateway and DNS with `AT+UWSIPS`. Store the configuration with `AT&W` to keep it across reboots.

NORA-W36 supports **WPA2 Personal** and **WPA3 Personal** (SAE) as a station. As an Access Point only WPA2 Personal is supported.

> **⚠ Migration note (since 3.4.0):** Security parameters must be configured **before** `AT+UWSC`, see [Quick Wi-Fi connection](#quick-wi-fi-connection).

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set the SSID                  | `AT+UWSCP=0,"ssid"`               | `OK` |
| 2a | Set the password (WPA2/WPA3 compatible)       | `AT+UWSSW=0,"password",0`         | `OK` |
| 2b | Set the password (WPA3 only)                  | `AT+UWSSW=0,"password",1`         | `OK` |
| 3 | Connect                     | `AT+UWSC=0`                      | `OK` |
| 4 | Wait for the Wi-Fi link                  |                                   | `+UEWLU:0,BBBBBBBBBBBB,6` |
| 5 | Wait for the network interface                |                                   | `+UEWSNU` |
| 6 | Read the IP address (optional)               | `AT+UWSNST=0`                     | `+UWSNST:0,192.168.1.179` |
| 7 | Read the RSSI (optional)                     | `AT+UWSST=4`                     | `+UWSST:4,-66` |
| 8 | Disconnect                   | `AT+UWSDC`                       | `OK` |

`AT+UWSSW=<wlan_handle>,<password>,<wpa_threshold>`: the password is 8..63 characters; `wpa_threshold` `0` accepts WPA2 or higher, `1` requires WPA3.

Once the station has an IP address, the module can open [TCP](#wi-fi-tcp-client) / [UDP](#wi-fi-udp-client) sockets, an [MQTT session](#mqtt-use-cases) or an [HTTP request](#http-and-https-use-cases).

**Connect at startup:** send `AT+UWSC=0`, `AT&W` and `AT+CPWROFF`. The station configuration is stored in flash and the module connects with the stored SSID and password at startup.

## Wi-Fi PEAP enterprise security

NORA-W36 connects as a Wi-Fi station using PEAP (PEAPv0 with EAP-MSCHAPv2) and a RADIUS server.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set the SSID                  | `AT+UWSCP=0,"NORA-W36 Access Point"`               | `OK` |
| 2 | Set the user and password with TLS 1.3    | `AT+UWSSP=0,2,"peap_user_name","peap_password"`            | `OK` |
| 3 | Connect                     | `AT+UWSC=0`                         | `OK` |
| 4 | Wait for the Wi-Fi link                  |                                   | `+UEWLU:0,BBBBBBBBBBBB,6` |
| 5 | Wait for the network interface                |                                   | `+UEWSNU` |

`AT+UWSSP=<wlan_handle>,<tls_version>,<peap_user>,<peap_password>[,<ca_name>]`. User and password are 1..31 characters each. See [TLS version configuration](#tls-version-configuration) for `<tls_version>`.

## Wi-Fi EAP-TLS enterprise security

NORA-W36 connects as a Wi-Fi station using EAP-TLS. The CA certificate, client certificate and client key must be uploaded first, see [Certificate management](#certificate-management).

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Write the X.509 certificate and private key using [binary data](#simple-binary-data-example) | `AT+USECUB=0,"ca.pem"{binary_content}` + `AT+USECUB=1,"client.pem"{binary_content}` + `AT+USECUB=2,"client.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 2 | Set the SSID                  | `AT+UWSCP=0,"NORA-W36 Access Point"`               | `OK` |
| 3 | Set the certificates and key with TLS 1.3    | `AT+UWSSE=0,2,"ca.pem","client.pem","client.key"`            | `OK` |
| 4 | Connect                     | `AT+UWSC=0`                         | `OK` |
| 5 | Wait for the Wi-Fi link                  |                                   | `+UEWLU:0,BBBBBBBBBBBB,6` |
| 6 | Wait for the network interface                |                                   | `+UEWSNU` |

## Wi-Fi access point WPA2

NORA-W36 operates as an Access Point with **WPA2 Personal** encryption (WPA3 is not supported in Access Point mode) and a **DHCP server** that assigns addresses from 192.168.1.100 to connected stations. The password (`AT+UWAPSW`) is 8..63 characters.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Set the SSID and channel 6   | `AT+UWAPCP="NORA-W36 Access Point",6`               | `OK` |
| 2 | Set the password (WPA2)      | `AT+UWAPSW="mypassword"`            | `OK` |
| 3 | Activate the Access Point (the DHCP server is enabled by default)   | `AT+UWAPA`                        | `OK` |
| 4 | Wait for the Access Point        |                                   | `+UEWAPU` |
| 5 | Wait for the network interface        |                                   | `+UEWAPNU` |
| 6 | Read the IP address of the AP (optional)        | `AT+UWAPNST=0`    | `+UWAPNST:0,192.168.1.80` |
| 7 | A station connects            |                    | `+UEWAPSA:AAAAAAAAAAAA`  |
| 8 | A station disconnects            |                    | `+UEWAPSDA:AAAAAAAAAAAA`  |
| 9 | Deactivate the Access Point           |    `AT+UWAPD`        | `OK` |

Once a station has joined, the module can open [TCP](#wi-fi-tcp-client) / [UDP](#wi-fi-udp-client) sockets, an [MQTT session](#mqtt-use-cases) or an [HTTP request](#http-and-https-use-cases) towards the station.

**Activate at startup:** send `AT+UWAPA`, `AT&W` and `AT+CPWROFF`. The Access Point state is stored in flash and the module activates the Access Point with the stored SSID and password at startup.

**Static IP:** the Access Point uses 192.168.1.80 by default. Set a different address, subnet mask and gateway **before** `AT+UWAPA`, and read the active configuration with `AT+UWAPIP?`.

| Nr | Instructions | AT command | AT event |
|---|---|---|---|
| 1 | Set the static IPv4 address, subnet mask and gateway | `AT+UWAPIPS="10.0.0.1","255.255.255.0","10.0.0.1"` | `OK` |
| 2 | Store the configuration (optional) | `AT&W` | `OK` |
| 3 | Activate the Access Point | `AT+UWAPA` | `OK` |
| 4 | Read the configuration | `AT+UWAPIP?` | `+UWAPIP:1,"10.0.0.1","255.255.255.0","10.0.0.1","0.0.0.0","0.0.0.0"` |

# Wi-Fi Sockets use cases

The socket commands work on the Wi-Fi station and Access Point interfaces. Use host names or IP addresses in `AT+USOC`, for example `AT+USOC=0,"www.u-blox.com",80` or `AT+USOC=0,"75.2.60.5",80`. `ATE0` turns off the AT command echo, which speeds up data transfer in AT mode and makes parsing easier.

## Wi-Fi TCP client

NORA-W36 initiates a TCP connection to a server. One TCP socket sends and receives data.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 2 | Connect to the server on port 5003                | `AT+USOC=0,"192.168.0.200",5003`      | `+UESOC:0` |
| 3 | Close the socket             |  `AT+USOCL=0`                 | `+UESOCL:0`  |

With the socket connected, send with `AT+USOWS` (string) or `AT+USOWB` (binary) and receive with `AT+USORS` / `AT+USORB`, see [string vs binary modes](#string-mode).

## Wi-Fi TCP server (listener)

NORA-W36 accepts incoming TCP connections on a port.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 2 | Start the listener on port 5003            | `AT+USOL=0,5003`      | `+UESOC:0` |
| 3 | Incoming connection: handle 1 is created for it                |                     | `+UESOIC:0,192.168.1.100,1` |
| 4 | The remote side closes the connection          |                   | `+UESOCL:1`  |
| 5 | Close the listener            |  `AT+USOCL=0`                 | `+UESOCL:0`  |

On the new handle (here `1`) send with `AT+USOWS` / `AT+USOWB` and receive with `AT+USORS` / `AT+USORB`.

## Wi-Fi UDP client

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a UDP socket                        | `AT+USOCR=17`                        | `+USOCR:0` |
| 2 | Connect to UDP port 5003                | `AT+USOC=0,"192.168.0.200",5003`      | `+UESOC:0` |
| 3 | Close the socket               |  `AT+USOCL=0`                 | `+UESOCL:0`  |

With the UDP socket connected, send datagrams with `AT+USOWS` / `AT+USOWB`. To receive datagrams, use a listener socket.

## Wi-Fi UDP server (listener)

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a UDP socket                        | `AT+USOCR=17`                        | `+USOCR:0` |
| 2 | Start the listener on port 5003            | `AT+USOL=0,5003`      | `+UESOC:0` |
| 3 | Close the listener            |  `AT+USOCL=0`                 | `+UESOCL:0`  |

Receive datagrams with `AT+USORS` (string) or `AT+USORB` (binary), or `AT+USORFS` / `AT+USORFB` to also get the sender address.

## Wi-Fi TCP using TLS without certificates

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 2 | Add a TLS 1.3 context to the socket                    | `AT+USOTLS=0,2`                         | `OK` |
| 3 | Connect to the TLS server on port 443                | `AT+USOC=0,"www.u-blox.com",443`      | `+UESOC:0` |
| 4 | Close the socket             |  `AT+USOCL=0`                 | `+UESOCL:0`  |

Some older TLS servers do not support the TLS extensions that are enabled by default, see [TLS extensions configuration](#tls-extensions-configuration).

## Wi-Fi TCP using TLS with certificates

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Write the X.509 certificate and private key using [binary data](#simple-binary-data-example) | `AT+USECUB=0,"ca.pem"{binary_content}` + `AT+USECUB=1,"client.pem"{binary_content}` + `AT+USECUB=2,"client.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 2 | Create a TCP socket                        | `AT+USOCR=6`                        | `+USOCR:0` |
| 3 | Add a TLS 1.3 context with certificates                        | `AT+USOTLS=0,2,"ca.pem","client.pem","client.key"`                         | `OK` |
| 4 | Connect on port 443                | `AT+USOC=0,"www.u-blox.com",443`      | `+UESOC:0` |
| 5 | Close the socket             |  `AT+USOCL=0`                 | `+UESOCL:0`  |

## Certificate management

NORA-W36 stores X.509 certificates and private keys in a flat namespace and binds them by name into each TLS-enabled service (HTTPS, MQTT over TLS, secure sockets, EAP-TLS).

**Storage limits (NORA-W36 3.5.0, mbedTLS 3.6.4):**

- Maximum **8** credentials stored simultaneously (CAs, client certificates and private keys share the pool).
- Maximum **15&nbsp;360 bytes** per credential (a single certificate **or** a PEM-concatenated chain).
- Credential `<name>`: 1..32 characters. Private-key password (PKCS8/AES only): 1..64 characters.
- Format: PEM only (DER is not supported).
- Uploading the same `<name>` again overwrites the credential in full. There is no append.

| Command | Purpose |
|---------|---------|
| `AT+USECUB=<type>,<name>{binary_content}` | Upload a credential, see [Binary data](#binary-data) |
| `AT+USECL?` | List stored credentials |
| `AT+USECD=<name>` | Show details (SHA-256 fingerprint, size, validity) |
| `AT+USECR=<type>,<name>` | Remove one credential |
| `AT+USECR` | Remove all credentials |

`AT+USECUBI` and `AT+USECLI` are the equivalents for **internal** credentials, which `AT+USECL?` does not list and `AT+USECR` does not remove.

Credential types (`<cert_type>`): `0` root CA or CA bundle (verifies the remote peer), `1` client certificate or chain (mutual TLS), `2` client private key.

```text
AT+USECL?
+USECL:0,"ca-root"
+USECL:1,"device-cert"
+USECL:2,"device-key"

AT+USECD="device-cert"
+USECD:0,A1B2C3D4E5F6...           // SHA-256 fingerprint (hex)
+USECD:1,2048                      // Size in bytes
+USECD:2,61F2D000                  // Not valid before: Unix time in hex
+USECD:3,6586A400                  // Not valid after: Unix time in hex
```

The fingerprint is returned as a continuous hex string; `openssl x509 -noout -fingerprint -sha256 -in ca.pem` prints the same value with colons. The validity dates are hexadecimal Unix timestamps; for example `6586A400` is 1703462400, 2023-12-25 00:00:00 UTC.

### Certificate chains

A credential is **one slot** regardless of how many certificates the PEM contains. Concatenate the PEM blocks in chain order before `AT+USECUB`.

- **Server CA bundle (`cert_type=0`)**: root and any intermediates the server does not send itself. The order is not strict.
- **Client certificate chain (`cert_type=1`)**: device leaf **first**, intermediates after, root **omitted**.

### Password-protected private keys

AES-encrypted PKCS8 private keys are supported. Pass the password as the third parameter; the PEM follows in the binary block as for an unencrypted key:

```text
AT+USECUB=2,"device_key","<password>"{<encrypted PKCS8 PEM>}
```

### TLS rules and limitations

- There is no CRL (revocation) support.
- SNI is enforced by default for TLS 1.2 and later; a server without an SNI-matching certificate fails the handshake. Disable it with `AT+USETE0=0` if needed. EAP-TLS does not support SNI.
- The device clock must be inside the certificate validity window. An unset clock causes `BADCERT_FUTURE` / `BADCERT_EXPIRED` errors. Set the time with [NTP](#network-time-protocol-ntp-use-cases) before opening TLS connections.
- If a handshake fails with `unknown CA`, the server probably sends only its leaf certificate. Inspect with `openssl s_client -connect <host>:<port> -showcerts`, append the missing intermediates to the PEM uploaded as `cert_type=0` and upload it again.

### Creating test certificates with OpenSSL

```bash
openssl genrsa -out ca.key 2048
openssl req -x509 -sha256 -new -nodes -key ca.key -days 365 -out ca.pem
openssl req -newkey rsa:2048 -keyout server.key -out server.csr -nodes
openssl x509 -req -CA ca.pem -CAkey ca.key -in server.csr -out server.pem -days 365 -CAcreateserial
openssl req -newkey rsa:2048 -keyout client.key -out client.csr -nodes
openssl x509 -req -CA ca.pem -CAkey ca.key -in client.csr -out client.pem -days 365 -CAcreateserial
```

Use 4096 instead of 2048 for 4096-bit keys. Test a mutual-TLS server locally with:

```bash
openssl s_server -CAfile ca.pem -key server.key -cert server.pem -accept 44331 -tls1_3 -state -Verify 1
openssl s_client -connect localhost:44331 -CAfile ca.pem -key client.key -cert client.pem -tls1_3
```

On Windows Git Bash prefix interactive OpenSSL commands with `winpty`.

## TLS version configuration

All TLS-enabled commands take the same `<tls_version>` parameter:

| Value | Meaning |
|-------|---------|
| `0` | TLS disabled |
| `1` | TLS 1.2 only |
| `2` | TLS 1.3 only |
| `3` | TLS 1.2 or 1.3 (negotiates the highest available) |

| Protocol | AT command | Example |
|----------|------------|---------|
| EAP-TLS | `AT+UWSSE` | `AT+UWSSE=0,2,"ca.pem","client.pem","client.key"` |
| PEAP | `AT+UWSSP` | `AT+UWSSP=0,2,"username","password"` |
| TCP socket | `AT+USOTLS` | `AT+USOTLS=0,2,"ca.pem","client.pem","client.key"` |
| MQTT | `AT+UMQTLS` | `AT+UMQTLS=0,2,"ca.pem","client.pem","client.key"` |
| HTTP | `AT+UHTCTLS` | `AT+UHTCTLS=0,2,"ca.pem","client.pem","client.key"` |

## TLS extensions configuration

TLS extensions are enabled by default and configured on system level. Disable them for servers that do not support them, see [RFC 6066](https://www.rfc-editor.org/rfc/rfc6066.html).

| Extension | AT command | Default |
|-----------|------------|---------|
| Server Name Indication (SNI) | `AT+USETE0=<enabled>` | Enabled |
| Handshake fragmentation (Maximum Fragment Length Negotiation) | `AT+USETE1=<enabled>` | Enabled |

`<enabled>` is `1` (enabled) or `0` (disabled). Read all settings with `AT+USETE?`. Store with `AT&W` and `AT+CPWROFF` to keep them across reboots.

# MQTT use cases

NORA-W36 includes an MQTT v3.1.1 client (MQTT v5.0 is not supported) with TLS 1.2/1.3, QoS 0-2, retained messages and last will. Set up the Wi-Fi connection first, see [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3).

- Only one MQTT command (connect, disconnect, subscribe or publish) can be outstanding at a time. Wait for the corresponding URC (`+UEMQC`, `+UEMQDC`, `+UEMQSC`, `+UEMQPC`) before the next command.
- `AT+UMQPS=<mqtt_id>,<qos>,<retain>,<topic>,<message>` publishes a string; QoS is `0` at most once, `1` at least once, `2` exactly once, and retain `1` keeps the message on the broker.
- `+UEMQDA` signals a received message and `+UEMQDD` a message that was dropped because it could not be stored.
- Maximum message size: 1000 bytes per string call, 5000 bytes per binary call.

## MQTT client without TLS - Mosquitto

![mqtt](https://content.u-blox.com/sites/default/files/2024-09/mqtt_no_tls.png)

NORA-W36 connects as an MQTT client to test.mosquitto.org on port 1883 without TLS. Client ID, user name and password are not used.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure the broker host and port              | `AT+UMQCP=0,"test.mosquitto.org",1883`| `OK` |
| 2 | Read the connection parameters (optional)          | `AT+UMQCP=0` | `+UMQCP:0,"test.mosquitto.org",1883,"",""` |
| 3 | Connect                    | `AT+UMQC=0`                            | `OK` then `+UEMQC:0` |
| 4 | Publish a message on **pubtopic**       | `AT+UMQPS=0,0,0,"pubtopic","Hello from NORA-W36"`                  | `OK` |
| 5 | Subscribe to **subtopic**                | `AT+UMQS=0,0,"subtopic"`            | `OK` then `+UEMQSC:0,0` |
| 6 | Publish **Hello from remote device** to **subtopic** from another client | -  | - |
| 7 | A message is received                |                                   | `+UEMQDA:0,24` |
| 8 | Read the message                                | `AT+UMQRS=0`                         | `+UMQRS:0,"subtopic",24,"Hello from remote device"` |
| 9 | Disconnect                    | `AT+UMQDC=0`                            | `OK` then `+UEMQDC:0,<reason>` |

Use `#` as topic to subscribe to all topics. Not all brokers support this, for example Azure IoT Hub does not.

## MQTT TLS client - Mosquitto

![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mosquitto-text-side.png)

NORA-W36 connects to test.mosquitto.org on port **8884** (TLS, client certificate required). Generate the client certificate and key as described on [test.mosquitto.org/ssl](https://test.mosquitto.org/ssl/) and download the CA certificate [mosquitto.org.crt](https://test.mosquitto.org/ssl/mosquitto.org.crt).

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure the broker host and port              | `AT+UMQCP=0,"test.mosquitto.org",8884`| `OK` |
| 2 | Write the X.509 certificate and private key using [binary data](#simple-binary-data-example) | `AT+USECUB=0,"mosquitto.org.crt"{binary_content}` + `AT+USECUB=1,"client.crt"{binary_content}` + `AT+USECUB=2,"client.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Set up TLS 1.3 with the certificates          | `AT+UMQTLS=0,2,"mosquitto.org.crt","client.crt","client.key"`| `OK` |
| 4 | Connect                    | `AT+UMQC=0`                            | `OK` then `+UEMQC:0` |

Publish, subscribe, read and disconnect as in [MQTT client without TLS](#mqtt-client-without-tls---mosquitto).

## MQTT TLS client - thingstream

![mqtt](https://content.u-blox.com/sites/default/files/2024-04/u-blox-thingstream.png)

[Thingstream](https://www.u-blox.com/en/product/thingstream) is the u-blox service delivery platform for IoT Communication-as-a-Service and IoT Location-as-a-Service. NORA-W36 connects with a CA root certificate, client ID, user name and password. Thingstream uses the [Amazon Root CA 1](https://www.amazontrust.com/repository/AmazonRootCA1.pem).

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure host, port, client ID, user name and password             | `AT+UMQCP=0,"mqtt.thingstream.io",8883,"device:78e3d356-876f-483b-872f-3485853fAAAA","HMVK8C09FQP245O2BBBB","ofYyBB/L3GkPvo060J6Dv+t+mfrh0XpGMcf7CCCC"`| `OK` |
| 2 | Write the CA root certificate using [binary data](#simple-binary-data-example) | `AT+USECUB=0,"AmazonRootCA1.pem"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Set up TLS 1.2 with the CA certificate only (no client certificate)                  | `AT+UMQTLS=0,1,"AmazonRootCA1.pem"`| `OK` |
| 4 | Connect                    | `AT+UMQC=0`                            | `OK` then `+UEMQC:0` |

## MQTT TLS client - AWS IoT core

![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mqtt.png)

NORA-W36 connects to Amazon AWS IoT Core on port 8883 with a CA root certificate, client certificate and private key.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure the endpoint and port              | `AT+UMQCP=0,"a3loryode2aaaa-ats.iot.us-east-2.amazonaws.com",8883`| `OK` |
| 2 | Write the X.509 certificate and private key using [binary data](#simple-binary-data-example) | `AT+USECUB=0,"AmazonRootCA1.pem"{binary_content}` + `AT+USECUB=1,"aws_client.crt"{binary_content}` + `AT+USECUB=2,"aws_priv_key.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Set up TLS 1.2 with the certificates                  | `AT+UMQTLS=0,1,"AmazonRootCA1.pem","aws_client.crt","aws_priv_key.key"`| `OK` |
| 4 | Connect                    | `AT+UMQC=0`                            | `OK` then `+UEMQC:0` |

## MQTT TLS client - Azure IoT hub

![mqtt](https://content.u-blox.com/sites/default/files/2024-02/mqtt.png)

NORA-W36 connects to Microsoft Azure IoT Hub on port 8883 using certificates. Azure IoT Hub is not a full-featured MQTT broker and does not support all behaviors of MQTT v3.1.1.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Configure host, port, client ID and user name   | `AT+UMQCP=0,"iothub-test-sw.azure-devices.net",8883,"device1","iothub-test-sw.azure-devices.net/device1/"`| `OK` |
| 2 | Write the X.509 certificate and private key using [binary data](#simple-binary-data-example) | `AT+USECUB=0,"AzureCa.pem"{binary_content}` + `AT+USECUB=1,"azure_client.crt"{binary_content}` + `AT+USECUB=2,"azure_priv_key.key"{binary_content}` **Note**: Brackets { } should NOT be sent | `OK` |
| 3 | Set up TLS 1.2 with the certificates                  | `AT+UMQTLS=0,1,"AzureCa.pem","azure_client.crt","azure_priv_key.key"`| `OK` |
| 4 | Connect                    | `AT+UMQC=0`                            | `OK` then `+UEMQC:0` |

## MQTT last will and testament

`AT+UMQLWT=<mqtt_id>,<topic>,<will_msg>[,<qos>[,<retain>]]` configures the message the broker publishes if the client disconnects unexpectedly. Set it before `AT+UMQC`; it can be stored with `AT&W`.

```text
AT+UMQLWT=0,"device/status","offline",1,1
OK
```

# HTTP and HTTPS use cases

NORA-W36 includes an HTTP/1.1 client with GET, POST, PUT, DELETE and HEAD requests and optional TLS. Set up the Wi-Fi connection first, see [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3).

- Request and response bodies pass through the AT interface in chunks. `AT+UHTCRPOS`, `AT+UHTCRPUS` and `AT+UHTCGBS` handle up to **1000 bytes** per call. The binary read `AT+UHTCGBB` handles up to **2048 bytes** per call. `<more_to_read>` in the response tells if more body data is available.
- The binary write commands (`AT+UHTCRPOB`, `AT+UHTCRPUB`) are streamed: when `Content-Length` is set in the request header, several calls add up to that length; otherwise the bytes of a single call become the `Content-Length`.
- TLS is enabled for a session with `AT+UHTCTLS`. `<tls_version>` and the certificates are described in [TLS version configuration](#tls-version-configuration).
- A request can have up to 10 custom header fields (`AT+UHTCRHAF`: name 1..30 and value 1..70 characters). `AT+UHTCRHCS` sets a complete custom header and `AT+UHTCRHCC` clears the header configuration.
- String parameters use `\"` for a double quote, see [String mode](#string-mode).

## Simple HTTP get request

Target: `http://httpbin.org/get`

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure the server | `AT+UHTCCP=0,"httpbin.org",80` | `OK` |
| 2 | Set the request path | `AT+UHTCRP=0,"/get"` | `OK` |
| 3 | Send the GET request | `AT+UHTCRG=0` | `OK` |
| 4 | Wait for the response | | `+UEHTCRS:0,200,"OK"` |
| 5 | Read the response header | `AT+UHTCGH=0` | `+UHTCGH:0,0,"HTTP/1.1 200 OK..."` |
| 6 | Read the response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,0,<len>,"{\"args\":{}..."` |
| 7 | Disconnect | `AT+UHTCDC=0` | `OK` |

## HTTPS get with certificate validation

Target: `https://api.github.com/repos/octocat/Hello-World`

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Upload the CA certificate | `AT+USECUB=0,"github-ca.pem"{binary certificate data}` | `OK` |
| 2 | Configure the server | `AT+UHTCCP=0,"api.github.com",443` | `OK` |
| 3 | Enable TLS 1.3 with the CA certificate | `AT+UHTCTLS=0,2,"github-ca.pem"` | `OK` |
| 4 | Set the request path | `AT+UHTCRP=0,"/repos/octocat/Hello-World"` | `OK` |
| 5 | Add a User-Agent header | `AT+UHTCRHAF=0,"User-Agent","NORA-W36/1.0"` | `OK` |
| 6 | Send the GET request | `AT+UHTCRG=0` | `OK` |
| 7 | Wait for the response | | `+UEHTCRS:0,200,"OK"` |
| 8 | Read the response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,<more_to_read>,<len>,"{\"id\":123456..."` |
| 9 | Disconnect | `AT+UHTCDC=0` | `OK` |

## HTTP post with JSON data

Target: `https://httpbin.org/post`

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure the server | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Enable TLS (1.2 or 1.3) | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set the request path | `AT+UHTCRP=0,"/post"` | `OK` |
| 4 | Set the Content-Type header | `AT+UHTCRHAF=0,"Content-Type","application/json"` | `OK` |
| 5 | Send the POST request with a JSON body | `AT+UHTCRPOS=0,"{\"temperature\":25.6,\"humidity\":60.2}"` | `OK` |
| 6 | Wait for the response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Read the response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,<more_to_read>,<len>,"..."` |
| 8 | Disconnect | `AT+UHTCDC=0` | `OK` |

## HTTP post with binary data

Target: `https://httpbin.org/post`, payload `sensor_data.bin` (256 bytes).

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure the server | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Enable TLS (1.2 or 1.3) | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set the request path | `AT+UHTCRP=0,"/post"` | `OK` |
| 4 | Set the Content-Type header | `AT+UHTCRHAF=0,"Content-Type","application/octet-stream"` | `OK` |
| 5 | Send the POST request with binary data, see [Binary data](#binary-data) | `AT+UHTCRPOB=0{256 bytes of binary data}` | `+UHTCRPOB:0,256` |
| 6 | Wait for the response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Read the response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,<more_to_read>,<len>,"..."` |
| 8 | Disconnect | `AT+UHTCDC=0` | `OK` |

## HTTP delete request

Target: `https://httpbin.org/delete`

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Configure the server | `AT+UHTCCP=0,"httpbin.org",443` | `OK` |
| 2 | Enable TLS (1.2 or 1.3) | `AT+UHTCTLS=0,3` | `OK` |
| 3 | Set the request path | `AT+UHTCRP=0,"/delete"` | `OK` |
| 4 | Add an authorization header | `AT+UHTCRHAF=0,"Authorization","ApiKey abc123"` | `OK` |
| 5 | Send the DELETE request | `AT+UHTCRD=0` | `OK` |
| 6 | Wait for the response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Read the response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,<more_to_read>,<len>,"..."` |
| 8 | Disconnect | `AT+UHTCDC=0` | `OK` |

## HTTPS with mutual TLS authentication

| Nr | Instructions | AT Command | AT Response |
|---|---|---|---|
| 1 | Upload the CA certificate, client certificate and private key, see [Binary data](#binary-data) | `AT+USECUB=0,"server-ca.pem"{binary data}` + `AT+USECUB=1,"client.crt"{binary data}` + `AT+USECUB=2,"client.key"{binary data}` | `OK` |
| 2 | Configure the server | `AT+UHTCCP=0,"secure-api.example.com",443` | `OK` |
| 3 | Enable mutual TLS 1.3 | `AT+UHTCTLS=0,2,"server-ca.pem","client.crt","client.key"` | `OK` |
| 4 | Set the request path | `AT+UHTCRP=0,"/api/secure-data"` | `OK` |
| 5 | Send the GET request | `AT+UHTCRG=0` | `OK` |
| 6 | Wait for the response | | `+UEHTCRS:0,200,"OK"` |
| 7 | Read the response body | `AT+UHTCGBS=0,1000` | `+UHTCGBS:0,<more_to_read>,<len>,"..."` |
| 8 | Disconnect | `AT+UHTCDC=0` | `OK` |

# Network Time Protocol (NTP) use cases

NORA-W36 synchronizes the system clock with up to 5 NTP servers (ids 0..4). The network must allow UDP port 123.

| Nr| Instructions                              | AT command                        | AT event/Response              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Connect to Wi-Fi first           | See [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3) |  |
| 2 | Configure the NTP servers           | `AT+UNTSC=0,"pool.ntp.org"` `AT+UNTSC=1,"time.google.com"`      | `OK` |
| 3 | Enable the NTP client with the configured servers (`2` uses the servers from DHCP if available, otherwise the configured ones) | `AT+UNTE=1`                       | `OK` |
| 4 | Read the servers and their reachability                 | `AT+UNTSC?`                       | `+UNTSC:0,"pool.ntp.org","185.255.55.20",1` |
| 5 | Read the system time as Unix time in hex | `AT+USYTU?`                       | `+USYTU:66E7B2A4` |
| 6 | Store and restart                    | `AT&W` `AT+CPWROFF`                            | `OK` |

`66E7B2A4` (hex) is 1726460580, 2024-09-16 04:23:00 UTC. Remove a server with `AT+UNTSC=<id>,""`. `reachable=0` in the `+UNTSC` response means that the server does not answer; check the network and firewall.

# mDNS use cases

Multicast DNS (mDNS, RFC 6762) lets the module advertise itself on the local link as `<hostname>.local` so that other devices can find it without a DNS server. With DNS-SD (RFC 6763) the module also advertises services that hosts can browse for by type, for example `_http._tcp`. Wi-Fi (Station or Access Point) must be up before the responder is enabled.

| Command | Purpose |
|---|---|
| `AT+UMDE=<enabled>`   | Enable (`1`) or disable (`0`) the mDNS responder |
| `AT+UMDHN=<hostname>` | Set the hostname advertised as `<hostname>.local`. Defaults to the Wi-Fi hostname (`AT+UWHN`) |
| `AT+UMDSA=<service_type>,<protocol>,<port>[,<instance_name>]` | Register a DNS-SD service; returns `+UMDSA:<service_id>`. Protocol `0` = TCP, `1` = UDP. Up to 3 services |
| `AT+UMDSR=<service_id>` | Remove a service |
| `AT+UMDSL?` | List the registered services |
| `AT+UMDTRA=<service_id>,<txt_key>,<txt_value>` | Add or replace a TXT record (up to 10 per service) |
| `AT+UMDTRR=<service_id>,<txt_key>` | Remove a TXT record |
| `AT+UMDTRL=<service_id>` | List the TXT records |
| `AT+UMDTRC=<service_id>` | Clear all TXT records |

`+UEMDU` signals that the responder is up and `+UEMDD` that it is down, for example after a Wi-Fi disconnect.
If another device on the network already uses the hostname or a service instance name, the module renames its own name automatically and sends `+UEMDCD:<conflict_type>,<previous_name>,<new_name>`. `<conflict_type>` is `0` for a hostname conflict and `1` for a service instance name conflict. Read the active hostname with `AT+UMDHN?`.

| Nr | Instructions | AT command | AT event |
|----|--------------|------------|----------|
| 1 | Connect Wi-Fi, see [Quick Wi-Fi connection](#quick-wi-fi-connection) | | `+UEWLU`, `+UEWSNU` |
| 2 | Set the hostname | `AT+UMDHN="nora-w36"` | `OK` |
| 3 | Enable the responder | `AT+UMDE=1` | `OK` |
| 4 | From a host on the LAN: `ping nora-w36.local` | | reply from the module |
| 5 | Advertise an HTTP service on TCP port 80 | `AT+UMDSA="http",0,80,"NORA-W36 Sensor"` | `+UMDSA:0` `OK` |
| 6 | Add TXT records to service `0` | `AT+UMDTRA=0,"path","/api"` `AT+UMDTRA=0,"fw","3.5.0"` | `OK` |
| 7 | List services and TXT records | `AT+UMDSL?` `AT+UMDTRL=0` | `+UMDSL:0,"http",0,80,"NORA-W36 Sensor"` `+UMDTRL:0,"path","/api"` |
| 8 | Remove the service | `AT+UMDSR=0` | `OK` |

Browse from a host with `dns-sd -B _http._tcp` (macOS, Windows Bonjour) or `avahi-browse -t _http._tcp` (Linux). If the module is not found, check that the network does not block multicast (UDP port 5353, 224.0.0.251) and that `+UEWSNU` was received before `AT+UMDE=1`. `ERROR` is returned when the service or TXT record limit is reached.

# Roaming use cases

NORA-W36 supports client-initiated Wi-Fi roaming based on RSSI thresholds. It is **disabled by default**; enable it with `AT+UWSROE=1` before connecting. Both Access Points must use the same SSID and security configuration. There is a brief connectivity interruption during the handover.

| Command | Default | Valid values | Description |
|---------|---------|--------------|-------------|
| `AT+UWSROE=<roaming>` | 0 | 0: disable, 1: enable | Enable roaming |
|`AT+UWSROS0=<roaming_scanning_threshold>` | -70 | -95..0 | RSSI threshold that triggers scanning (dBm) |
|`AT+UWSROS1=<roaming_switch_limit>` | 10 | 1..50 | Minimum RSSI improvement needed (dB) |
|`AT+UWSROS2=<roaming_scan_interval>` | 5000 | 100..3600000 | Background scan interval (ms) |
| `AT+UWSROS3=<roaming_current_rssi>` | 0 | 0: fixed threshold, 1: current RSSI | Roaming calculation mode |
|`AT+UWSROS4=<roaming_delay_time>` | 0 | 0..30000 | Handover delay (ms) |
| `AT+UWSROS5=<roaming_all_channels>` | 1 | 0: current channel only, 1: all channels | Scan scope |

**Fixed threshold mode (`AT+UWSROS3=0`):** scanning starts when the RSSI drops to -70 dBm or below. The module roams if an Access Point with `-70 + 10 = -60 dBm` or better is found.

**Current RSSI mode (`AT+UWSROS3=1`):** the target is the current RSSI plus the switch limit. With `AT+UWSROS1=3` and a current RSSI of -78 dBm the module roams to an Access Point with -75 dBm or better.

```text
AT+UWSROE=1      // Enable roaming
AT+UWSROS0=-70   // Start scanning at -70 dBm
AT+UWSROS1=3     // Require 3 dB improvement
AT+UWSROS3=1     // Current RSSI mode
```

# Power save use cases

## Auto sleep

By default no low power mode is enabled in NORA-W36, for maximal performance and response time. Power save level `1` reduces power consumption at the cost of higher latency.

| Command | Purpose | Default |
|---------|---------|---------|
| `AT+UPMPSL=<level>` | Power save level: `0` no power save, `1` moderate power save | `0` |
| `AT+UPMPSTO=<timeout_ms>` | Active state timeout after the last activity, 1..60000 ms | `1000` |

```text
AT+UPMPSL=1
AT+UPMPSTO=2000
AT&W             // Store the settings
AT+CPWROFF       // Restart to apply the stored settings
```

- In power save level 1 only baud rates up to 115200 are allowed.
- The first AT command after the timeout cannot be longer than 16 bytes.
- No further action is needed from the host; any AT command or data activity restarts the timeout.

## Light sleep

`AT+UPMS` puts the module in light sleep. The Wi-Fi connection is kept and baud rates above 115200 are supported. The host keeps receiving events, but the module does not respond to AT commands. On a connection event the module wakes up, sends the URC and goes back to sleep. Bluetooth must be disabled (`AT+UBTM=0`) before light sleep can be used.
| Nr | Instructions | AT command |
|----|--------------|------------|
| 1 | Disable Bluetooth, store and restart | `AT+UBTM=0` `AT&W` `AT+CPWROFF` |
| 2 | Connect Wi-Fi, see [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3) | |
| 3 | Enter light sleep | `AT+UPMS` |
| 4 | Exit light sleep: pull the `WAKE_UP` pin low, or send a character on the UART and wait 50 ms | |

## Deep sleep

Deep sleep is the most efficient power level and almost like a power off; no radio communication is possible.

- Enter deep sleep with `AT+UPMDS`.- Wake up the module by pulling the module wake-up pin low, see the data sheet for the pin.
- After wake-up the module is in the same state as after a reset.

# Send and receive data

NORA-W36 supports three ways to exchange data:

| Mode | Characters | Typical use |
|------|------------|-------------|
| **String mode** | Printable ASCII (`0x21-0x7E`, `0xA1-0xFF`) | Text, JSON, XML, NMEA |
| **Binary mode** | Full byte range (`0x00-0xFF`) | Files, certificates, binary protocols |
| **Transparent mode** | Full byte range (`0x00-0xFF`) | Serial cable replacement, highest throughput |

Received data is delivered in one of two ways: in **buffered mode** (default) a data-available event is sent and the host reads the data; in **direct mode** the data is delivered in the event. Select the mode with `AT+USPSRM` for SPS and `AT+USORM` for sockets.

## String mode

String parameters are enclosed in double quotes. Use the escape sequences `\"` (double quote), `\\` (backslash), `\r`, `\n`, `\t`, `\0` (null) and `\xHH` (any byte).

`AT+USORM=<receive_mode>`: `0` buffered mode (`+UESODA`), `1` direct string mode (`+UESODS` for TCP and `+UESODSF` for UDP).

`AT+USPSRM=<receive_mode>`: `0` buffered mode (`+UESPSDA`), `1` direct string mode (`+UESPSDS`).

| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write socket data | `AT+USOWS=0,"Hello from NORA-W36"` | `+USOWS:0,19` `OK` |
| 2 | Incoming socket data (buffered mode) | | `+UESODA:0,19` |
| 3 | Read socket data | `AT+USORS=0,19` | `+USORS:0,19,"Hello from NORA-W36"` |
| 4 | Write SPS data | `AT+USPSWS=0,"Hello from NORA-W36"` | `+USPSWS:0,19` `OK` |
| 5 | Incoming SPS data (buffered mode) | | `+UESPSDA:0,19` |
| 6 | Read SPS data | `AT+USPSRS=0,19` | `+USPSRS:0,19,"Hello from NORA-W36"` |

The write response contains the number of bytes that were written. It can be less than requested when the socket transmit buffer is full; the remaining data must be sent again later.

## Binary mode

Use binary mode for files and binary protocols. See [Binary data](#binary-data) for the frame format.

> **Binary AT-command framing in one line.** Every binary command (`…B`) is followed **immediately** by a 3-byte header `01 <lenMSB> <lenLSB>` and then the raw payload bytes. Commas inside the parameter list are normal — the rule is that the **last** parameter butts straight up against the `0x01` (SOH) byte: no trailing `,`, no space, no `\r`. The `0x01` IS the separator between the parameter list and the binary block. Sending the same command in string form (with a trailing `,"..."` instead of the SOH frame) returns **`ERROR:47`** (`U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD`).

`AT+USORM=2` selects direct binary mode: `+UESODB:<socket_handle>{binary_data}` for TCP and `+UESODBF:<socket_handle>,<remote_ip>,<remote_port>{binary_data}` for UDP.

`AT+USPSRM=2` selects direct binary mode for SPS: `+UESPSDB:<conn_handle>{binary_data}`.

| Command | Syntax | Response |
|---------|--------|----------|
| Socket write | `AT+USOWB=<socket_handle>{binary_data}` | `+USOWB:<socket_handle>,<written_length>` |
| Socket read | `AT+USORB=<socket_handle>,<length>` | `+USORB:<socket_handle>{binary_data}` |
| SPS write | `AT+USPSWB=<conn_handle>{binary_data}` | `+USPSWB:<conn_handle>,<written_length>` |
| SPS read | `AT+USPSRB=<conn_handle>,<length>` | `+USPSRB:<conn_handle>{binary_data}` |

`{binary_data}` is the 3-byte header `01 <lenMSB> <lenLSB>` followed by the raw payload. Read example: `AT+USPSRB=0,19` returns `+USPSRB:0` + `01 00 13` + 19 raw payload bytes.

## Transparent mode overview

Transparent mode (TM) turns NORA-W36 into a bridge that forwards all UART data to a remote device without AT command processing, like the data mode of legacy u-blox short range products. It works with TCP, UDP (Wi-Fi) and SPS (Bluetooth LE) connections.

- Only **one active connection** is allowed at a time and it must be established before entering transparent mode.
- All UART data is sent unmodified. Return to command mode with the escape sequence `+++` (no line ending), after at least 1 second without data before and after the sequence. The timing can be changed with `AT+UTMES=<pre_timeout>,<post_timeout>,<escape_timeout>` (defaults 1000, 1000 and 200 ms; the escape character is set with `ATS2`).
- A partial escape sequence is not transmitted to the peer until another character is sent (known limitation).

`AT+UTM=<link_type>,<handle>` enters transparent mode on an existing connection: `<link_type>` `0` SPS, `1` TCP socket, `2` UDP socket; `<handle>` is the connection or socket handle.

```text
AT+UTM=0,0                        // SPS connection 0
OK
Hello from NORA-W36!    // forwarded to the remote device
+++                               // no CR/LF
OK
```

```text
AT+USOCR=6
+USOCR:0
AT+USOC=0,"192.168.1.100",8080
OK
AT+UTM=1,0                        // TCP socket 0
OK
```

For UDP, bind a local port with `AT+USOB` to receive and send with `AT+USOSTS` (or `AT+USOSTB`) before entering transparent mode on the UDP socket:

```text
AT+USOCR=17
+USOCR:1
AT+USOB=1,5005                    // Receive on local port 5005
OK
AT+USOSTS=1,"192.168.1.174",5003,"test"
+USOSTS:1,4
AT+UTM=2,1                        // UART data goes to 192.168.1.174:5003, UDP data to port 5005 goes to the UART
OK
```

**Connection status on the Host Wakeup pin:** `AT+USYHWP=1` configures the Host Wakeup pin to indicate the transparent mode connection status. The default `AT+USYHWP=0` leaves the pin free to use as a GPIO. The setting is stored with `AT&W` and takes effect after a reboot.

## Persistent transparent mode

Persistent transparent mode (TMP) enters transparent mode automatically at startup. The configuration is stored in flash.

`AT+UTMP=<link_type>,<config_id>`: `<link_type>` `0` for an SPS link (`<config_id>` from `AT+UBTP`) or `1` for a socket (TCP or UDP, `<config_id>` from `AT+USOP`).
`AT+UTMP` uses different link types than `AT+UTM`: `1` means socket (TCP or UDP) instead of TCP only.

| Step | Description | AT Command | Expected Response |
|------|-------------|------------|-------------------|
| 1 | Configure the remote BLE device | `AT+UBTP=BBBBBBBBBBBB,1` | `+UBTP:200` |
| 2 | Enable persistent transparent mode | `AT+UTMP=0,200` | `OK` |
| 3 | Store and restart | `AT&W` `AT+CPWROFF` | `+STARTUP` |
| 4 | Persistent transparent mode is active | *(automatic)* | |
| 5 | Exit to AT mode when needed | `+++` | `OK` |

For a persistent socket, configure Wi-Fi first (see [Wi-Fi station](#wi-fi-station-wpa2-and-wpa3)), then:

| Step | Description | AT Command | Expected Response |
|------|-------------|------------|-------------------|
| 1 | Create a persistent TCP socket (`17` for UDP) | `AT+USOPCR=6` | `+USOPCR:100` |
| 2 | Configure the server | `AT+USOP=100,"192.168.0.26",5003` | `OK` |
| 3 | For UDP, bind a local port to receive (optional) | `AT+USOB=100,5005` | `OK` |
| 4 | Enable persistent transparent mode | `AT+UTMP=1,100` | `OK` |
| 5 | Store and restart | `AT&W` `AT+CPWROFF` | `+STARTUP` |
| 6 | The connection and transparent mode start automatically | *(automatic)* | |

If the connection fails at startup the module stays in AT mode. Clear the configuration with `AT+UTMPC`, `AT&W` and `AT+CPWROFF`.

# Binary data

Binary data lets you send raw bytes, for example files and certificates, through AT commands. Every binary transmission consists of a 3-byte header followed by the data.

| Byte Position | Value | Description  |
|---------------|-------|------------- |
| Byte 1 | `0x01` | Start marker (SOH) |
| Byte 2 | MSB | Most significant byte of the data length |
| Byte 3 | LSB | Least significant byte of the data length |

Example: for 2 bytes of data the header is `0x01, 0x00, 0x02`. The length is big-endian; for example 256 bytes is `01 01 00` and 1024 bytes is `01 04 00`.

## Important rules

- **Do** send the binary data immediately after the last parameter of the AT command.
- **Do not** add a *trailing* comma (`,`) after the last parameter — the SOH byte (`0x01`) is the separator. Commas *between* parameters earlier in the list are normal, see the certificate example below.
- **Do not** add a carriage return (`\r`), spaces or a hexadecimal escape (`\x`) before the binary data.

> **If you send a binary command in string form** (with a trailing `,"..."` instead of the SOH-framed block) the module replies with **`ERROR:47`** (`U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD`). That error means "this is a `…B` command — use the binary frame described here."

## Simple binary data example

Send 2 bytes (`0xFF, 0xEE`) to socket 0. On the wire each cell is one byte; `│` separates the AT command, the 3-byte header and the payload:

```text
ascii :  A  T  +  U  S  O  W  B  =  0   │             │
hex   : 41 54 2B 55 53 4F 57 42 3D 30   │ 01 00 02    │ FF EE
                                         └─ SOH ─┼─ len ─┘   ↑ payload (2 bytes)
```

- `AT+USOWB=0` (10 ASCII bytes) writes to socket 0.
- `01` is the SOH start marker and `00 02` the length (2 bytes, big-endian).
- `FF EE` are the 2 raw payload bytes.

There is **no comma and no `\r`** between `=0` and `01`. The text form `AT+USOWB=0010002FFEE` seen in older documents prints the same bytes as ASCII hex digits and is **not** what travels down the UART.

Data received with `AT+USORB` includes the same header:

```text
resp  :  +  U  S  O  R  B  :  0          │             │
hex   : 2B 55 53 4F 52 42 3A 30          │ 01 00 02    │ FF EE
```

The text `Hello from NORA-W36` is 19 bytes (`0x0013`), so the header is `01 00 13`.

## Certificate upload example

Upload `ca.pem`, a certificate of 1342 bytes (`0x053E`), to slot 0:

```text
ascii :  A  T  +  U  S  E  C  U  B  =  0  ,  "  c  a  .  p  e  m  "   │             │  -  -  -  -  -  B  E  G  I  N  …
hex   : 41 54 2B 55 53 45 43 55 42 3D 30 2C 22 63 61 2E 70 65 6D 22   │ 01 05 3E    │  2D 2D 2D 2D 2D 42 45 47 49 4E …
                                                                       └─ SOH ─┼─ len ─┘   ↑ 1342 PEM bytes
```

- `AT+USECUB=0,"ca.pem"` uploads to slot 0 with the name `ca.pem`. The closing `"` is the last byte of the parameter list: no comma, no `\r` after it.
- `01 05 3E` is the header (1342 bytes) and the PEM follows verbatim, without escaping.
- The module confirms with `+USECUB:1342` and `OK`.

## Programming examples

Both examples write the AT command, the 3-byte header and the payload in **one** write so that the frame stays intact. Open the serial port in raw 8N1 mode and do **not** terminate the command with `\r` or `\n`. A single call accepts up to 1460 bytes for `AT+USOWB`.

### Python

```python
import serial

MAX_PAYLOAD = 1460  # bytes per AT binary call


def send_binary_data(port: serial.Serial, at_command: str, payload: bytes) -> None:
    """Send an AT command followed by the 3-byte binary header and the payload."""
    if len(payload) > MAX_PAYLOAD:
        raise ValueError(f"payload exceeds {MAX_PAYLOAD} bytes per call")
    header = b"\x01" + len(payload).to_bytes(2, "big")
    port.write(at_command.encode("ascii") + header + payload)


with serial.Serial("COM3", 115200) as port:
    send_binary_data(port, "AT+USOWB=0", b"Hello from NORA-W36")
```

### C (POSIX)

```c
#include <errno.h>
#include <stddef.h>
#include <stdint.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

/* Returns 0 on success, -1 on error (errno set). */
int send_binary_data(int fd, const char *at_command, const uint8_t *payload, size_t payload_len)
{
    if (payload_len > 0xFFFF) {
        errno = EMSGSIZE;
        return -1;
    }

    size_t cmd_len = strlen(at_command);
    size_t frame_len = cmd_len + 3 + payload_len;
    uint8_t *frame = malloc(frame_len);
    if (frame == NULL) {
        errno = ENOMEM;
        return -1;
    }

    memcpy(frame, at_command, cmd_len);
    frame[cmd_len] = 0x01;                                    /* start marker */
    frame[cmd_len + 1] = (uint8_t)((payload_len >> 8) & 0xFF); /* length MSB */
    frame[cmd_len + 2] = (uint8_t)(payload_len & 0xFF);        /* length LSB */
    memcpy(frame + cmd_len + 3, payload, payload_len);

    /* write() may return short: loop until the whole frame is sent. */
    size_t sent = 0;
    while (sent < frame_len) {
        ssize_t n = write(fd, frame + sent, frame_len - sent);
        if (n < 0) {
            if (errno == EINTR) {
                continue;
            }
            free(frame);
            return -1;
        }
        sent += (size_t)n;
    }
    free(frame);
    return 0;
}
```

Usage: configure the port in raw 8N1 mode with `termios`, then call `send_binary_data(fd, "AT+USOWB=0", payload, payload_len)`.

# Diagnostic tools

## Network status

`AT+UWSNST=<status_id>` reads one parameter of the Wi-Fi station network interface; `AT+UWSNST?` reads all of them.

| `status_id` | Parameter | Example |
|-------------|-----------|---------|
| 0 | Station IP address | `+UWSNST:0,192.168.1.179` |
| 1 | Subnet mask | `+UWSNST:1,255.255.255.0` |
| 2 | Default gateway | `+UWSNST:2,192.168.1.1` |
| 3 | Primary DNS server | `+UWSNST:3,192.168.1.1` |
| 4 | Secondary DNS server | `+UWSNST:4,0.0.0.0` |
| 5 | IPv6 link-local address | `+UWSNST:5,[fe80::56f8:2aff:fe13:6310]` |

`AT+UWSST=4` reads the RSSI of the connected Access Point, for example `+UWSST:4,-45`. A quick connectivity check is `AT+USOCR=6`, `AT+USOC=0,"8.8.8.8",53` (expect `+UESOC:0`) and `AT+USOCL=0`.

## Iperf performance testing

NORA-W36 supports Iperf version 2 as TCP or UDP, client or server. The implementation is experimental and may change between releases. Use [Iperf 2](https://sourceforge.net/projects/iperf2/files/) on the PC, see the [Iperf 2 manual](https://iperf2.sourceforge.io/iperf-manpage.html).

`AT+UDGI=<iperf_action>,<protocol_type>[,<role>,<port>,<report_interval>[,<time_boundary>,<ip_addr>[,<length>[,<bandwidth>[,<bidirectional>]]]]]`

| Parameter | Values |
|-----------|--------|
| `iperf_action` | `1` start, `2` stop |
| `protocol_type` | `1` TCP, `2` UDP |
| `role` | `1` server, `2` client |
| `port` | Port number |
| `report_interval` | Report interval |
| `time_boundary` | Test time, client only |
| `ip_addr` | Server address, client only |
| `length` | Packet size, 1..1460 (default 1460) |
| `bandwidth` | Bandwidth for UDP |
| `bidirectional` | `1` for a bidirectional test, client only. Start a server on both sides first |

**Module as server** (PC: `iperf -c <module_ip> -p 5001 -t 10`, add `-u -b 10M` for UDP):

| Nr| AT command | AT event | Description |
|---|------------|----------|-------------|
| 1 |`AT+UDGI=1,1,1,5001,1`| `+UEDGI:"TCP: Start TCP server!"` | Start a TCP server on port 5001 |
| 2 |`AT+UDGI=1,2,1,5002,1`| `+UEDGI:"UDP: Start UDP server!"` | Start a UDP server on port 5002 |

**Module as client** (PC: `iperf -s -p 5001`, add `-u` for UDP):

| Nr| AT command | AT event | Description |
|---|------------|----------|-------------|
| 1 |`AT+UDGI=1,1,2,5001,1,20,"192.168.0.41"`| `+UEDGI:"tcp_client_func: Send 1435 KBytes in 1000 ms, 11761 Kbits/sec"` | TCP test for 20 s |
| 2 |`AT+UDGI=1,2,2,5001,1,10,"192.168.0.41"`| `+UEDGI:"udp_client_func: Send 1024 KBytes in 1000 ms, 8388 Kbits/sec"` | UDP test for 10 s |

Stop a running test with `AT+UDGI=2,<protocol_type>`, for example `AT+UDGI=2,1`.

## Crash information

`AT+USYCI?` returns information about the last system crash. It is a non-official debug command.

```text
AT+USYCI?
+USYCI:"HwFault","timerEvent","3.5.0"
OK
```

`<crash_type>` is the type of fault (for example `HwFault`, `SwFault`, `WatchdogReset`), `<crash_reason>` the specific reason and the last parameter the firmware version when the crash occurred. If crashes continue, [open a Short Range support case on the u-blox portal](https://portal.u-blox.com/s/topic/0TO2p000000Hr7eGAC/short-range) or e-mail [support@u-blox.com](mailto:support@u-blox.com) with this output.

# Error codes

Extended error codes show why an AT command failed. They are for information only and may change between versions. The complete list for each release is in the [error code list](https://github.com/u-blox/u-connectXpress/blob/main/NORA-W36/3.5.0/error_codes.md).

- `AT+USYEE=1` enables extended error reporting: failed commands return `ERROR:<error_code>`.
- `AT+USYEC?` returns the error code of the last failed command: `+USYEC:<error_code>`.
- `AT+USOE?` returns the last socket error: `+USOE:<error_code>`.

```text
AT+USYEE=1
OK
AT+USPSWB=0,"abc"      // binary command sent in string form
ERROR:47
```

Error `47` is `U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD`: use the binary frame described in [Binary data](#binary-data).

## Common error codes (1-22)

| Code | Error name |
|------|------------|
| **1** | `U_ERROR_COMMON_BSD_ERROR` |
| **2** | `U_ERROR_COMMON_NOT_INITIALISED` |
| **3** | `U_ERROR_COMMON_NOT_IMPLEMENTED` |
| **4** | `U_ERROR_COMMON_NOT_SUPPORTED` |
| **5** | `U_ERROR_COMMON_INVALID_PARAMETER` |
| **6** | `U_ERROR_COMMON_NO_MEMORY` |
| **7** | `U_ERROR_COMMON_NOT_RESPONDING` |
| **8** | `U_ERROR_COMMON_PLATFORM` |
| **9** | `U_ERROR_COMMON_TIMEOUT` |
| **10** | `U_ERROR_COMMON_DEVICE_ERROR` |
| **11** | `U_ERROR_COMMON_NOT_FOUND` |
| **12** | `U_ERROR_COMMON_INVALID_ADDRESS` |
| **13** | `U_ERROR_COMMON_TEMPORARY_FAILURE` |
| **14** | `U_ERROR_COMMON_AUTHENTICATION_FAILURE` |
| **15** | `U_ERROR_COMMON_OPERATION_IN_PROGRESS` |
| **16** | `U_ERROR_COMMON_NOT_CONNECTED` |
| **17** | `U_ERROR_COMMON_LIMIT_REACHED` |
| **18** | `U_ERROR_COMMON_ALREADY_CREATED` |
| **19** | `U_ERROR_COMMON_END_OF_TRANSMISSION` |
| **19** | `U_ERROR_COMMON_REMOTE_CANCELLED_TRANSMISSION` |
| **20** | `U_ERROR_COMMON_NOT_CONFIGURED` |
| **21** | `U_ERROR_COMMON_INVALID_RESPONSE` |
| **22** | `U_ERROR_COMMON_UNKNOWN` |

## AT command error codes (31-51)

| Code | Error name |
|------|------------|
| **31** | `U_AT_STATUS_NOT_IMPLEMENTED` |
| **32** | `U_AT_STATUS_INVALID_COMMAND` |
| **33** | `U_AT_STATUS_INVALID_ARGUMENTS` |
| **34** | `U_AT_STATUS_INVALID_ARGUMENT_COUNT` |
| **35** | `U_AT_STATUS_INVALID_INT_ARG` |
| **36** | `U_AT_STATUS_INVALID_INT_RANGE` |
| **37** | `U_AT_STATUS_INVALID_STR_ARG` |
| **38** | `U_AT_STATUS_INVALID_STR_LENGTH` |
| **39** | `U_AT_STATUS_INVALID_ENUM_ARG` |
| **40** | `U_AT_STATUS_INVALID_IP_ADDR_ARG` |
| **41** | `U_AT_STATUS_INVALID_MAC_ADDR_ARG` |
| **42** | `U_AT_STATUS_INVALID_BD_ADDR_ARG` |
| **43** | `U_AT_STATUS_INVALID_BYTE_ARRAY_ARG` |
| **44** | `U_AT_STATUS_INVALID_BYTE_ARRAY_LENGTH` |
| **45** | `U_AT_STATUS_UNMATCHED_QUOTE` |
| **46** | `U_AT_STATUS_TIMEOUT` |
| **47** | `U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD` |
| **48** | `U_AT_STATUS_INVALID_ESCAPE_CODE` |
| **49** | `U_AT_STATUS_INVALID_CHARACTER` |
| **50** | `U_AT_STATUS_INVALID_INT_LIST_ARG` |
| **51** | `U_AT_STATUS_INVALID_INT_LIST_LENGTH` |

## Wi-Fi error codes (60-71)

| Code | Error name |
|------|------------|
| **60** | `U_ERROR_WIFI_AT` |
| **61** | `U_ERROR_WIFI_NOT_CONFIGURED` |
| **62** | `U_ERROR_WIFI_NOT_FOUND` |
| **63** | `U_ERROR_WIFI_INVALID_MODE` |
| **64** | `U_ERROR_WIFI_TEMPORARY_FAILURE` |
| **65** | `U_ERROR_WIFI_ALREADY_CONNECTED` |
| **66** | `U_ERROR_WIFI_ALREADY_CONNECTED_TO_SSID` |
| **67** | `U_ERROR_WIFI_DISCONNECTED` |
| **68** | `U_ERROR_WIFI_ALREADY_UP` |
| **69** | `U_ERROR_WIFI_AP_NOT_STARTED` |
| **70** | `U_ERROR_WIFI_IS_DOWN` |
| **71** | `U_ERROR_WIFI_ALREADY_STARTED` |

## Bluetooth GATT error codes (91-114)

| Code | Error name |
|------|------------|
| **91** | `U_PORT_GATT_STATUS_INVALID_HANDLE` |
| **92** | `U_PORT_GATT_STATUS_READ_NOT_PERMITTED` |
| **93** | `U_PORT_GATT_STATUS_WRITE_NOT_PERMITTED` |
| **94** | `U_PORT_GATT_STATUS_INVALID_PDU` |
| **95** | `U_PORT_GATT_STATUS_AUTHENTICATION` |
| **96** | `U_PORT_GATT_STATUS_NOT_SUPPORTED` |
| **97** | `U_PORT_GATT_STATUS_INVALID_OFFSET` |
| **98** | `U_PORT_GATT_STATUS_AUTHORIZATION` |
| **99** | `U_PORT_GATT_STATUS_PREPARE_QUEUE_FULL` |
| **100** | `U_PORT_GATT_STATUS_ATTRIBUTE_NOT_FOUND` |
| **101** | `U_PORT_GATT_STATUS_ATTRIBUTE_NOT_LONG` |
| **102** | `U_PORT_GATT_STATUS_ENCRYPTION_KEY_SIZE` |
| **103** | `U_PORT_GATT_STATUS_INVALID_ATTRIBUTE_LEN` |
| **104** | `U_PORT_GATT_STATUS_UNLIKELY` |
| **105** | `U_PORT_GATT_STATUS_INSUFFICIENT_ENCRYPTION` |
| **106** | `U_PORT_GATT_STATUS_UNSUPPORTED_GROUP_TYPE` |
| **107** | `U_PORT_GATT_STATUS_INSUFFICIENT_RESOURCES` |
| **108** | `U_PORT_GATT_STATUS_DB_OUT_OF_SYNC` |
| **109** | `U_PORT_GATT_STATUS_VALUE_NOT_ALLOWED` |
| **110** | `U_PORT_GATT_STATUS_WRITE_REQ_REJECTED` |
| **111** | `U_PORT_GATT_STATUS_CCC_IMPROPER_CONF` |
| **112** | `U_PORT_GATT_STATUS_PROCEDURE_IN_PROGRESS` |
| **113** | `U_PORT_GATT_STATUS_OUT_OF_RANGE` |
| **114** | `U_PORT_GATT_STATUS_UNKNOWN` |

## HTTP and socket error codes

| Code | Error name |
|------|------------|
| **160** | `U_ERROR_HTTP_HEADER_NOT_READ` |
| **180** | `U_ERROR_SOCKET_ALREADY_BOUND` |

Further HTTP and socket codes exist; read them with `AT+USYEC?` and `AT+USOE?`.

# Software update

The software is updated with the XMODEM-1K protocol over the UART, at baud rates up to 3000000 bps. There are two ways to start an update: with an AT command or with the bootloader. The firmware image is named `NORA-W36X-SW-3.5.0-<build>.bin` in the release archive.

![firmware](https://content.u-blox.com/sites/default/files/2024-02/firmware.png)

## Update software by AT command

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 |  Start the XMODEM protocol with an AT command  | `AT+USYFWUS=3000000` | |
| 2 | NORA-W36 is ready to receive the software with XMODEM or XMODEM-1K | `CCCCCCCCCCC...`  | |
| 3 | When the software has been downloaded the module restarts |  | `+STARTUP`   |
| 4 | Check the version of the software | `AT+GMR`| `"v3.5.0"` |

## Update software by bootloader

- Enter the bootloader command line mode with an AT command, or press `SWITCH_1` and `SWITCH_2` during startup or after reset.
- A command must be sent within 10 seconds in bootloader command line mode, otherwise the device reboots in normal mode. Enter `?` for the list of commands.
- The XMODEM protocol times out after 10 seconds without data.

| Nr| Instructions                              | AT command                        | Event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1a |  Enter the bootloader  | `AT+USYBL=115200` | |
| 1b |  Alternatively, press `SWITCH_1` and `SWITCH_2` during startup or reset|  | |
| 2 |  Wait for the `>` prompt  | |`>`|
| 3 |  Change the baud rate, up to 3000000 bps (optional)  | `r 3000000` | |
| 4 |  Start the XMODEM protocol  | `x`  | |
| 5 | NORA-W36 is ready to receive the software with XMODEM or XMODEM-1K |  | `CCCCCCCCCCC...` |
| 6    | Wait for the prompt that shows that the software has been downloaded | |  `>` |
| 7    | Restart the module |  `q`  | |
| 8 | Wait for the module to restart in AT mode |  | `+STARTUP`   |
| 9 | Check the version of the software | `AT+GMR`| `"v3.5.0"` |

## XMODEM host tool

The [u-blox/ucx-xmodem](https://github.com/u-blox/ucx-xmodem) repository contains an XMODEM-1K sender in Python ([xmodem.py](https://github.com/u-blox/ucx-xmodem/blob/main/xmodem.py), [README](https://github.com/u-blox/ucx-xmodem/blob/main/README_xmodem_python.md)) and in C for Windows ([xmodem.c](https://github.com/u-blox/ucx-xmodem/blob/main/xmodem.c), [README](https://github.com/u-blox/ucx-xmodem/blob/main/README_xmodem_c.md)). Both tools use the same arguments, send the AT command that starts the XMODEM mode and show the transfer progress.

```bash
# Python (pyserial)
pip install pyserial
python xmodem.py COM3 "NORA-W36X-SW-3.5.0-<build>.bin" 115200
python xmodem.py /dev/ttyUSB0 "NORA-W36X-SW-3.5.0-<build>.bin"  # Linux

# C (Windows, GCC/MinGW)
gcc -o xmodem xmodem.c -lkernel32
xmodem.exe COM3 "NORA-W36X-SW-3.5.0-<build>.bin" 115200
```

```python
from xmodem import ublox_firmware_update

success = ublox_firmware_update("COM3", "NORA-W36X-SW-3.5.0-<build>.bin", 3000000)
```

# Related information

- **[NORA-W36 Product Page](https://www.u-blox.com/en/product/nora-w36-series)** — product information, specifications and ordering details
- **[s-center 2](https://www.u-blox.com/en/product/s-center)** — configuration and development tool for u-blox modules
- **[NORA-W36 AT Command Manual](https://github.com/u-blox/u-connectXpress/blob/main/NORA-W36/3.5.0/at_commands.md)** — AT command reference
- **[u-blox/u-connectXpress](https://github.com/u-blox/u-connectXpress)** — firmware releases, AT command manuals and changelogs
- **[u-blox/sps](https://github.com/u-blox/sps)** — Serial Port Service protocol documentation and Python tools
- **[u-blox/ucx-xmodem](https://github.com/u-blox/ucx-xmodem)** — XMODEM-1K firmware update tools

# Contacts

u-blox AG
Address: Zürcherstrasse 68
8800 Thalwil
Switzerland

**Technical support:**
- Open a Short Range support case on the u-blox portal: [portal.u-blox.com → Short Range](https://portal.u-blox.com/s/topic/0TO2p000000Hr7eGAC/short-range)
- Or e-mail [support@u-blox.com](mailto:support@u-blox.com)

For general product information, visit [u-blox Support](https://www.u-blox.com/support).