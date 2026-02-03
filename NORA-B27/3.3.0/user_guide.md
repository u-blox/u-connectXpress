# **NORA-B27 u-connectXpress**

## Stand-alone Bluetooth LE modules

## <span style="color: gray;">User guide</span>

![short range](https://content.u-blox.com/sites/default/files/2024-02/shortrange.png)

This document provides an overview of the u-connectXpress software for u-blox short range modules
and describes how the products can be configured for Bluetooth Low Energy use cases.

![NORA-B27](https://content.u-blox.com/sites/default/files/2026-01/NORA-B27.png)

**Quick Navigation Guide for First-Time Users:**

- **Getting Started Fast** → [Quick Start Guide](#quick-start-guide) (quick setup)
- **Bluetooth Setup** → [Bluetooth GATT server](#bluetooth-gatt-server) (peripheral mode)
- **Data Transfer** → [Send and receive data](#send-and-receive-data) (modes explained)
- **Troubleshooting** → [Error codes](#error-codes) (when things go wrong)
- **AT Commands Index** → [Appendix A](#appendix) (command lookup)

## Document information

| Title | NORA-B27 series u-connectXpress |
| :------------ | ---------------- |
| Subtitle    |  Stand-alone Bluetooth LE modules             |
| Document type | User guide |
| Version and date |3.3.0 22-Jan-2026 |
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
|**Remote device**    | A remote device in a wireless network connecting over the Bluetooth Low Energy or Wi-Fi interfaces supported in the module.|

## Bluetooth Low Energy modules

u-blox compact and powerful stand-alone Bluetooth Low Energy modules are designed for the development of Internet-of-Things (IoT) applications. NORA-B27 modules include an embedded Bluetooth stack and an application for wireless data transfer. The wireless support includes Bluetooth Low Energy 6.0 with Coded PHY.
The modules support point-to-point and point-to-multipoint configurations.
They are delivered with u-connectXpress software that provides support for u-blox Bluetooth LE Serial Port Service, Generic Attribute Profile (GATT) server, Bluetooth beacons, Peripheral role - all configurable from a host by means of AT commands.

# Quick Start Guide

## Initial setup checklist

Before starting with NORA-B27 configuration, ensure the following setup is complete:

### Hardware setup

**Essential Hardware Connections:**

- ☐ **Power Supply (3.3V)** - Connect regulated 3.3V power to VCC pin
- ☐ **Ground Connection** - Connect GND pin to your system's ground reference
- ☐ **UART Interface** - Connect TX/RX pins between NORA-B27 and host system

**Recommended:**

- ☐ **Reset Circuit** - Wire reset pin for hardware reset capability
- ☐ **Bootloader Recovery Switches** - Install SW1 and SW2 for easy factory reset and bootloader access (see NORA-B27 SIM for details)

### Software setup

- ☐ **s-center 2 Installation**: Download and install [s-center 2](https://www.u-blox.com/en/product/s-center)
- ☐ **Serial Connection**: Configure correct COM port and baud rate (115200 default)
- ☐ **AT Command Testing**: Verify communication with basic `AT` command

#### UART configuration defaults

**Current NORA-B27 UART Settings:**

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
| 4 | `AT+GMM` | `NORA-B27` | Check model |
| 5 | `AT+GMR` | Software version | Check firmware version |

## First connection examples


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

    • Interval: 100ms         • Device name            • "NORA-B27"
    • Legacy mode             • BLE 6.0 compliant     • RSSI signal
    • Auto-connectable        • Low power mode        • Available services

```

**Basic BLE Advertising Setup:**

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UBTALS=160,160` | Set legacy advertising parameters (100ms interval) |
| 2 | `AT+UBTAL` | Start legacy advertising |
| 3 | Device is now discoverable | Check with smartphone BLE scanner |

**Expected Result:** Module appears as "NORA-B27" in Bluetooth device scans


## Common quick start issues

### Communication problems

**🔧 Hardware & Communication Troubleshooting:**

| Issue | Symptom | Solution |
|-------|---------|----------|
| 🔇 No response to AT | Silent or garbled text | ✅ Check baud rate (115200), TX/RX/GND wiring (CTS/RTS optional) |
|  `ERROR` responses | Commands not recognized | ✅ Check firmware version, command syntax |
|  Connection timeouts | Commands hang | ✅ Check power supply stability, reset module |


## Next steps

After successful quick start:
1. **Explore Bluetooth use cases** → [Bluetooth use cases](#bluetooth-use-cases)
2. **Understand data modes** → [Send and receive data](#send-and-receive-data)
3. **Advanced features** → [Bluetooth security configuration](#pairing-and-bonding)


# Key features

The possibility of replacing serial cables with simple wireless connections is a key feature of u-blox modules. It allows system hosts to transfer data to one another over wireless Bluetooth connections that are established between u-blox modules in Central/Peripheral configuration.
Depending on the module capabilities, data from each host is transferred to local u-blox modules over a serial UART interface.
u-blox modules can, depending on module capabilities, be configured to automatically establish new connections and/or accept incoming connections using AT commands. For connected hosts, this means that physical serial cables can be replaced with more convenient wireless solutions.

## Bluetooth GATT connection

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
NORA-B27 can function as a Peripheral unit, connecting to devices such as laptops, cellular phones, and tablets using the Generic Attribute Profile (GATT).

## Bluetooth SPS connection

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
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
|SPS MTU size | 244 bytes, 1000 bytes can be sent in AT command |


|u-connectXpress software components |Versions in 3.3.0|
|:-----------------|:------------------|
|Nordic nRF Connect SDK including Bluetooth stack| See product release notes |
|Mbed TLS cryptographic algorithms| 3.6.4 https://github.com/Mbed-TLS/mbedtls/releases |




More information about the AT commands used in this use cases can be found in the [NORA-B27 AT command manual](https://www.u-blox.com/en/sho-online-documentation/nora-b27/at-manual).


# AT Command Programming

This chapter covers the fundamental concepts of AT command programming with NORA-B27, including command response handling, event management, and timing considerations that are essential before diving into specific protocol implementations.


This chapter covers the fundamental concepts of event-driven programming with NORA-B27, including AT command response handling, Unsolicited Result Code (URC) event management, and data flow fundamentals that are essential before diving into specific protocol implementations.

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

#### Synchronous responses (immediate)

```bash

// Command sent:

AT+UBTBDL

// Immediate response:

+UBTBDL:AAAAAAAAAAAAp              // Bonded device 1
+UBTBDL:BBBBBBBBBBBBp              // Bonded device 2
OK
```

#### Asynchronous responses (delayed)

```bash

// Command sent:

AT+UBTAL

// Immediate acknowledgment:

OK

// Later event (when Bluetooth connected):

+UEBTC:0,BBBBBBBBBBBBp
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


## Command timing considerations

**Response Timeouts by Command Type:**

| Command Type | Typical Timeout | Max Timeout | Example |
|--------------|----------------|-------------|---------|
| Configuration | 1 second | 5 seconds | `AT+UBTM=1` |
| BLE Advertising | 10 seconds | 30 seconds | `AT+UBTAL` |
| Data Transfer | 5 seconds | 15 seconds | `AT+USPSWS=0,"data"` |
| Status Query | 3 seconds | 10 seconds | `AT+UBTCL` |

## Unsolicited result code (URC) event management

## Understanding urcs

**Unsolicited Result Codes (URCs)** are events generated by NORA-B27 without being prompted by a command. They provide real-time information about module status, incoming data, and connectivity changes.

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
+UESPSC:0        // SPS connected
+UESPSDC:0       // SPS disconnected
```

#### Data availability urcs

```bash
+UESPSDS:0,"SPS Data"              // SPS string data received
```

#### Status change urcs

```bash
+STARTUP         // Module started/restarted
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

// Handle SPS data events immediately

if URC == "+UESPSDS:0,*":

- data = extract_data_from_urc()
- process_incoming_data(data)


if URC == "+UESPSDA:0,*":

- bytes_available = extract_count_from_urc()
- read_buffered_sps_data(bytes_available)

```

#### Strategy 3: error recovery

```bash

// Handle error conditions

if URC == "+UESPSDC:0":

- log_error("SPS disconnected")
- attempt_reconnection()


if URC == "+UEBTDC:0":

- log_error("Bluetooth disconnected")
- enable_advertising()

```


# Data Handling and Processing

This chapter covers advanced data handling concepts, event processing patterns, and practical implementation strategies for building robust NORA-B27 applications.

## Data flow fundamentals

## Data mode overview

NORA-B27 supports multiple data handling modes, each optimized for different use cases:

| Data Mode | Behavior | Event Type | Best For |
|-----------|----------|------------|----------|
| **String Mode** | Text data only | `+UESPSDS` | JSON, XML, sensor readings |
| **Binary Mode** | All data types | `+UESPSDB` | Files, certificates, images |
| **Buffered Mode** | Store until read | `+UESPSDA` | Event-driven applications |
| **Direct Mode** | Immediate delivery | `+UESPSDS`/`+UESPSDB` | Real-time applications |
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

+UESPSDA:0,256            // 256 bytes available on SPS connection 0

// Host reads data:

AT+USPSRB=0,256
+USPSRB:0,256,"actual data content here..."
OK
```

#### Direct mode flow

```bash

// Data arrives → immediately delivered

+UESPSDS:0,"immediate data"         // SPS string data delivered directly

// No additional read command needed

```

## Protocol-specific event patterns

## Event categories


#### Bluetooth SPS events

```bash

// SPS connection sequence:

+UESPSC:0        // SPS connected
+UESPSDS:0,"Hello"       // String data received
+UESPSDA:0,64            // Binary data available
+UESPSDC:0       // SPS disconnected
```


## Event processing best practices

## Event handler design patterns

#### Pattern 1: central event dispatcher

```pseudocode
function handle_event(event_string):

- if event_string.startswith("+UEBTC"):
- handle_bluetooth_connected(event_string)
- elif event_string.startswith("+UESPSDS"):
- handle_sps_data(event_string)
- elif event_string.startswith("+STARTUP"):
- handle_module_startup()

```

#### Pattern 2: state-based processing

```pseudocode
function process_event(event, current_state):

- switch current_state:
- case CONNECTING:
- if event == "+UESPSC:0":
- transition_to_state(CONNECTED)
- case CONNECTED:
- if event.startswith("+UESPSDA"):
- handle_sps_data_available(event)

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

// Track Bluetooth connection state

connection_states = {
    "bluetooth": "DISCONNECTED",
    "sps": "DISCONNECTED"
}

// Update states based on events

function update_connection_state(event):

- if "+UEBTC" in event:
- connection_states["bluetooth"] = "CONNECTED"
- elif "+UEBTDC" in event:
- connection_states["bluetooth"] = "DISCONNECTED"
- elif "+UESPSC" in event:
- connection_states["sps"] = "CONNECTED"
-                // ... etc

```

## Data collection pattern

```bash

// Collect SPS data

data_sources = {
    "sps_0": []
}

function handle_data_event(event):

- if "+UESPSDS:0" in event:
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
```

This foundation in event-driven programming and data handling prepares you for implementing specific protocol use cases covered in subsequent chapters. Understanding these fundamentals is crucial for building robust IoT applications with NORA-B27.

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

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
![bt-gatt-server](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-server.png)
This use case configures NORA-B27 as a Peripheral device that operates as GATT server and sends notifications.

This configuration works in combination with a remote Central device that acts as a GATT client.



| Nr| Instructions                              | AT command                        | AT event              |
|---|:-------------------------------------------|:-----------------------------------|:------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled **2: Peripheral** and **3: Central and Peripheral**. If so jump to step 6.   | `AT+UBTM?`     |   `+UBTM:2` or `+UBTM:3`         |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
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


### Bluetooth SPS peripheral

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
![bt-sps-central](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-peripheral.png)
This use case configures NORA-B27 module as a Peripheral device that sends and receives data from another NORA-B27 module operating as a Central device. The communication between the two modules is facilitated using the proprietary [u-blox Serial Port Service](https://content.u-blox.com/sites/default/files/u-connectXpress-LowEnergySerialPortService_ProtocolSpec_UBX-16011192.pdf). It is also possible to connect to other devices that support the SPS protocol.
This use case configuration works with a remote Central device that supports SPS.



| Nr| Instructions                          | AT command  |  AT events |
|---|:---------------------------------------|:--------------------------------------|:--------------------|
| 1 | Check that Bluetooth Peripheral is enabled. **2: Peripheral** and **3: Central and Peripheral**. If so, jump to step 6   | `AT+UBTM?`     |   `+UBTM:2` or `+UBTM:3`         |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
| 3 | Store command                         | `AT&W`          | `OK` |
| 4 | Restart                               | `AT+CPWROFF`    | `OK` |
| 5 | Wait for NORA-B27 to startup | | `+STARTUP` |
| 6 | Enable SPS on Peripheral              | `AT+USPS=1`        | `OK` |
| 7 | Enable Legacy Advertising    | `AT+UBTAL` | `OK` |
| 8 | Peripheral receives Incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 9 | Read MTU, maximum data size on both | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 10 | Read RSSI (optional)   | `AT+UBTRSS=0`     | `+UBTRSS:-52` |
| 11 | Central connects SPS (Peripheral receives connection)  |   | `+UESPSC:0` |
| 12 | It is now possible to send and receive SPS data in [String](#string-mode) or  [Binary](#binary-mode) mode |  |  |
| 13 | SPS and Bluetooth link is down | `+UESPSDC:0` `+UEBTDC:0` |  |


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


### Bluetooth security responder

![ble](https://content.u-blox.com/sites/default/files/2024-04/u-blox-bluetooth.png)
Bluetooth Security is disabled by default and must be configured and enabled before use.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 | Check that Bluetooth Peripheral is enabled, **2: Peripheral** or **3: Central and Peripheral**, if so move to step 6   | `AT+UBTM?`     |   `+UBTM:2` or `+UBTM:3`         |
| 2 | Enable Bluetooth **2: Peripheral** or **3: Central and Peripheral** | `AT+UBTM=2` or `AT+UBTM=3` | `OK` |
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

NORA-B27 provides multiple data transmission modes optimized for different use cases and performance requirements. Understanding when to use each mode is crucial for optimal application performance and reliability.

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
`AT+USPSRS=<socket_handle>,<length>`
`+USPSRS:<socket_handle>,<length>,<string_data>`

Example to read SPS data
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming SPS data     | | `+UESPSDA:0,19` |
| 2 | Reads incoming SPS data in string format |`AT+USPSRS=0,19` |   `+USPSRS:0,19,"Hello from NORA-B27"` |

## Binary mode

The binary mode should be used when binary content is transmitted, like files and binary protocols.

See [Binary data](#simple-binary-data-example) for more information about the format of the data.


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


**Example to write SPS data**
| Nr| Instructions                          | AT command | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write SPS data in binary format size |    `AT+USPSWB=0010013Hello from NORA-B27` | `OK` |

## SPS read binary

**Syntax**
`AT+USPSRB=<conn_handle>,<length>`

**Response**

`+USPSRB:<conn_handle><01><length_high><length_low><data>`


**Example to read SPS data**
| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Incoming SPS data     | | `+UESPSDA:0,19` |
| 2 | Reads incoming SPS data in binary format |`AT+USPSRB=0,19` |   `+USPSRB:0010013Hello from NORA-B27` |

## Transparent mode overview

Transparent mode (TM) allows the NORA-B27 to act as a transparent bridge, forwarding all UART data directly to a remote device without AT command processing. This works similarly to Data mode in legacy u-blox short range products.

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

   // gatt_client

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

- ✅ **DO**: Send binary data immediately after the AT command and parameters
-  **DON'T**: Add comma (`,`) before binary data
-  **DON'T**: Add carriage return (`\r`) before binary data
-  **DON'T**: Add any spaces or other characters before binary data
-  **DON'T**: Add hexadecimal escape (`\x`) before binary data


## Simple binary data example

Let's send 2 bytes of data (`0xFF, 0xEE`) via SPS.

## Step-by-step breakdown:

1. **Your data**: `0xFF, 0xEE` (2 bytes)
2. **Calculate length**: 2 bytes = `0x0002` in hexadecimal
3. **Create header**: `0x01, 0x00, 0x02` (start marker + length)
4. **Complete command**: `AT+USPSWB=0` + header + data

## What you actually send:

```
AT+USPSWB=0010002FFEE
```

**Explanation:**
- `AT+USPSWB=0` = Write to SPS connection 0
- `01` = Start marker
- `00` = Length high byte (0)
- `02` = Length low byte (2)
- `FFEE` = Your 2 bytes of actual data (binary bytes 0xFF, 0xEE)

## Text message example

Let's send the text `Hello from NORA-B27` as binary data.

## Step-by-step calculation:

1. **Count characters**: `Hello from NORA-B27` = 19 characters = 19 bytes
2. **Convert to hex**: 19 = `0x0013` in hexadecimal
3. **Split into bytes**: `0x00` (high byte) and `0x13` (low byte)
4. **Create header**: `0x01, 0x00, 0x13`

## Complete command:

```
AT+USPSWB=0010013Hello from NORA-B27
```

**When you receive data back, it includes the same header:**
```
+USPSRB:0010013Hello from NORA-B27
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
- XMODEM-1K and baud rate up to 3 Mbps is supported.

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 |  Start XMODEM protocol with AT command  | `AT+USYFWUS=3000000` | |
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
- XMODEM-1K and baud rate up to 3 Mbps is supported

| Nr| Instructions                              | AT command                        | Event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1a |  Enter the bootloader  | `AT+USYBL=115200` | |
| 1b |  Alternatively, press `SWITCH_1` and `SWITCH_2` during startup or reset to enter the bootloader reset|  | |
| 2 |  Wait for the `>` prompt  | |`>`|
| 3 |  Change baud rate to up to 3 Mbit/s (optional)  | `r 3000000` | |
| 4 |  Start XMODEM protocol with the command `x`  | `x`  | |
| 5 | Now NORA-B27 is ready to receive the software using the XMODEM or XMODEM-1K protocol|  | `CCCCCCCCCCC...` |
| 6    | Wait for the prompt to indicate that the software has been downloaded successfully | |  `>` |
| 7    | Enter the `q` command to restart the module|  `q`  | |
| 8 | Wait for the prompt to display that the module has restarted in AT mode |  `+STARTUP`   | |
| 9 | Check the version of the software | `AT+GMR`| `"3.0.0-041"` |

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

- **[Appendix C.1: Python XMODEM Implementation](#c1-python-xmodem-implementation)** - Complete Python implementation with cross-platform support
- **[Appendix C.2: C XMODEM Implementation](#c2-c-xmodem-implementation)** - Native Windows C implementation with COM port handling

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
python xmodem.py COM3 NORA-B27X-SW-3.1.0-150.bin 115200

# C implementation  
xmodem.exe COM3 NORA-B27X-SW-3.1.0-150.bin 115200
```

Both implementations use identical command-line interfaces and have been proven to work reliably with NORA-B27 hardware.

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

### NORA-B27 specific implementation

**Firmware Update Process:**
1. **AT Command Mode**: Send `AT+USYFWUS=3000000` to enter XMODEM mode
2. **Protocol Detection**: NORA-B27 sends 'C' characters requesting CRC mode
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

- **[NORA-B27 Product Page](https://www.u-blox.com/en/product/NORA-B27-series)**
  Complete product information, specifications, and ordering details

- **[s-center 2 Webpage](https://www.u-blox.com/en/product/s-center)**
  Configuration and development tool for u-blox modules

- **[NORA-B27 AT Command Manual](https://www.u-blox.com/en/sho-online-documentation/NORA-B27/at-manual)**
  Comprehensive AT command reference and syntax guide

# Contacts

u-blox AG
Address: Zürcherstrasse 68
8800 Thalwil
Switzerland
For further support and contact information, visit us at **[u-blox Support](https://www.u-blox.com/support)**.

---

# Appendix



## Bluetooth commands

### BLE advertising commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UBTALS` | BLE Advertising Parameters | [](#bluetooth-advertise) |
| `AT+UBTAL` | BLE Advertising Start | [](#bluetooth-advertise) |
| `AT+UBTALD` | BLE Advertising Stop | [](#bluetooth-advertise) |


### BLE SPS commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USPSWS` | SPS Write String | [](#string-mode) |
| `AT+USPSWB` | SPS Write Binary | [](#binary-mode) |
| `AT+USPSRS` | SPS Read String | [](#string-mode) |
| `AT+USPSRB` | SPS Read Binary | [](#binary-mode) |


## System and diagnostic commands

### Power management

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+CPWROFF` | Module Reset/Power Off | Multiple sections |


### Error handling

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+USYEC` | System Extended Error Code | [](#query-last-error-code) |
| `AT+USYEE` | System Extended Errors Enable | [](#socket-error-codes-180) |

### Data mode commands

| Command | Purpose | Section |
|---------|---------|---------|
| `AT+UTM` | Transparent Mode | [](#basic-transparent-mode) |
| `ATE0/ATE1` | Command Echo Control | [](#wi-fi-tcp-client) |
| `AT&W` | Store Configuration (use with AT+CPWROFF) | Multiple sections |
| `+++` | Escape Sequence (Exit Transparent Mode) | [](#basic-transparent-mode) |


// Appendix B: Enhanced Debugging and Visual Reference Guide

This appendix provides visual troubleshooting aids, standardized code examples, and enhanced debugging techniques for optimal NORA-B27 implementation and troubleshooting.

## Visual status indicators and LED patterns

### NORA-B27 LED status indicators

**Official LED Patterns (from NORA-B27 Datasheet):**

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
   AT+UBTAL (Start advertising)
        ↓
🟣 Magenta (Advertising/Connecting)
        ↓
🔵 Blue (Connected)
```

**Troubleshooting with LEDs:**
- **Stuck in Magenta**: Check advertising parameters or remote device
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
AT+UBTM=<mode>
```

**Parameters:**
- `mode`: Bluetooth mode (2 = Peripheral, 3 = Central+Peripheral)

**Response:**
```bash
OK
```

**Examples:**
```bash
// Basic usage
AT+UBTM=2
OK

// Error case
AT+UBTM=99
ERROR:5          // U_ERROR_COMMON_INVALID_PARAMETER
```

**Notes:** Mode changes require module restart to take effect



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


This enhanced visual reference guide provides immediate troubleshooting support with visual indicators, standardized examples, and copy-paste ready command sequences for efficient NORA-B27 development and deployment.

## C.1 Python XMODEM implementation

This Python XMODEM sender implementation has been tested with real NORA-B27 hardware for firmware updates.

The complete implementation is provided in the accompanying `xmodem/xmodem.py` file.

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
python xmodem.py COM3 NORA-B27X-SW-3.1.0-150.bin
python xmodem.py COM3 NORA-B27X-SW-3.1.0-150.bin 115200
python xmodem.py /dev/ttyUSB0 NORA-B27X-SW-3.1.0-150.bin  # Linux
```

**Integration Example:**
```python
from xmodem import ublox_firmware_update

# Update firmware with default baud rate
success = ublox_firmware_update("COM3", "NORA-B27X-SW-3.1.0-150.bin")

# Update firmware with custom baud rate
success = ublox_firmware_update("COM3", "NORA-B27X-SW-3.1.0-150.bin", 3000000)
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
xmodem.exe COM3 NORA-B27X-SW-3.1.0-150.bin
xmodem.exe COM3 NORA-B27X-SW-3.1.0-150.bin 115200
xmodem.exe COM15 NORA-B27X-SW-3.1.0-150.bin 3000000  # High COM port
```

See the `xmodem/README_xmodem_c.md` file for detailed documentation.
