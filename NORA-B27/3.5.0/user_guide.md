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
| Version and date | 3.5.0 19-Oct-2026 |
| Disclosure restriction    |C1-Public |

**This document applies to the following products**
| Product name    |  Software version |
| :------------ | ---------------- |
| NORA-B27 series    |  3.5.0|

**Disclaimer**
u-blox or third parties may hold intellectual property rights in the products, names, logos, and designs included in this document. Copying, reproduction, or modification of this document or any part thereof is only permitted with the express written permission of u-blox. Disclosure to third parties is permitted for clearly public documents only.
The information contained herein is provided "as is" and u-blox assumes no liability for its use. No warranty, either express or implied, is given, including but not limited to, with respect to the accuracy, correctness, reliability, and fitness for a particular purpose of the information. This document may be revised by u-blox at any time without notice. For the most recent documents, visit [www.u-blox.com](https://www.u-blox.com).
Copyright © u-blox AG

# Overview

This document describes how to set up and use u-blox short range stand-alone modules with u-connectXpress software for NORA-B27. It includes AT command examples for the supported use cases. The document is applicable for Bluetooth® Low Energy (LE) modules.
Several u-blox short range stand-alone modules support open software variants; see the system integration manuals for the available options.
For older generation modules like ODIN-W2, NINA-W15 and ANNA-B1, the [u-connectXpress user guide](https://www.u-blox.com/docs/UBX-16024251) describes the functionality of these modules.

## What's new in 3.5.0

For the complete list of fixes and known limitations see the
[CHANGELOG-NORA-B27.md](https://github.com/u-blox/u-connectXpress/blob/main/NORA-B27/CHANGELOG-NORA-B27.md).

- **Advertising (since 3.3.0)** — `AT+UBTAES` sets the interval of extended advertisements, `AT+UBTADL` and `AT+UBTADE` support non-connectable advertising, and the identity address is returned as soon as it is available for privacy peers. See [Advertising options](#advertising-options).
- **Host Wakeup pin** — `AT+USYHWP` configures the Host Wakeup pin to indicate the transparent mode connection status. See [Transparent mode](#transparent-mode-overview).
- **Stability fixes** — URCs cut in half at high throughput (for example `+UESODS`) no longer lose payload bytes on the host.
- **SPS and Bluetooth fixes** — An SPS client with flow control waits for the server credit notification, an assert on disconnect while the credit timer runs and a credit calculation overflow are fixed, an early MTU exchange no longer leaves SPS at MTU 23, and a race while ATT is torn down is fixed.

## Product description

u-blox modules are developed for integration into a vast range of devices that demand a high level of reliability, such as those that are typically used in industrial and medical applications.
These professional grade modules operate over an extended temperature range and are approved for radio type application products in many countries.

| Concept             | Definition |
| ------------------ | :------------ |
|**Host**                |In this document, a host refers to the device connected to a u-blox short range stand-alone module through any of the available physical interfaces. In a real application, the host is typically a microcontroller Unit (MCU) running a customer specific application. |
|**Module**               | In this document, module refers to a u-blox stand-alone module running the u-connectXpress software. |
|**Remote device**    | A remote device in a wireless network connecting over the Bluetooth Low Energy interface supported in the module.|

NORA-B27 modules include an embedded Bluetooth stack and an application for wireless data transfer. The wireless support includes Bluetooth Low Energy 6.0 with Coded PHY.
u-connectXpress provides the u-blox Bluetooth LE Serial Port Service (SPS), Generic Attribute Profile (GATT) server and Bluetooth beacons. All features are configured from a host with AT commands.

# Quick start guide

## Initial setup checklist

### Hardware setup

- **Power and ground** — connect power as described in the NORA-B27 system integration manual.
- **UART** — connect TX/RX/GND between NORA-B27 and the host. Add CTS/RTS for hardware flow control at higher baud rates.
- **Reset and bootloader switches** (recommended) — wire the reset pin and `SWITCH_1`/`SWITCH_2` for hardware reset and bootloader access, see [Update software by bootloader](#update-software-by-bootloader).

### Software setup

Install [s-center 2](https://www.u-blox.com/en/product/s-center) or any serial terminal and open the module's COM port. The UART defaults are 115200 bps, 8 data bits, no parity, 1 stop bit (8N1), and hardware flow control **disabled**.

### Initial verification commands

| Step | Command | Expected Response |
|------|---------|------------------|
| 1 | `AT` | `OK` |
| 2 | `ATI` | Module information |
| 3 | `AT+GMI` | `u-blox` |
| 4 | `AT+GMM` | `NORA-B27` |
| 5 | `AT+GMR` | Software version |

## First connection examples

### Quick Bluetooth advertising

| Step | Command | Description |
|------|---------|-------------|
| 1 | `AT+UBTALS=160,160` | Set legacy advertising interval (160 × 0.625 ms = 100 ms) |
| 2 | `AT+UBTAL` | Start legacy advertising |

The module is now discoverable as "NORA-B27" in a Bluetooth scanner.

# u-connectXpress software

## Operating modes

NORA-B27 operates in the following modes:

- **AT mode (default)**: AT commands and data can be sent at the same time. Data is sent and received in AT commands and events, in string or binary mode.
- **Transparent Mode (TM)**: All data sent and received on the UART is connected to the remote device.

The low power modes are independent of the operating mode, see [Power save use cases](#power-save-use-cases).

## Changing operating modes

The module starts in AT (command) mode. Switch to transparent mode with an AT command (`AT+UTM`) and back to command mode with the escape sequence `+++`, see [Transparent mode](#transparent-mode-overview).

## NORA-B27 capabilities

|u-connectXpress Features |Capability in 3.5.0 |
|:-----------------|:------------------|
|Chipset | Nordic nRF54L05 |
|Radio | Bluetooth Low Energy 6.0 with Coded PHY (Long Range), Extended Advertising |
|Bluetooth Qualification | Declaration ID: [TBD](https://qualification.bluetooth.com) QDID: [TBD](https://qualification.bluetooth.com) Qualification date: TBD NORA-B27 listing date: TBD |
|BLE Peripheral connections|1 Central connected |
|BLE Link key storage    |10 Devices. The keys that are the least used are removed first when storage is full |
|Data transfer modes | Buffer Mode (event and read data), Direct Mode (data in event), Transparent mode (like serial port cable replacement). Buffer Mode is Default, Transparent mode only supports one link. Transparent Mode has highest throughput, then Direct Mode and then Buffer Mode |
|SPS MTU size | 244 bytes link MTU; up to 1000 bytes per AT string call (`AT+USPSWS`), 1000 bytes per AT binary call (`AT+USPSWB`) |

The table below summarises the major third-party components built into the firmware. The authoritative Software Bill of Materials is the CycloneDX `NORA-B27X-SBOM.json` shipped alongside the binary in each release archive.

|u-connectXpress software components |Versions in 3.5.0|
|:-----------------|:------------------|
|Zephyr RTOS | 4.4.2 — [github.com/zephyrproject-rtos/zephyr](https://github.com/zephyrproject-rtos/zephyr) |
|nRF Connect SDK | 3.4.1 — [github.com/nrfconnect/sdk-nrf](https://github.com/nrfconnect/sdk-nrf) |
|Mbed TLS | 4.1.1 — [github.com/Mbed-TLS/mbedtls](https://github.com/Mbed-TLS/mbedtls) |


For the AT command syntax see the [NORA-B27 AT command manual](https://github.com/u-blox/u-connectXpress/blob/main/NORA-B27/3.5.0/at_commands.md).

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

# Bluetooth use cases

The default Bluetooth configuration of NORA-B27 (3.5.0):

|u-connectXpress BLE default values | 3.5.0 |
|:----------------|:-----------------|
|BLE Mode default |**ON**, Peripheral (Mode = 2) |
|BLE Legacy Advertising default    |**OFF**, enable with `AT+UBTAL` |

The examples use these placeholder addresses; replace them with the real Bluetooth addresses of your devices.

- Peripheral address: AAAAAAAAAAAA
- Central address: BBBBBBBBBBBB

## Selecting the Bluetooth role

The use cases below assume that the required role is enabled. Check it first and change it if needed.

| Nr| Instructions | AT command | AT event |
|---|--------------|------------|----------|
| 1 | Read the Bluetooth mode | `AT+UBTM?` | `+UBTM:<mode>` |
| 2 | If needed, set the mode: `2` Peripheral | `AT+UBTM=<mode>` | `OK` |
| 3 | Store the setting | `AT&W` | `OK` |
| 4 | Restart | `AT+CPWROFF` | `+STARTUP` |

## Bluetooth GATT use cases

### Bluetooth GATT server

![bt-gatt-server](https://content.u-blox.com/sites/default/files/2024-02/bt-gatt-server.png)

NORA-B27 operates as a Peripheral and GATT server that sends notifications. It works with a remote Central acting as GATT client. The Peripheral role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

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

### Bluetooth SPS peripheral

![bt-sps-peripheral](https://content.u-blox.com/sites/default/files/2024-02/bt-sps-peripheral.png)

NORA-B27 operates as a Peripheral that accepts an SPS connection. It works with a remote Central that supports SPS. The Peripheral role must be enabled, see [Selecting the Bluetooth role](#selecting-the-bluetooth-role).

| Nr| Instructions                          | AT command  |  AT events |
|---|:---------------------------------------|:--------------------------------------|:--------------------|
| 1 | Enable SPS              | `AT+USPS=1`        | `OK` |
| 2 | Enable legacy advertising    | `AT+UBTAL` | `OK` |
| 3 | Wait for an incoming Bluetooth connection  |   | `+UEBTC:0,BBBBBBBBBBBBp` |
| 4 | Read the MTU | `AT+UBTCST=0,3` | `+UBTCST:3,247` |
| 5 | Read the RSSI (optional)   | `AT+UBTRSS=0`     | `+UBTRSS:-52` |
| 6 | The Central connects SPS |   | `+UESPSC:0` |
| 7 | SPS and Bluetooth link are down | | `+UESPSDC:0` `+UEBTDC:0` |

### SPS host tools and protocol documentation

The [u-blox/sps](https://github.com/u-blox/sps) repository documents the SPS GATT protocol and provides a Python reference implementation for hosts that talk SPS directly over Bluetooth LE, for example a PC or Raspberry Pi connecting to NORA-B27.

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

## Advertising options

| Feature | Command | Description |
|---------|---------|-------------|
| Non-connectable legacy advertising | `AT+UBTADL=<adv_data>,<adv_type>` | `<adv_type>` `0` connectable and scannable (default), `1` non-connectable scannable, `2` non-connectable non-scannable. Custom data is up to 28 bytes for connectable and 31 bytes for non-connectable advertising |
| Non-connectable extended advertising | `AT+UBTADE=<index>,<adv_data>,<ext_adv_type>` | `<ext_adv_type>` `0` connectable (default), `1` non-connectable. Custom data is up to 226 bytes for connectable and 229 bytes for non-connectable advertising |
| Extended advertising interval | `AT+UBTAES=<index>,<min>,<max>` | Interval in units of 0.625 ms, range 32..16384 (defaults 1600 and 2000) |

## Bluetooth security

Pairing establishes an encrypted link between two devices. Bonding stores the exchanged keys so that the peers can reconnect securely.

- `AT+UBTPM=1` — allow incoming pairing requests
- `AT+UBTIOC=<cap>` — set the I/O capabilities used during pairing
- `AT+UBTBSM=<mode>` — set the minimum security mode required for bonding
- `AT+UBTBDL` — list bonded devices
- `AT+UBTUB=<bd_addr>` — delete a stored bond

Bluetooth security is disabled by default and must be configured before use.

For peers using Resolvable Private Addresses (RPA), the resolved identity address is returned as soon as it is available.

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

# Power save use cases

## Light sleep

`AT+UPMS` puts the module in light sleep. The Bluetooth connections are kept. The host keeps receiving events, but the module does not respond to AT commands. On a connection event the module wakes up, sends the URC and goes back to sleep.
| Nr | Instructions | AT command |
|----|--------------|------------|
| 1 | Enter light sleep | `AT+UPMS` |
| 2 | Exit light sleep: pull the `WAKE_UP` pin low, or send a character on the UART and wait 50 ms | |

## Deep sleep

Deep sleep is the most efficient power level and almost like a power off; no radio communication is possible.

- Enter deep sleep with `AT+UPMDS` or `AT+UPMDS=<wakeup_mode>`.- `<wakeup_mode>` selects how the module wakes up: `0` pull the module wake-up pin low (default), `1` module reset pin, `2` module UART RX pin. See the data sheet for the pins.
- After wake-up the module is in the same state as after a reset.

# Send and receive data

NORA-B27 supports three ways to exchange data:

| Mode | Characters | Typical use |
|------|------------|-------------|
| **String mode** | Printable ASCII (`0x21-0x7E`, `0xA1-0xFF`) | Text, JSON, XML, NMEA |
| **Binary mode** | Full byte range (`0x00-0xFF`) | Files, certificates, binary protocols |
| **Transparent mode** | Full byte range (`0x00-0xFF`) | Serial cable replacement, highest throughput |

Received data is delivered in one of two ways: in **buffered mode** (default) a data-available event is sent and the host reads the data; in **direct mode** the data is delivered in the event. Select the mode with `AT+USPSRM` for SPS.

## String mode

String parameters are enclosed in double quotes. Use the escape sequences `\"` (double quote), `\\` (backslash), `\r`, `\n`, `\t`, `\0` (null) and `\xHH` (any byte).

`AT+USPSRM=<receive_mode>`: `0` buffered mode (`+UESPSDA`), `1` direct string mode (`+UESPSDS`).

| Nr| Instructions                          | AT command  | AT event|
|---|---------------------------------------|-----------------------------------|---|
| 1 | Write SPS data | `AT+USPSWS=0,"Hello from NORA-B27"` | `+USPSWS:0,19` `OK` |
| 2 | Incoming SPS data (buffered mode) | | `+UESPSDA:0,19` |
| 3 | Read SPS data | `AT+USPSRS=0,19` | `+USPSRS:0,19,"Hello from NORA-B27"` |

## Binary mode

Use binary mode for files and binary protocols. See [Binary data](#binary-data) for the frame format.

> **Binary AT-command framing in one line.** Every binary command (`…B`) is followed **immediately** by a 3-byte header `01 <lenMSB> <lenLSB>` and then the raw payload bytes. Commas inside the parameter list are normal — the rule is that the **last** parameter butts straight up against the `0x01` (SOH) byte: no trailing `,`, no space, no `\r`. The `0x01` IS the separator between the parameter list and the binary block. Sending the same command in string form (with a trailing `,"..."` instead of the SOH frame) returns **`ERROR:47`** (`U_AT_STATUS_BIN_CMD_EXEC_AS_STD_CMD`).

`AT+USPSRM=2` selects direct binary mode for SPS: `+UESPSDB:<conn_handle>{binary_data}`.

| Command | Syntax | Response |
|---------|--------|----------|
| SPS write | `AT+USPSWB=<conn_handle>{binary_data}` | `+USPSWB:<conn_handle>,<written_length>` |
| SPS read | `AT+USPSRB=<conn_handle>,<length>` | `+USPSRB:<conn_handle>{binary_data}` |

`{binary_data}` is the 3-byte header `01 <lenMSB> <lenLSB>` followed by the raw payload. Read example: `AT+USPSRB=0,19` returns `+USPSRB:0` + `01 00 13` + 19 raw payload bytes.

## Transparent mode overview

Transparent mode (TM) turns NORA-B27 into a bridge that forwards all UART data to a remote device without AT command processing, like the data mode of legacy u-blox short range products. It works with SPS (Bluetooth LE) connections.

- Only **one active connection** is allowed at a time and it must be established before entering transparent mode.
- All UART data is sent unmodified. Return to command mode with the escape sequence `+++` (no line ending), after at least 1 second without data before and after the sequence. The timing can be changed with `AT+UTMES=<pre_timeout>,<post_timeout>,<escape_timeout>` (defaults 1000, 1000 and 200 ms; the escape character is set with `ATS2`).
- A partial escape sequence is not transmitted to the peer until another character is sent (known limitation).

`AT+UTM=<link_type>,<handle>` enters transparent mode on an existing connection: `<link_type>` `0` SPS, `1` TCP socket, `2` UDP socket; `<handle>` is the connection or socket handle.

```text
AT+UTM=0,0                        // SPS connection 0
OK
Hello from NORA-B27!    // forwarded to the remote device
+++                               // no CR/LF
OK
```

**Connection status on the Host Wakeup pin:** `AT+USYHWP=1` configures the Host Wakeup pin to indicate the transparent mode connection status. The default `AT+USYHWP=0` leaves the pin free to use as a GPIO. The setting is stored with `AT&W` and takes effect after a reboot.

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

Send 2 bytes (`0xFF, 0xEE`) over SPS connection 0. On the wire each cell is one byte; `│` separates the AT command, the 3-byte header and the payload:

```text
ascii :  A  T  +  U  S  P  S  W  B  =  0   │             │
hex   : 41 54 2B 55 53 50 53 57 42 3D 30   │ 01 00 02    │ FF EE
                                            └─ SOH ─┼─ len ─┘   ↑ payload (2 bytes)
```

- `AT+USPSWB=0` (11 ASCII bytes) writes to SPS connection 0.
- `01` is the SOH start marker and `00 02` the length (2 bytes, big-endian).
- `FF EE` are the 2 raw payload bytes.

There is **no comma and no `\r`** between `=0` and `01`. The text form `AT+USPSWB=0010002FFEE` seen in older documents prints the same bytes as ASCII hex digits and is **not** what travels down the UART.

Data received with `AT+USPSRB` includes the same header:

```text
resp  :  +  U  S  P  S  R  B  :  0          │             │
hex   : 2B 55 53 50 53 52 42 3A 30          │ 01 00 02    │ FF EE
```

The text `Hello from NORA-B27` is 19 bytes (`0x0013`), so the header is `01 00 13`.

## Programming examples

Both examples write the AT command, the 3-byte header and the payload in **one** write so that the frame stays intact. Open the serial port in raw 8N1 mode and do **not** terminate the command with `\r` or `\n`. A single call accepts up to 1000 bytes for `AT+USPSWB`.

### Python

```python
import serial

MAX_PAYLOAD = 1000  # bytes per AT binary call


def send_binary_data(port: serial.Serial, at_command: str, payload: bytes) -> None:
    """Send an AT command followed by the 3-byte binary header and the payload."""
    if len(payload) > MAX_PAYLOAD:
        raise ValueError(f"payload exceeds {MAX_PAYLOAD} bytes per call")
    header = b"\x01" + len(payload).to_bytes(2, "big")
    port.write(at_command.encode("ascii") + header + payload)


with serial.Serial("COM3", 115200) as port:
    send_binary_data(port, "AT+USPSWB=0", b"Hello from NORA-B27")
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

Usage: configure the port in raw 8N1 mode with `termios`, then call `send_binary_data(fd, "AT+USPSWB=0", payload, payload_len)`.

# Error codes

Extended error codes show why an AT command failed. They are for information only and may change between versions. The complete list for each release is in the [error code list](https://github.com/u-blox/u-connectXpress/blob/main/NORA-B27/3.5.0/error_codes.md).

- `AT+USYEE=1` enables extended error reporting: failed commands return `ERROR:<error_code>`.
- `AT+USYEC?` returns the error code of the last failed command: `+USYEC:<error_code>`.

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

# Software update

The software is updated with the XMODEM-1K protocol over the UART, at baud rates up to 1000000 bps. There are two ways to start an update: with an AT command or with the bootloader. The firmware image is named `NORA-B27X-SW-3.5.0-<build>.bin` in the release archive.

![firmware](https://content.u-blox.com/sites/default/files/2024-02/firmware.png)

## Update software by AT command

| Nr| Instructions                              | AT command                        | AT event              |
|---|-------------------------------------------|-----------------------------------|------------------------------|
| 1 |  Start the XMODEM protocol with an AT command  | `AT+USYFWUS=1000000` | |
| 2 | NORA-B27 is ready to receive the software with XMODEM or XMODEM-1K | `CCCCCCCCCCC...`  | |
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
| 3 |  Change the baud rate, up to 1000000 bps (optional)  | `r 1000000` | |
| 4 |  Start the XMODEM protocol  | `x`  | |
| 5 | NORA-B27 is ready to receive the software with XMODEM or XMODEM-1K |  | `CCCCCCCCCCC...` |
| 6    | Wait for the prompt that shows that the software has been downloaded | |  `>` |
| 7    | Restart the module |  `q`  | |
| 8 | Wait for the module to restart in AT mode |  | `+STARTUP`   |
| 9 | Check the version of the software | `AT+GMR`| `"v3.5.0"` |

## XMODEM host tool

The [u-blox/ucx-xmodem](https://github.com/u-blox/ucx-xmodem) repository contains an XMODEM-1K sender in Python ([xmodem.py](https://github.com/u-blox/ucx-xmodem/blob/main/xmodem.py), [README](https://github.com/u-blox/ucx-xmodem/blob/main/README_xmodem_python.md)) and in C for Windows ([xmodem.c](https://github.com/u-blox/ucx-xmodem/blob/main/xmodem.c), [README](https://github.com/u-blox/ucx-xmodem/blob/main/README_xmodem_c.md)). Both tools use the same arguments, send the AT command that starts the XMODEM mode and show the transfer progress.

```bash
# Python (pyserial)
pip install pyserial
python xmodem.py COM3 "NORA-B27X-SW-3.5.0-<build>.bin" 115200
python xmodem.py /dev/ttyUSB0 "NORA-B27X-SW-3.5.0-<build>.bin"  # Linux

# C (Windows, GCC/MinGW)
gcc -o xmodem xmodem.c -lkernel32
xmodem.exe COM3 "NORA-B27X-SW-3.5.0-<build>.bin" 115200
```

```python
from xmodem import ublox_firmware_update

success = ublox_firmware_update("COM3", "NORA-B27X-SW-3.5.0-<build>.bin", 3000000)
```

# Related information

- **[NORA-B27 Product Page](https://www.u-blox.com/en/product/nora-b2-series)** — product information, specifications and ordering details
- **[s-center 2](https://www.u-blox.com/en/product/s-center)** — configuration and development tool for u-blox modules
- **[NORA-B27 AT Command Manual](https://github.com/u-blox/u-connectXpress/blob/main/NORA-B27/3.5.0/at_commands.md)** — AT command reference
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