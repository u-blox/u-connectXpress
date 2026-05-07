# **NORA-B27 u-connectXpress**

## Stand-alone Bluetooth LE modules

## <span style="color: gray;">User guide</span>

![short range](https://content.u-blox.com/sites/default/files/2024-02/shortrange.png)

This document provides an overview of the u-connectXpress software for u-blox short range modules
and describes how the products can be configured for Bluetooth Low Energy use cases.

![NORA-B27](https://content.u-blox.com/sites/default/files/2026-01/NORA-B27.png)

## Document information

| Title | NORA-B27 series u-connectXpress |
| :------------ | ---------------- |
| Subtitle    |  Stand-alone Bluetooth LE modules             |
| Document type | User guide |
| Version and date | 3.3.0 07-May-2026 |
| Disclosure restriction    |C1-Public |

**This document applies to the following products**
| Product name    |  Software version |
| :------------ | ---------------- |
| NORA-B27 series    |  3.3.0|

**Disclaimer**
u-blox or third parties may hold intellectual property rights in the products, names, logos, and designs included in this document. Copying, reproduction, or modification of this document or any part thereof is only permitted with the express written permission of u-blox. Disclosure to third parties is permitted for clearly public documents only.
The information contained herein is provided "as is" and u-blox assumes no liability for its use. No warranty, either express or implied, is given, including but not limited to, with respect to the accuracy, correctness, reliability, and fitness for a particular purpose of the information. This document may be revised by u-blox at any time without notice. For the most recent documents, visit [www.u-blox.com](https://www.u-blox.com).
Copyright © u-blox AG

# Overview

This document describes how to set up and use u-blox short range stand-alone modules with u-connectXpress software for NORA-B27. It explains the functionality of different u-blox short range stand-alone modules and includes examples that describe how to use the software in different environments with AT commands. The document is applicable for Bluetooth® Low Energy (LE) modules.
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
|**Remote device**    | A remote device in a wireless network connecting over the Bluetooth Low Energy interface supported in the module.|

## Bluetooth Low Energy modules

u-blox compact and powerful stand-alone Bluetooth Low Energy modules are designed for the development of Internet-of-Things (IoT) applications. NORA-B27 modules include an embedded Bluetooth stack and an application for wireless data transfer. The wireless support includes Bluetooth Low Energy 6.0 with Coded PHY.
The modules support point-to-point and point-to-multipoint configurations.
They are delivered with u-connectXpress software that provides support for u-blox Bluetooth LE Serial Port Service, Generic Attribute Profile (GATT) server and client, Bluetooth beacons, Peripheral and Central role - all configurable from a host by means of AT commands.

# Quick start guide

## Initial setup checklist

Before starting with NORA-B27 configuration, ensure the following setup is complete:

### Hardware setup

**Essential Hardware Connections:**

- **Power Supply (3.3V)** — connect regulated 3.3 V to VCC
- **Ground** — connect GND to your system reference
- **UART** — connect TX/RX between NORA-B27 and host

**Recommended:**

- **Reset Circuit** — wire the reset pin for hardware reset
- **Bootloader Recovery Switches** — install SW1 and SW2 for easy factory reset and bootloader access (see NORA-B27 SIM for details)

### Software setup

- **s-center 2** — download and install [s-center 2](https://www.u-blox.com/en/product/s-center)
- **Serial connection** — set the correct COM port and baud rate (115200 by default)
- **AT command testing** — verify communication with a basic `AT` command

#### UART configuration defaults

**Current NORA-B27 UART Settings:**

- **Baud Rate**: 115200 bps
- **Data Bits**: 8
- **Start Bits**: 1
- **Stop Bits**: 1
- **Parity**: None (8N1 format)
- **Hardware Flow Control**: **Disabled by default** (only TX/RX/GND required)

**Connection requirements:**

- Minimum: TX, RX, and GND only
- Recommended for higher baud rates: CTS/RTS for hardware flow control

### Initial verification commands

| Step | Command | Expected Response | Purpose |
|------|---------|------------------|---------|
| 1 | `AT` | `OK` | Test basic communication |
| 2 | `ATI` | Module information | Verify module identity |
| 3 | `AT+GMI` | `u-blox` | Check manufacturer |
| 4 | `AT+GMM` | `NORA-B27` | Check model |
| 5 | `AT+GMR` | Software version | Check firmware version |

## First connection examples


### Quick Bluetooth advertising


**Basic BLE Advertising Setup:**

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UBTALS=160,160` | Set legacy advertising parameters (100ms interval) |
| 2 | `AT+UBTAL` | Start legacy advertising |
| 3 | Device is now discoverable | Check with smartphone BLE scanner |

**Expected Result:** Module appears as "NORA-B27" in Bluetooth device scans


## Common quick start issues

### Communication problems

| Issue | Symptom | Solution |
|-------|---------|----------|
| No response to AT | Silent or garbled text | Check baud rate (115200), TX/RX/GND wiring (CTS/RTS optional) |
| `ERROR` responses | Commands not recognized | Check firmware version and command syntax |
| Connection timeouts | Commands hang | Check power supply stability, reset the module |


## Next steps

After successful quick start:
1. **Explore Bluetooth use cases** → [Bluetooth use cases](#bluetooth-use-cases)
2. **Understand data modes** → [Send and receive data](#send-and-receive-data)
3. **Advanced features** → [Bluetooth security configuration](#bluetooth-security)


# Key features


## Bluetooth GATT connection

NORA-B27 can function as a Peripheral unit, connecting to devices such as laptops, cellular phones, and tablets using the Generic Attribute Profile (GATT).

## Bluetooth SPS connection


The possibility of replacing serial cables with simple wireless connections is a key feature of u-blox modules. It allows system hosts to transfer data to one another over wireless Bluetooth connections that are established between u-blox modules in Central/Peripheral configuration.
Depending on the module capabilities, data from each host is transferred to local u-blox modules over a serial UART interface.
u-blox modules can, depending on module capabilities, be configured to automatically establish new connections and/or accept incoming connections using AT commands. For connected hosts, this means that physical serial cables can be replaced with more convenient wireless solutions.

NORA-B27 can function as a Peripheral unit, connecting to devices such as laptops, cellular phones, and tablets via the u-blox Serial Port Service (SPS).


# u-connectXpress software

## Operating modes

NORA-B27 operates in the following modes:

- **AT mode (default)**:  AT commands and data can be sent at the same time. Data is sent and received in AT commands and events - in string or binary mode
- **Transparent Mode (TM)**:  All data sent and received on the UART is connected to the remote device
Additionally, the module supports various low-power modes, which optimize power consumption regardless of the operating mode. See also Low power modes and Power consumption optimization.
Deep sleep is supported with the command `AT+UPMDS`, see AT command manual and Data sheet for more information.


## Changing operating modes

u-blox modules can be configured to start in any operating mode. Once up and running, the modules can be switched between most modes. The modes are changed with a command or escape sequence sent to the module:
- Switch from Command mode to Transparent mode using an AT command
- Switch from Transparent mode to command mode with an escape sequence.

The module is controlled using AT commands in (default) Command mode. In this mode, the host sends control and configuration commands and indicates when data is to be sent over the UART interface.

## NORA-B27 capabilities

|u-connectXpress Features |Capability in 3.3.0 |
|:-----------------|:------------------|
|Chipset | Nordic nRF54L05 |
|Radio | Bluetooth Low Energy 6.0 with Coded PHY (Long Range), Extended Advertising |
|Bluetooth Qualification | Declaration ID: [TBD](https://qualification.bluetooth.com) QDID: [TBD](https://qualification.bluetooth.com) Qualification date: TBD NORA-B27 listing date: TBD |
|BLE Peripheral connections|1 Central connected |
|BLE Link key storage    |30 Devices. The keys that are the least used are removed first when storage is full |
|Data transfer modes | Buffer Mode (event and read data), Direct Mode (data in event), Transparent mode (like serial port cable replacement). Buffer Mode is Default, Transparent mode only supports one link. Transparent Mode has highest throughput, then Direct Mode and then Buffer Mode |
|SPS MTU size | 244 bytes link MTU; up to 1000 bytes per AT string call (`AT+USPSWS`), 1000 bytes per AT binary call (`AT+USPSWB`) |


The table below summarises the major third-party components built into the firmware. The authoritative Software Bill of Materials is the CycloneDX `NORA-B27X-SBOM.json` shipped alongside the binary in each release archive.

|u-connectXpress software components |Versions in 3.3.0|
|:-----------------|:------------------|
|Nordic nRF Connect SDK including Bluetooth stack| See product release notes |
|Mbed TLS cryptographic algorithms| 3.6.4 https://github.com/Mbed-TLS/mbedtls/releases |




More information about the AT commands used in this use cases can be found in the [NORA-B27 AT command manual](https://github.com/u-blox/u-connectXpress/blob/main/NORA-B27/3.3.0/at_commands.md).


# AT command programming

This chapter covers the fundamental concepts of event-driven programming with NORA-B27, including AT command response handling, Unsolicited Result Code (URC) event management, and timing considerations that are essential before diving into specific protocol implementations.

## Event-driven programming fundamentals

## Understanding the event model

NORA-B27 operates on an **event-driven architecture** where the module continuously monitors for various conditions and notifies the host application through events. This approach enables efficient, asynchronous programming patterns.

**Key Concepts:**

- **Events are asynchronous** - They can occur at any time regardless of when commands are sent
- **Events require handling** - Your application must be prepared to process events when they arrive
- **Events provide real-time status** - They inform about connection status, data availability, errors, and more

## Event types overview

NORA-B27 generates several categories of events:

| Event Category | Purpose | Examples |
|----------------|---------|----------|
| **Connection Events** | Bluetooth connectivity | `+UEBTC`, `+UEBTDC`, `+UESPSC` |
| **Data Events** | Incoming data availability | `+UESPSDS` |
| **Status Events** | Module state changes | `+STARTUP` |
| **Error Events** | Problem notifications | `+UESPSDC`, `+UEBTDC` |
| **Security Events** | Authentication and bonding | `+UEBTB`, `+UEBTUC`, `+UEBTUPE` |

## AT command response handling

## Command response types

Every AT command generates predictable response patterns that your application must handle:

### Synchronous responses (immediate)

```bash

// Command sent:

AT+UBTBDL

// Immediate response:

+UBTBDL:AAAAAAAAAAAAp              // Bonded device 1
+UBTBDL:BBBBBBBBBBBBp              // Bonded device 2
OK
```

### Asynchronous responses (delayed)

```bash

// Command sent:

AT+UBTAL

// Immediate acknowledgment:

OK

// Later event (when Bluetooth connected):

+UEBTC:0,BBBBBBBBBBBBp
```

## Response parsing best practices

### Command response validation

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


## Command timing considerations

**Response Timeouts by Command Type:**

| Command Type | Typical Timeout | Max Timeout | Example |
|--------------|----------------|-------------|---------|
| Configuration | 1 second | 5 seconds | `AT+UBTM=1` |
| BLE Advertising | 10 seconds | 30 seconds | `AT+UBTAL` |
| Data Transfer | 5 seconds | 15 seconds | `AT+USPSWS=0,"data"` |
| Status Query | 3 seconds | 10 seconds | `AT+UBTCL` |

## Unsolicited result code (URC) event management

## Understanding URCs

**Unsolicited Result Codes (URCs)** are events generated by NORA-B27 without being prompted by a command. They provide real-time information about module status, incoming data, and connectivity changes.

**URC Characteristics:**

- **Unprompted** - Arrive without commands being sent
- **Time-critical** - Often require immediate handling
- **Context-dependent** - May require maintaining state information
- **Protocol-specific** - Different protocols generate different URCs

## Critical URC categories

### Connectivity URCs

```bash
+UEBTC:0,AAAAAAAAAAAAp             // Bluetooth connected
+UEBTDC:0        // Bluetooth disconnected
+UESPSC:0        // SPS connected
+UESPSDC:0       // SPS disconnected
```

### Data availability URCs

```bash
+UESPSDS:0,"SPS Data"              // SPS string data received
```

### Status change URCs

```bash
+STARTUP         // Module started/restarted
```

## URC handling strategies

### Strategy 1: event-driven state machine

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

### Strategy 2: data-driven processing

```bash

// Handle SPS data events immediately

if URC == "+UESPSDS:0,*":

- data = extract_data_from_urc()
- process_incoming_data(data)


if URC == "+UESPSDA:0,*":

- bytes_available = extract_count_from_urc()
- read_buffered_sps_data(bytes_available)

```

### Strategy 3: error recovery

```bash

// Handle error conditions

if URC == "+UESPSDC:0":

- log_error("SPS disconnected")
- attempt_reconnection()


if URC == "+UEBTDC:0":

- log_error("Bluetooth disconnected")
- enable_advertising()

```


# Bluetooth use cases

## Bluetooth GATT use cases

The following Bluetooth Low Energy use case, show some functionality to get started with GATT client and GATT server.

|u-connectXpress BLE default values | 3.3.0 |
|:----------------|:-----------------|
|BLE Mode default |**ON**, Peripheral (Mode = 2) |
|BLE Legacy Advertising default    |**OFF**, enable with `AT+UBTAL` |

The following examples use the MAC address below, this must be replaced by the real MAC address of the devices that are used.
- Peripheral MAC address: AAAAAAAAAAAA
- Central MAC address: BBBBBBBBBBB


### Bluetooth GATT server

![bt-gatt-server](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-server.png)
This use case configures NORA-B27 as a Peripheral device that operates as GATT server and sends notifications.

This configuration works in combination with a remote Central device that acts as a GATT client.



| Nr| Instructions                              | AT command                        | AT event              |
|---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled (**2: Peripheral**). If so jump to step 6.   | `AT+UBTM?`     |   `+UBTM:2`         |
| 2 | Enable Bluetooth **2: Peripheral** | `AT+UBTM=2` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-B27 to start | | `+STARTUP` |
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


Once the SPS link is up, exchange data with `AT+USPSWS` / `AT+USPSWB` (write) and `AT+USPSRS` / `AT+USPSRB` (read). See [string vs binary modes](#string-mode).

### Bluetooth SPS peripheral

![bt-sps-central](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-peripheral.png)

This use case configures NORA-B27 module as a Peripheral device that sends and receives data from another NORA-B27 module operating as a Central device. The communication between the two modules is facilitated using the proprietary [u-blox Serial Port Service](https://content.u-blox.com/sites/default/files/u-connectXpress-LowEnergySerialPortService_ProtocolSpec_UBX-16011192.pdf). It is also possible to connect to other devices that support the SPS protocol.
This use case configuration works with a remote Central device that supports SPS.



| Nr| Instructions                          | AT command  |  AT events |
|---|:---------------------------------------|:--------------------------------------|:--------------------|
| 1 | Check that Bluetooth Peripheral is enabled. (**2: Peripheral**). If so, jump to step 6   | `AT+UBTM?`     |   `+UBTM:2`         |
| 2 | Enable Bluetooth **2: Peripheral** | `AT+UBTM=2` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-B27 to startup | | `+STARTUP` |
| 6 | Enable SPS on Peripheral              | `AT+USPS=1`        | `OK` |
| 7 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 8 | Peripheral receives Incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 9 | Read MTU, maximum data size on both | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 10 | Read RSSI (optional)   | `AT+UBTRSS=0`     | `+UBTRSS:-52` |
| 11 | Central connects SPS (Peripheral receives connection)  |   | `+UESPSC:0` |
| 12 | SPS and Bluetooth link is down | `+UESPSDC:0` `+UEBTDC:0` |  |

Once the SPS link is up, exchange data with `AT+USPSWS` / `AT+USPSWB` (write) and `AT+USPSRS` / `AT+USPSRB` (read). See [string vs binary modes](#string-mode).



## Bluetooth security

Pairing establishes an encrypted link between two devices. Bonding stores the
exchanged keys so that the same peers can reconnect securely without repeating
the pairing flow. The relevant AT commands are:

- `AT+UBTPM=1` — allow incoming pairing requests
- `AT+UBTIOC=<cap>` — set the I/O capabilities used during pairing
- `AT+UBTBSM=<mode>` — set the minimum security mode required for bonding
- `AT+UBTBDL` — list bonded devices
- `AT+UBTUB=<bd_addr>` — delete a stored bond


### Bluetooth security responder

Bluetooth Security is disabled by default and must be configured and enabled before use.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled, (**2: Peripheral**), if so move to step 6   | `AT+UBTM?`     |   `+UBTM:2`         |
| 2 | Enable Bluetooth **2: Peripheral** | `AT+UBTM=2` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-B27 to startup | | `+STARTUP` |
| 6 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 7 | Set Bluetooth I/O Capabilities to Display Yes/No (2)   |          `AT+UBTIOC=2` |  |
| 8 | Set Only allow authenticated bonding with encrypted Bluetooth link (3)| `AT+UBTBSM=3` |  |
| 9 | Allow Pairing| `AT+UBTPM=1` |  |
| 10 | Bluetooth Connected event |  | `+UEBTC:0,AAAAAAAAAAAAp` |
| 11 | Bluetooth User Confirmation event, check the number on both devices, should be the same| | `+UEBTUC:AAAAAAAAAAAAp,786920` |
| 12 | Bluetooth User Confirmation, confirm with yes| `AT+UBTUC=AAAAAAAAAAAAp,1` |  |
| 13 | Bluetooth Bond success | | `+UEBTB:AAAAAAAAAAAAp,0` |
| 14 | Bluetooth Bonded Devices List (optional) | `AT+UBTBDL` | `+UBTBDL:AAAAAAAAAAAAp` |


# Power save use cases


## Deep sleep

The most efficient power level is Deep sleep which is almost like a power off, no radio communication is possible in this mode.

- To initiate Deep sleep mode, the host uses the AT command `AT+UPMDS`
- To wake up the module from Deep sleep mode, the host sets `GPIO_J9 to GND`
- After wake up, the module assumes the same state as it does after a reset


# Send and receive data

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
| **Buffered Mode** | Data stored until read | Data ready event triggered | Applications with event-driven processing | Higher |
| **Direct Mode** | Data delivered immediately | Immediate data delivery events | Real-time applications, streaming | Lower |

## When to use each data mode

## String mode - text and structured data

**Use string mode when:**
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

**Use binary mode when:**
- Transferring **files** (images, documents, firmware)
- Working with **binary protocols** (custom, proprietary)
- Data contains **null bytes** or control characters
- Need **full byte range** support (`0x00-0xFF`)
- **Data integrity** is critical

**Avoid binary mode when:**
- Only working with **simple text data**
- **Ease of debugging** is more important than functionality

**Example use cases:**
- File transfers: Images, PDFs, firmware updates
- Encrypted data transmission
- Custom binary protocols

## Transparent mode - maximum performance

**Use transparent mode when:**
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

NORA-B27 supports several modes for sending and receiving data:
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

To receive data without an event and read it out, the read mode can be changed to direct mode `AT+USPSRM=1`

## String mode


**SPS Receive data mode**

**Syntax**
`AT+USPSRM=<receive_mode>`
* 0: **Buffered mode**
  * `+UESPSDA` SPS Data Available event, default mode
* 1: **Direct string mode**
  * `+UESPSDS` - SPS Data String event


## SPS write string

**Syntax**
`AT+USPSWS=<conn_handle>,<string_data>`

Example to write SPS data
| Nr| Instructions                          | AT command | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write SPS data in string format size |    `AT+USPSWS=0,"Hello from NORA-B27"` | `OK` |


## SPS read string

**Syntax**
`AT+USPSRS=<connection_handle>,<length>`
`+USPSRS:<connection_handle>,<length>,<string_data>`

Example to read SPS data
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming SPS data     | | `+UESPSDA:0,19` |
| 2 | Reads incoming SPS data in string format |`AT+USPSRS=0,19` |   `+USPSRS:0,19,"Hello from NORA-B27"` |

## Binary mode

The binary mode should be used when binary content is transmitted, like files and binary protocols.

See [Binary data](#simple-binary-data-example) for more information about the format of the data.

> **Binary AT-command framing in one line.** Every binary command (`…B`) is followed **immediately** — no `,`, no space, no `\r` — by a 3-byte header `01 <lenMSB> <lenLSB>` and then the raw payload bytes. The `0x01` (SOH) IS the separator between the comma-separated parameter list and the binary block. Sending the same command in string form (with `,` and `"..."`) instead returns **`ERROR:47`** (`U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD`).


**SPS receive mode**

**Syntax**
`AT+USPSRM=<receive_mode>`
* 0: **Buffered mode**
  * `+UESPSDA` SPS Data Available event, default mode
* 2: **Direct binary mode**
  * `+UESPSDB` - SPS Data Binary event

See more information about [Binary Data](#simple-binary-data-example).


## SPS write binary

**Syntax**

`AT+USPSWB=<conn_handle><01><length_high><length_low><data>`

Where `<01>` is the start marker, `<length_high><length_low>` is the 2-byte data length, and `<data>` is your actual data.

> **This is a binary AT command.** The `<01><lenMSB><lenLSB><data>` block is sent **immediately** after the last comma-separated parameter — no `,`, no space, no `\r` between them. See [Binary data](#simple-binary-data-example). Sending it in string form returns `ERROR:47`.

**Example to write SPS data** — payload `Hello from NORA-B27` (19 bytes = `0x0013`):

```text
ascii :  A  T  +  U  S  P  S  W  B  =  0   │             │  H  e  l  l  o     f  r  o  m     NORA-B27
hex   : 41 54 2B 55 53 50 53 57 42 3D 30   │ 01 00 13    │  48 65 6C 6C 6F 20 66 72 6F 6D 20 …
                                            └─ SOH ─┼─ len ─┘
```

The textual short-hand `AT+USPSWB=0010013Hello from NORA-B27` is the same three header bytes printed as ASCII hex — not the on-wire form. Send the raw bytes.

## SPS read binary

**Syntax**
`AT+USPSRB=<conn_handle>,<length>`

**Response**

`+USPSRB:<conn_handle><01><length_high><length_low><data>`

> **Binary response.** The reply contains the 3-byte header (`01 <lenMSB> <lenLSB>`) followed by the raw payload bytes — no `,` between header and data. See [Binary data](#simple-binary-data-example).

**Example to read SPS data**
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming SPS data     | | `+UESPSDA:0,19` |
| 2 | Reads incoming SPS data in binary format |`AT+USPSRB=0,19` |   `+USPSRB:0` + `01 00 13` + `Hello from NORA-B27` (19 raw payload bytes) |

## Transparent mode overview

Transparent mode (TM) allows the NORA-B27 to act as a transparent bridge, forwarding all UART data directly to a remote device without AT command processing. This works similarly to Data mode in legacy u-blox short range products.

**Key Features:**
- Direct UART-to-remote data forwarding
- No AT command processing during transparent mode
- Escape sequence `+++` to return to AT command mode. Note that there should be no EOL after the escape
sequence
- Support for SPS (Bluetooth LE) connections

**Important Limitations:**
- Only **one active connection** allowed at a time
- Must establish connection before entering transparent mode
- All UART data is sent unmodified (no flow control indicators)

## Basic transparent mode

The `AT+UTM` command enters transparent mode on an existing connection.

### Basic transparent mode command syntax
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
Hello from NORA-B27!
[Data sent transparently to remote BLE device]
+++
OK
[Back in AT command mode]
```


### Escape sequence timing
- Send `+++` with **no line ending** (no CR/LF)
- Wait **1 second** before and after sending `+++`
- Module responds with `OK` when returning to AT mode


# Binary data

## What is binary data?

Binary data allows you to send raw bytes (like images, certificates, or any non-text data) through AT commands. This is useful when you need to transfer files, certificates, or binary content that cannot be represented as regular text.

## How binary data works

When sending binary data with NORA-B27, you need to follow a specific format that tells the module exactly how many bytes to expect.

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

- **Do** send binary data immediately after the AT command and parameters.
- **Do not** add a comma (`,`) before the binary data.
- **Do not** add a carriage return (`\r`) before the binary data.
- **Do not** add spaces or any other characters before the binary data.
- **Do not** add a hexadecimal escape (`\x`) before the binary data.

> **If you send a binary command in string form** (with `,"..."` instead of the SOH-framed block) the module replies with **`ERROR:47`** (`U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD`). That error means "this is a `…B` command — use the binary frame on this page."


## Simple binary data example

Let's send 2 bytes of data (`0xFF, 0xEE`) via SPS.

## Step-by-step breakdown:

1. **Your data**: `0xFF, 0xEE` (2 bytes)
2. **Calculate length**: 2 bytes = `0x0002` in hexadecimal
3. **Create header**: `0x01, 0x00, 0x02` (start marker + length)
4. **Complete command**: `AT+USPSWB=0` + header + data

## What you actually send:

```text
ascii :  A  T  +  U  S  P  S  W  B  =  0   │             │
hex   : 41 54 2B 55 53 50 53 57 42 3D 30   │ 01 00 02    │ FF EE
                                            └─ SOH ─┼─ len ─┘   ↑ payload (2 bytes)
```

**Explanation:**

- `AT+USPSWB=0` (11 ASCII bytes) = write to SPS connection 0
- `01` = SOH start marker
- `00 02` = length = 2 bytes (big-endian)
- `FF EE` = your 2 raw payload bytes

Note: **no comma, no `\r`** between `=0` and `01`. The textual short-hand `AT+USPSWB=0010002FFEE` is just the bytes printed as ASCII hex — not the on-wire form.

## Text message example

Let's send the text `Hello from NORA-B27` as binary data.

## Step-by-step calculation:

1. **Count characters**: `Hello from NORA-B27` = 19 characters = 19 bytes
2. **Convert to hex**: 19 = `0x0013` in hexadecimal
3. **Split into bytes**: `0x00` (high byte) and `0x13` (low byte)
4. **Create header**: `0x01, 0x00, 0x13`

## Complete command:

```text
ascii :  A  T  +  U  S  P  S  W  B  =  0   │             │  H  e  l  l  o     f  r  o  m     NORA-B27
hex   : 41 54 2B 55 53 50 53 57 42 3D 30   │ 01 00 13    │  48 65 6C 6C 6F 20 66 72 6F 6D 20 …
                                            └─ SOH ─┼─ len ─┘   ↑ 19 payload bytes
```

**When you receive data back, it includes the same header:**

```text
resp  :  +  U  S  P  S  R  B  :  0          │             │  H  e  l  l  o   …
hex   : 2B 55 53 50 53 52 42 3A 30          │ 01 00 13    │  48 65 6C 6C 6F …
```


## Programming examples

The three examples below are functionally identical: write the AT-command bytes, append the 3-byte binary header (`0x01`, length high, length low), append the payload, then send the whole buffer in one write to keep the framing intact. Open the serial port in raw, 8N1, no flow-control conversion, and **do not** terminate the command with `\r` or `\n` before the binary header.

## Python example

```python
def send_binary_data(serial_port, at_command: str, payload: bytes) -> None:
    """Send AT command + binary payload using the NORA-B27 3-byte header."""
    if len(payload) > 0xFFFF:
        raise ValueError("payload exceeds 65535-byte AT binary limit")
    header = b"\x01" + len(payload).to_bytes(2, "big")
    serial_port.write(at_command.encode("ascii") + header + payload)

# Example usage
with open("file.bin", "rb") as f:
    payload = f.read()
send_binary_data(serial_port, "AT+USPSWB=0", payload)
```

## C# example

```csharp
public static void SendBinaryData(SerialPort port, string atCommand, byte[] payload)
{
    if (payload.Length > 0xFFFF)
        throw new ArgumentException("payload exceeds 65535-byte AT binary limit");

    byte[] cmd = System.Text.Encoding.ASCII.GetBytes(atCommand);
    byte[] frame = new byte[cmd.Length + 3 + payload.Length];

    Buffer.BlockCopy(cmd, 0, frame, 0, cmd.Length);
    frame[cmd.Length]     = 0x01;                                   // start marker
    frame[cmd.Length + 1] = (byte)((payload.Length >> 8) & 0xFF);   // length MSB
    frame[cmd.Length + 2] = (byte)( payload.Length       & 0xFF);   // length LSB
    Buffer.BlockCopy(payload, 0, frame, cmd.Length + 3, payload.Length);

    port.Write(frame, 0, frame.Length);                             // single write
}

// Example usage
byte[] payload = File.ReadAllBytes("file.bin");
SendBinaryData(port, "AT+USPSWB=0", payload);
```

## C example (POSIX)

```c
#include <stdint.h>
#include <stddef.h>
#include <string.h>
#include <unistd.h>
#include <errno.h>

/* Returns 0 on success, -1 on error (errno set, or EMSGSIZE if too large). */
int send_binary_data(int fd, const char *at_command,
                     const uint8_t *payload, size_t payload_len)
{
    if (payload_len > 0xFFFF) { errno = EMSGSIZE; return -1; }

    size_t cmd_len   = strlen(at_command);
    size_t frame_len = cmd_len + 3 + payload_len;
    uint8_t *frame   = (uint8_t *)malloc(frame_len);
    if (!frame) { errno = ENOMEM; return -1; }

    memcpy(frame, at_command, cmd_len);
    frame[cmd_len]     = 0x01;                                /* start marker */
    frame[cmd_len + 1] = (uint8_t)((payload_len >> 8) & 0xFF);/* length MSB  */
    frame[cmd_len + 2] = (uint8_t)( payload_len       & 0xFF);/* length LSB  */
    memcpy(frame + cmd_len + 3, payload, payload_len);

    /* Loop until the full frame is written -- write() may return short. */
    size_t sent = 0;
    while (sent < frame_len) {
        ssize_t n = write(fd, frame + sent, frame_len - sent);
        if (n < 0) {
            if (errno == EINTR) continue;
            free(frame);
            return -1;
        }
        sent += (size_t)n;
    }
    free(frame);
    return 0;
}

/* Example usage:
 *   int fd = open("/dev/ttyUSB0", O_RDWR | O_NOCTTY);
 *   // ... configure termios for raw 8N1, no flow-control translation ...
 *   send_binary_data(fd, "AT+USPSWB=0", payload, payload_len);
 */
```

## Common use cases

Binary data is used in these NORA-B27 functions:

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





# Error codes

The Extended error codes provide essential debugging information to understand the reason for errors received during AT command execution. This section provides comprehensive error code documentation for immediate troubleshooting without requiring external references.

**Important Note**: Error codes should only be used for information and might change between versions in the future.

## Error code overview

NORA-B27 uses a structured error code system organized by functional categories:

| Category | Code Range | Description | Common Scenarios |
|----------|------------|-------------|------------------|
| **Common** | 1-22 | General system errors | Parameter validation, memory, timeouts |
| **AT Command** | 31-51 | AT command parsing errors | Invalid syntax, arguments, formatting |
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
AT+UBTM=99
ERROR:5
```

The error code `5` indicates `U_ERROR_COMMON_INVALID_PARAMETER` - the parameter value is out of valid range.


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


## Error code troubleshooting workflow

## Basic error diagnosis

**Step 1: Enable Extended Error Reporting**
```bash
AT+USYEE=1
OK
```

**Step 2: Execute Command and Observe Error**
```bash
AT+UBTAL
ERROR:95
```

**Step 3: Look Up Error Code**
- Error 95 = `U_PORT_GAP_STATUS_AUTHENTICATION_REQUIRED`
- Action: Complete authentication process

**Step 4: Apply Solution**
```bash
AT+UBTPM=1       // Enable pairing mode
AT+UBTIOC=2      // Set I/O capabilities
AT+UBTAL         // Restart advertising
OK
```

## Advanced error analysis

**For Bluetooth Advertising Issues:**
```bash
// Check last error
AT+USYEC?
+USYEC:95
OK

// Error 95 = Authentication required
// Complete authentication process
AT+UBTPM=1       // Enable pairing mode
AT+UBTIOC=2      // Set I/O capabilities
```

**For SPS Issues:**
```bash
// Check advertising status
AT+UBTAL?
+UBTAL:1
OK

// If not advertising, restart
AT+UBTAL         // Start advertising
```

## Error code integration with monitoring

## Automated error monitoring

**Enable Comprehensive Error Reporting:**
```bash
// Enable comprehensive error reporting for all commands
AT+USYEE=1

// Check errors periodically
AT+USYEC?        // Last general error
```

## Error code integration examples

**Bluetooth Connection with Error Handling:**
```bash
AT+UBTAL
OK
// Wait for connection
+UEBTC:0,BBBBBBBBBBBBp
// Check GATT if error
AT+USYEC?
+USYEC:91
// Error 91 = Invalid GATT handle
```

This comprehensive error code reference provides immediate debugging support without requiring external documentation, significantly enhancing the troubleshooting experience for NORA-B27 users.




# Software update

This use case shows what AT commands to send to start a software update.
There are two ways to start the software update:

- See more about the XMODEM protocol [here](https://en.wikipedia.org/wiki/XMODEM)

![firmware](https://content.u-blox.com/sites/default/files/2024-02/firmware.png)

## Update software by AT command

- Enter XMODEM mode for u-connect software update using serial port
- XMODEM-1K and baud rate up to 1000000 bps is supported.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 |  Start XMODEM protocol with AT command  | `AT+USYFWUS=1000000` | |
| 2 | Now NORA-B27 is ready to receive the software using the XMODEM or XMODEM-1K protocol | `CCCCCCCCCCC...`  | |
| 3 | When the software has been downloaded the module will restart |  `+STARTUP`   | |
| 4 | Check the version of the software | `AT+GMR`| `"4.0.0-041"` |

## Update software by bootloader

Consider the following points when updating the software using the bootloader:
- Enter the bootloader command line mode using serial port by AT command
- Press `SWITCH_1` and `SWITCH_2` during startup (or after reset)
- A command must be sent within 10 seconds when in bootloader command line mode. Otherwise, the device reboots in normal mode
- For the complete list of available commands, enter `?`
- An XMODEM protocol timeout is invoked after 10 seconds if nothing is received
- XMODEM-1K and baud rate up to 1000000 bps is supported

| Nr| Instructions                              | AT command                        | Event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1a |  Enter the bootloader  | `AT+USYBL=115200` | |
| 1b |  Alternatively, press `SWITCH_1` and `SWITCH_2` during startup or reset to enter the bootloader reset|  | |
| 2 |  Wait for the `>` prompt  | |`>`|
| 3 |  Change baud rate to up to 1000000 bps (optional)  | `r 1000000` | |
| 4 |  Start XMODEM protocol with the command `x`  | `x`  | |
| 5 | Now NORA-B27 is ready to receive the software using the XMODEM or XMODEM-1K protocol|  | `CCCCCCCCCCC...` |
| 6    | Wait for the prompt to indicate that the software has been downloaded successfully | |  `>` |
| 7    | Enter the `q` command to restart the module|  `q`  | |
| 8 | Wait for the prompt to display that the module has restarted in AT mode |  `+STARTUP`   | |
| 9 | Check the version of the software | `AT+GMR`| `"v3.3.0"` (matches the firmware version printed on the official release zip) |

## XMODEM protocol deep dive

XMODEM is a file transfer protocol used for reliable data transmission over serial connections. NORA-B27 supports both standard XMODEM (128-byte blocks) and XMODEM-1K (1024-byte blocks) for firmware updates.

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

Complete working XMODEM implementations for NORA-B27 firmware updates are provided in the appendices:

- **[Python XMODEM implementation](#python-xmodem-implementation)** — cross-platform Python
- **[C XMODEM implementation](#c-xmodem-implementation)** — native Windows C with COM port handling

**Key Features of Both Implementations:**
- **Hardware Validated**: Tested with real NORA-B27 modules for firmware updates
- **XMODEM-1K Protocol**: 1024-byte blocks with CRC-16 error detection
- **Robust Error Handling**: Automatic retries, timeout management, and recovery
- **Progress Tracking**: Real-time feedback during file transfers
- **NORA-B27 Integration**: Automated AT command sequence for firmware mode
- **High-Speed Support**: Up to 3Mbps baud rate for fast transfers

**Usage Examples:**
```bash
# Python implementation
python xmodem.py COM3 NORA-B27X-SW-3.3.0-<build>.bin 115200

# C implementation  
xmodem.exe COM3 NORA-B27X-SW-3.3.0-<build>.bin 115200
```

Both implementations use identical command-line interfaces and have been proven to work reliably with NORA-B27 hardware.

# Related information

## Documentation & resources

- **[NORA-B27 Product Page](https://www.u-blox.com/en/product/nora-b2-series)**
  Complete product information, specifications, and ordering details

- **[s-center 2 Webpage](https://www.u-blox.com/en/product/s-center)**
  Configuration and development tool for u-blox modules

- **[NORA-B27 AT Command Manual](https://github.com/u-blox/u-connectXpress/blob/main/NORA-B27/3.3.0/at_commands.md)**
  Comprehensive AT command reference and syntax guide

# Contacts

u-blox AG
Address: Zürcherstrasse 68
8800 Thalwil
Switzerland

**Technical support:**
- Open a Short Range support case on the u-blox portal: [portal.u-blox.com → Short Range](https://portal.u-blox.com/s/topic/0TO2p000000Hr7eGAC/short-range)
- Or e-mail [support@u-blox.com](mailto:support@u-blox.com)

For general product information, visit [u-blox Support](https://www.u-blox.com/support).

---

# Appendix

## Python XMODEM implementation

This Python XMODEM sender implementation has been tested with real NORA-B27 hardware for firmware updates.

The complete implementation is published in the [u-blox/ucx-xmodem](https://github.com/u-blox/ucx-xmodem) repository, file [xmodem.py](https://github.com/u-blox/ucx-xmodem/blob/main/xmodem.py).

**Key Features:**
- **Cross-platform**: Works on Windows, Linux, and macOS with pyserial
- **XMODEM-1K Protocol**: 1024-byte blocks with CRC-16 error detection
- **Robust Error Handling**: Automatic retries, timeout management, and recovery
- **Progress Tracking**: Real-time feedback during file transfers
- **NORA-B27 Integration**: Automated AT command sequence for firmware mode

**Requirements:**
```bash
pip install pyserial
```

**Usage:**
```bash
python xmodem.py <port> <firmware_file> [baud_rate]

# Examples:
python xmodem.py COM3 NORA-B27X-SW-3.3.0-<build>.bin
python xmodem.py COM3 NORA-B27X-SW-3.3.0-<build>.bin 115200
python xmodem.py /dev/ttyUSB0 NORA-B27X-SW-3.3.0-<build>.bin  # Linux
```

**Integration Example:**
```python
from xmodem import ublox_firmware_update

# Update firmware with default baud rate
success = ublox_firmware_update("COM3", "NORA-B27X-SW-3.3.0-<build>.bin")

# Update firmware with custom baud rate
success = ublox_firmware_update("COM3", "NORA-B27X-SW-3.3.0-<build>.bin", 3000000)
```

See [README_xmodem_python.md](https://github.com/u-blox/ucx-xmodem/blob/main/README_xmodem_python.md) for detailed documentation.

## C XMODEM implementation

This simplified C XMODEM sender provides the same functionality as the Python version with Windows-native serial port handling.

The complete implementation is published in the [u-blox/ucx-xmodem](https://github.com/u-blox/ucx-xmodem) repository, file [xmodem.c](https://github.com/u-blox/ucx-xmodem/blob/main/xmodem.c).

**Key Features:**
- **Native Windows API**: Direct serial port handling using kernel32
- **XMODEM-1K Protocol**: 1024-byte blocks with CRC-16 error detection
- **COM10+ Support**: Automatic handling of high-numbered COM ports
- **Robust Error Handling**: Automatic retries and timeout management
- **NORA-B27 Integration**: Automated AT command sequence for firmware mode

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
xmodem.exe COM3 NORA-B27X-SW-3.3.0-<build>.bin
xmodem.exe COM3 NORA-B27X-SW-3.3.0-<build>.bin 115200
xmodem.exe COM15 NORA-B27X-SW-3.3.0-<build>.bin 3000000  # High COM port
```

See [README_xmodem_c.md](https://github.com/u-blox/ucx-xmodem/blob/main/README_xmodem_c.md) for detailed documentation.
