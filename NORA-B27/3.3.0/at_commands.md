# NORA-B27 AT Command Manual

Firmware version: v3.3.0

# Contents

[1 AT command settings](#at-command-settings)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1 Definitions](#definitions)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.1 Command description](#commanddescription)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.2 Command line](#commandline)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.3 Default values](#defaultvalues)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.4 Information text responses and result codes](#infomation)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.5 S\-parameters](#sparameters)<br>
[2 General operation](#general-operation)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1 Start up](#startup)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.2 AT Command types](#atcommandtypes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.2\.1 Set command](#setcommand)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.2\.2 Read command](#readcommand)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.2\.3 Status command](#statuscommand)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.2\.4  Unsolicited result code \(URC\)](#unsolicited)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3 Data types](#datatypes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.1 String](#string)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.2 Integer](#integer)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.3 Enumerator](#enumerator)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.4  Byte\_Array](#bytearray)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.5 IPv4\_Addr](#ipv4addr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.6 IPv6\_Addr](#ipv6addr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.7 MAC\_Addr](#macaddr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.8 Bd\_Addr](#bdaddr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.9 List](#list)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.3\.10 Binary](#binary)<br>
[3 General](#general)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1 AT Commands](#u_31-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.1 AT \- Attention](#at)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.2 AT\+CGMI \- Manufacturer identification](#atcgmi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.3 AT\+GMI \- Manufacturer identification](#atgmi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.4 AT\+CGMM \- Model identification](#atcgmm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.5 AT\+GMM \- Model identification](#atgmm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.6 AT\+CGMR \- Software version identification](#atcgmr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.7 AT\+GMR \- Software version identification](#atgmr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.8 AT\+CGSN \- Serial number](#atcgsn)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.9 AT\+GSN \- Serial number](#atgsn)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.10 ATI \- Identification information](#ati)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.11 AT\+CSGT \- Greeting Text](#atcsgt)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2 Unsolicited Response Codes](#u_32-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.1 \+STARTUP \- Startup indication](#startup)<br>
[4 System](#system)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1 AT Commands](#u_41-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.1 AT\+CPWROFF \- Module switch off](#atcpwroff)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.2 AT\+USYFWUS \- Firmware Update using serial port](#atusyfwus)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.3 AT\+USYBL \- Start the boot loader command line interface](#atusybl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.4 AT&W \- Store current configuration](#atw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.5 AT\+USYLA \- Local Address](#atusyla)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.6 AT\+USYFR \- Factory Restore](#atusyfr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.7 AT\+USYDS \- Default Settings](#atusyds)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.8 AT\+USYUS \- Uart Settings](#atusyus)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.9 AT\+USYEC \- Error Code](#atusyec)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.10 AT\+USYEE \- Extended Error codes on/off](#atusyee)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.11 ATE \- Echo On/Off](#ate)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.12 ATS \- S\-registers](#ats)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.13 AT\+UTMES \- Transparent mode escape sequence settings](#atutmes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.14 AT\+USCT \- Chip Die Temperature \(experimental\)](#atusct)<br>
[5 Bluetooth](#bluetooth)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1 AT Commands](#u_51-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.1 AT\+UBTM \- Bluetooth Mode](#atubtm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.2 AT\+UBTDC \- Bluetooth Disconnect](#atubtdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.3 AT\+UBTLN \- Bluetooth Local Name](#atubtln)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.4 AT\+UBTRSS \- Bluetooth RSSI](#atubtrss)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.5 AT\+UBTCL \- Bluetooth Connection List](#atubtcl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.6 AT\+UBTCST \- Bluetooth Connection Status](#atubtcst)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.7 AT\+UBTA \- Read which advertisements are currently running](#atubta)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.8 AT\+UBTADL \- Bluetooth Advertisement Data Legacy](#atubtadl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.9 AT\+UBTADLC \- Bluetooth Advertising Data Legacy Clear](#atubtadlc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.10 AT\+UBTADE \- Bluetooth Advertising Data Extended](#atubtade)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.11 AT\+UBTADEC \- Bluetooth Advertising Data Extended Clear](#atubtadec)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.12 AT\+UBTAE \- Bluetooth Advertise Extended](#atubtae)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.13 AT\+UBTAED \- Bluetooth Advertise Extended Disable](#atubtaed)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.14 AT\+UBTASD \- Bluetooth Advertisement Scan Data](#atubtasd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.15 AT\+UBTASDC \- Bluetooth Scan Data Clear](#atubtasdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.16 AT\+UBTAL \- Bluetooth Advertise Legacy Enable](#atubtal)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.17 AT\+UBTALD \- Bluetooth Advertise Legacy Disable](#atubtald)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.18 AT\+UBTAD \- Bluetooth Directed Advertisement](#atubtad)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.19 AT\+UBTADD \- Bluetooth Advertise Directed Disable](#atubtadd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.20 AT\+UBTCS \- Bluetooth Connection Settings](#atubtcs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.21 AT\+UBTALS \- Bluetooth Advertisement Legacy Settings](#atubtals)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.22 AT\+UBTIOC \- Bluetooth I/O Capabilities](#atubtioc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.23 AT\+UBTBSM \- Bluetooth Bond Security Mode](#atubtbsm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.24 AT\+UBTPM \- Bluetooth Pairing Mode](#atubtpm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.25 AT\+UBTUC \- Bluetooth User Confirmation](#atubtuc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.26 AT\+UBTUPE \- User passkey entry](#atubtupe)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.27 AT\+UBTB \- Bluetooth Bond](#atubtb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.28 AT\+UBTUB \- Bluetooth Unbond](#atubtub)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.29 AT\+UBTBDL \- Bluetooth Bonded Devices List](#atubtbdl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.30 AT\+UBTDIS \- Bluetooth Device Information Service](#atubtdis)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.31 AT\+UBTPHYR \- Bluetooth PHY Request](#atubtphyr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.32 AT\+UBTMOP \- Bluetooth Max Output Power](#atubtmop)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.33 AT\+UBTMOPC \- Bluetooth Max Output Power Clear](#atubtmopc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2 Unsolicited Response Codes](#u_52-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.1 \+UEBTC \- Event Bluetooth Connected](#uebtc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.2 \+UEBTDC \- Event Bluetooth Disconnected](#uebtdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.3 \+UEBTB \- Event Bluetooth Bond status](#uebtb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.4 \+UEBTUC \- Event Bluetooth User Confirmation](#uebtuc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.5 \+UEBTUPD \- Event Bluetooth Passkey entry](#uebtupd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.6 \+UEBTUPE \- Event Bluetooth Passkey request](#uebtupe)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.7 \+UEBTPHYU \- Event Bluetooth PHY update](#uebtphyu)<br>
[6 GATT Server](#gatt-server)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1 AT Commands](#u_61-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.1 AT\+UBTGS \- GATT Service define](#atubtgs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.2 AT\+UBTGC \- GATT Characteristic define](#atubtgc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.3 AT\+UBTGHCC \- GATT Host Controlled Characteristic](#atubtghcc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.4 AT\+UBTGD \- GATT Descriptor define](#atubtgd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.5 AT\+UBTGSA \- GATT Service Activate](#atubtgsa)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.6 AT\+UBTGRRR \- GATT Read Request Respond](#atubtgrrr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.7 AT\+UBTGNS \- GATT Notification Send](#atubtgns)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.8 AT\+UBTGIS \- GATT Indication Send](#atubtgis)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.9 AT\+UBTGAV \- GATT Attribute Value](#atubtgav)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.10 AT\+UBTGRRRE \- GATT Read Request Respond with error code](#atubtgrrre)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.11 AT\+UBTGWRE \- GATT Write Respond with Error code](#atubtgwre)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.12 AT\+UBTGWRR \- GATT Write Request Respond](#atubtgwrr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2 Unsolicited Response Codes](#u_62-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.1 \+UEBTGCW \- Event GATT Server Write](#uebtgcw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.2 \+UEBTGRR \- Event GATT Server Read Response](#uebtgrr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.3 \+UEBTGIC \- Event GATT Server Indication Confirmation](#uebtgic)<br>
[7 SPS](#sps)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1 AT Commands](#u_71-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.1 AT\+USPS \- SPS \- Enable/Disable Service](#atusps)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.2 AT\+USPSWS \- SPS Write String](#atuspsws)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.3 AT\+USPSWB \- SPS Write Binary](#atuspswb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.4 AT\+USPSRM \- SPS Receive Mode](#atuspsrm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.5 AT\+USPSRS \- SPS Read String](#atuspsrs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.6 AT\+USPSRB \- SPS Read Binary](#atuspsrb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2 Unsolicited Response Codes](#u_72-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.1 \+UESPSC \- Event SPS Connection](#uespsc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.2 \+UESPSDC \- Event SPS Disconnection](#uespsdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.3 \+UESPSDS \- Event SPS Data String](#uespsds)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.4 \+UESPSDB \- Event SPS Data Binary](#uespsdb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.5 \+UESPSDA \- Event SPS Data Available](#uespsda)<br>
[8 Power](#power)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1 AT Commands](#u_81-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.1 AT\+UPMDS \- Power Management Deep Sleep](#atupmds)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.2 AT\+UPMS \- Power Management Sleep](#atupms)<br>
[9 Transparent](#transparent)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1 AT Commands](#u_91-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.1 AT\+UTM \- Transparent Mode](#atutm)<br>

<a name="at-command-settings" id="at-command-settings"></a>
# **1 AT command settings**
u-blox short range modules provide at least one physical serial interface for configuration and data transport.
At module power on, the module enters the command mode. For more details on the command mode, see

For module and terminal connection and settings, see the corresponding evaluation kit user guide.

<a name="definitions" id="definitions"></a>
## **1.1 Definitions**
In this document, the following naming conventions are used:
- DCE (Data Communications Equipment): u-blox short range module
- DTE (Data Terminal Equipment) or TE (Terminal Equipment): The terminal that issues the command to the
module.

The terms DCE and DTE are used in the serial interface context. The DCE interface can operate in the following
modes:
- AT mode: The DCE waits for AT command instructions. The DCE interprets all the characters
received as commands to execute. The DCE may send responses back to the DTE indicating the outcome
of the command or further information without having received any command from the DTE (for example,
 unsolicited response code - URC).
- Transparent mode (TM): The DCE transfers data after having sent the AT+UTM or AT+UTMP command; all characters sent to the DCE
are intended to be transmitted to the remote party. Any further characters received over the serial link are
deemed to be from the remote party, and any characters sent are transmitted to the remote party.
- Transparent mode persistent (TMP): The same as Transparent mode (TM) but it is possible to store the setting and enter this mode at start up.


It is possible to switch from the Transparent mode (TM) and Transparent mode persistent (TMP)to command mode in the following ways:
• Using the escape sequence: For more details, see Escape Character S2

<a name="commanddescription" id="commanddescription"></a>
### **1.1.1 Command description**
The AT commands configure and enable the short range module functionality according to 3GPP normative
and u-blox specifications. The AT commands are issued to the module via a hyper terminal through a command
line and are described in the following sections. A general description of each command is provided including
functionalities, correct syntax to be provided by the TE/DTE and allowed responses.
The command description defines each named parameter with its type, range (valid / acceptable values),
 default value (when available) and factory default setting (when applicable).
In this document, <CR><LF> are intentionally omitted in the command syntax. See Chapter 1.1.2 and
Chapter 1.1.4 for more information.

<a name="commandline" id="commandline"></a>
### **1.1.2 Command line**
The AT commands are typically issued to the short range modules using a command line with the following
generic syntax:
"AT"<command_name><string><S3_character>
Where:
- "AT": The prefix to be set at the beginning of each command line
- <command_name>: The command name string; it can have a "+" character as prefix
- <string>: The string consisting of the value parameters following the syntax provided in this manual.

The following rules are used when describing the command syntax:
- <...>: The name in angle brackets is a parameter. The brackets themselves do not appear in the
command line
- [...]: The square brackets represent the optional parameters of a command or an optional part of the DCE
information text response. Brackets themselves do not appear in the command line. When a parameter
is not given, the value will be set to the default value provided in the command description
- <S3_character>: The command line termination character; it can be set with Command line termination
character S3 command; the factory-programmed termination character is <CR>
The command line is not case sensitive.
The serial interface driver generally does not allow a new command until the previous one has been terminated
by "OK" or an error message.

<a name="defaultvalues" id="defaultvalues"></a>
### **1.1.3 Default values**
If the command has optional parameters, and default values are not specified, the default values are assumed
as follows:
- For parameters of type Number, the default value is 0
- For parameters of type String, the default value is an empty string

<a name="infomation" id="infomation"></a>
### **1.1.4 Information text responses and result codes**
The response format is as follows:
- Information text response(s): <S3_character><S4_character><text><S3_character><S4_character>
- Result codes: <S3_character><S4_character><verbose code><S3_character><S4_character>
where
- <S3_character> is the command line termination character; it can be set with S3 command
- <S4_character> is the linefeed character; it can be set with S4 command
If the command line is successfully processed and the command is correctly executed, in verbose response
format the string "OK" is sent as a final result code.
Intermediate output and descriptive output of a command are formatted as information text responses;
If more than one string has to be printed out (see for example Bluetooth Discovery {ref:AT+UBTD} command description),
additional command line termination and linefeed characters can be inserted for the sake of readability.
If the command is not accepted by the DCE, an error result code will be displayed. The error result has the
following format:
• <S3_character><S4_character>ERROR<S3_character><S4_character>
When using commands in <data_format> Binary, for example +AT+USPSWB, the formating of the AT command differs a bit from regular AT commands.

<a name="sparameters" id="sparameters"></a>
### **1.1.5 S-parameters**
The S-parameters, as specified in ITU-T recommendation V250, constitute a group of commands that begin
with the string "ATS". They are generally indicated as S registers and are used to configure the way the module
operates. Their syntax is:
ATS<parameter_number>?
ATS<parameter_number>=<value>
The number following the "ATS" is the referenced S parameter.
u-blox short range modules support the following set of S-parameters (<parameter_number>):
- 2: escape character setting (for more details see the S2)
- 3: command line termination character setting (for more details see the S3)
- 4: response formatting character setting (for more details see the S4)
- 5: command line editing character setting (for more details see the S5)

<a name="general-operation" id="general-operation"></a>
# **2 General operation**

<a name="startup" id="startup"></a>
## **2.1 Start up**
Start up mode is AT mode by default, if Persistent Transparent mode is use see AT+UTMP command.

<a name="atcommandtypes" id="atcommandtypes"></a>
## **2.2 AT Command types**

<a name="setcommand" id="setcommand"></a>
### **2.2.1 Set command**
A set command configures preferred settings for the specified command. The set command is the only way to
set the preferred settings in the DCE. Parameters set with a set command will be used immediately and the
parameters can be stored to the start up database using &W.
Some Set commands requires a reboot before using. Store with &W and reset with +CPWROFF.

<a name="readcommand" id="readcommand"></a>
### **2.2.2 Read command**
A read command provides current setting of the command parameters. It is used to find out the current
command configuration.

<a name="statuscommand" id="statuscommand"></a>
### **2.2.3 Status command**
A status command provides current operating status of the module.

<a name="unsolicited" id="unsolicited"></a>
### **2.2.4  Unsolicited result code (URC)**
An unsolicited result code is a string message (provided by the DCE) that is not triggered as a information
text response to a previous AT command and can be output, when enabled, at any time to inform the DTE of
a specific event or status change. The URC can have the same name of the command that enables it or can
be enabled by another command.

<a name="datatypes" id="datatypes"></a>
## **2.3 Data types**
The definition of each command specifies the data types used for values associated with the command. The
different data types are listed below and are described in the following subsections:
- String
- Integer
- Enumerator
- Byte_Array
- IPv4_Addr
- IPv6_Addr
- MAC_Addr
- Bd_Addr
- List
- Binary

<a name="string" id="string"></a>
### **2.3.1 String**
A string shall consist of a sequence of displayable characters from the ISO 8859-1 character set, except for characters `\`, `"` and some special characters, see table below. A string constant shall be delimited by two double quote `"` characters, for example, "Donald Duck". If the double quote character `"` is to be used within a string, for example, "My friend "Bono" is a singer", they have to be represented as the escape character `\"`. If the backslash character `\` is to be used within a string constant, it has to be represented as the escape character `\\`. An empty string is represented by two adjacent delimiters - `""`.

| Escape character | Special character|
| ----------|----------|
| `\r` | Carriage return
| `\n` | New line
| `\t` | Tab
| `\b` | Backspace
| `\"` | For using `"` character inside an AT string
| `\\` | Backslash
| `\0` | Null character
| `\xHH` | For representing any byte. HH is 2 hex characters

<a name="integer" id="integer"></a>
### **2.3.2 Integer**
An integer value consists of a sequence of characters, all in the range {0..9} plus a possible minus ("-") sign for
negative values. Numeric constants are expressed in decimal format only.

<a name="enumerator" id="enumerator"></a>
### **2.3.3 Enumerator**
An enumerator value is actually an integer, where all its possible values are specified in each case. Only the
defined values are accepted for the command in question.

<a name="bytearray" id="bytearray"></a>
### **2.3.4  Byte_Array**
A Byte_Array consists of a sequence of characters expressed in two digit hexadecimal in the ranges {0..9}, {a..f}
and {A..F}. The hexadecimal values are grouped together without delimiters; an example of Byte_Array (three
values) is "800000" (Bit 23 is set), excluding the double quote characters.

<a name="ipv4addr" id="ipv4addr"></a>
### **2.3.5 IPv4_Addr**
An IPv4_Addr is a special text string in dotted decimal notation form (that is, four numbers in the range 0-255
separated by periods). An example IP address is "192.168.0.1", including the double quote characters.

<a name="ipv6addr" id="ipv6addr"></a>
### **2.3.6 IPv6_Addr**
An IPv6_Addr is a special text string represented as eight groups of four hexadecimal digits, each group
representing 16 bits (two octets) and surrounded by brackets. The groups are separated by colons (\:). An
example of an IPv6 address is "[2001:0db8:85a3:0000:0000:8a2e:0370:7334]", including the double quote
characters.

<a name="macaddr" id="macaddr"></a>
### **2.3.7 MAC_Addr**
A MAC_Addr is a Byte_Array of fixed length (6 values). An example MAC_Addr is "01A0F7101C08", excluding
the double quote characters.

<a name="bdaddr" id="bdaddr"></a>
### **2.3.8 Bd_Addr**
A Bd_Addr is a MAC_Addr followed an optional address type, "r" for random address and "p" for public address.
If the address type is omitted, it will default to public. An example Bd_Addr is "01A0F7101C08p", excluding the
double quote characters.

<a name="list" id="list"></a>
### **2.3.9 List**
A List is a comma (,) separated list of items, where items can be any of the other data types. For example,
channel list is a list of integers, [1,6,11], inluding the two brackets characters. Example AT+UWCL=[1,6,11]

<a name="binary" id="binary"></a>
### **2.3.10 Binary**

The binary data starts with `\x01` (SOH - Start Of Header), following by the length of the data in two bytes format (UINT16) follwed by the binary data.
The binary data shall not be terminated with the normal `\x0D` (\r - Carriage Return).

The binary header is three bytes:
`{0x01(SOH Start Of Header), MSB_datalength, LSB_datalength}`

All commands and URC that use binary data are "complete" without the binary data, the binary data is sent directly after the AT command, in most case after the handle.

The AT command follows directly by the binary data, without any "," or "\r" or anything in between.

Example:
`AT+USPSWB=0{0x01,0x00,0x02,0xFF,0xEE}`
This command writes to socket 0, 2 bytes data the data is 0xFF 0xEE.
Note that the brackets { } should not be sent, only indicates the start and end of binary data.

Binary data for Socket, SPS and certificate upload all use the same Binary data format.


### **2.3.11 Buffered mode**
This is the default data mode, the data is read out after an event has been received. It is possible to stop and control the incoming data flow.
### **2.3.12 Direct mode**
In this mode the data is included in the received event, then data will be sent to the host as soon it is avaliable. It is not possible to stop the incoming data flow.
### **2.3.13 Transparent mode**
In this mode the data is sent and received without any AT commands, the limitation that this mode only works with a point-to-point connection.
### **2.3.13 Transparent mode persistent**
This is the same as transparent mode, but can be storted in flash and be active at startup.

<a name="general" id="general"></a>
# **3 General**

<a name="u_31-at-commands" id="u_31-at-commands"></a>
## **3.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT](#at) | Attention |
| [AT+CGMI](#atcgmi) | Manufacturer identification |
| [AT+GMI](#atgmi) | Manufacturer identification |
| [AT+CGMM](#atcgmm) | Model identification |
| [AT+GMM](#atgmm) | Model identification |
| [AT+CGMR](#atcgmr) | Software version identification |
| [AT+GMR](#atgmr) | Software version identification |
| [AT+CGSN](#atcgsn) | Serial number |
| [AT+GSN](#atgsn) | Serial number |
| [ATI](#ati) | Identification information |
| [AT+CSGT](#atcsgt) | Greeting Text |

<a name="at" id="at"></a>
### **3.1.1 AT - Attention**

Attention command that determines the presence of a Data Communication Equipment (DCE).


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT` | Attention command. |

<a name="atcgmi" id="atcgmi"></a>
### **3.1.2 AT+CGMI - Manufacturer identification**

Read a text string that identifies the manufacturer.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CGMI` | Read manufacturer text string. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<manufacturer>` | Successful read response.<br>Note: The manufacturer string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| manufacturer | string | Manufacturer ("u-blox"). |

<a name="atgmi" id="atgmi"></a>
### **3.1.3 AT+GMI - Manufacturer identification**

Read a text string that identifies the manufacturer.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+GMI` | Read manufacturer text string. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<manufacturer>` | Successful read response.<br>Note: The manufacturer string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| manufacturer | string | Manufacturer ("u-blox"). |

<a name="atcgmm" id="atcgmm"></a>
### **3.1.4 AT+CGMM - Model identification**

Read a text string that identifies the device model.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CGMM` | Read device model. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<device_model>` | Successful read response.<br>Note: The device_model string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| device\_model | string | Device model |

<a name="atgmm" id="atgmm"></a>
### **3.1.5 AT+GMM - Model identification**

Read a text string that identifies the device model.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+GMM` | Read device model. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<device_model>` | Successful read response.<br>Note: The device_model string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| device\_model | string | Device model |

<a name="atcgmr" id="atcgmr"></a>
### **3.1.6 AT+CGMR - Software version identification**

Read a text string that identifies the software version of the module.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CGMR` | Read software version. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<version>` | Successful read response.<br>Note: The version string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| version | string | Version. |

<a name="atgmr" id="atgmr"></a>
### **3.1.7 AT+GMR - Software version identification**

Read a text string that identifies the software version of the module.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+GMR` | Read software version. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<version>` | Successful read response.<br>Note: The version string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| version | string | Version. |

<a name="atcgsn" id="atcgsn"></a>
### **3.1.8 AT+CGSN - Serial number**

Read the product serial number.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CGSN` | Read serial number. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<serial_number>` | Successful read response.<br>Note: The serial_number string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| serial\_number | string | Serial number. |

<a name="atgsn" id="atgsn"></a>
### **3.1.9 AT+GSN - Serial number**

Read the product serial number.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+GSN` | Read serial number. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<serial_number>` | Successful read response.<br>Note: The serial_number string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| serial\_number | string | Serial number. |

<a name="ati" id="ati"></a>
### **3.1.10 ATI - Identification information**

Read identification information.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `ATI9` | Read identification information. |
| `ATI0` | Read type code. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<application_version>,<unique_identifier>` | Successful read response.<br>Note: The application_version and unique_identifier strings are returned without any response prefix.<br> |
| `<type_code>` | Successful read response.<br>Note: The type_code string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| application\_version | string | Application version. |
| unique\_identifier | string | Unique identifier. |
| type\_code | string | Type code for the module. |

<a name="atcsgt" id="atcsgt"></a>
### **3.1.11 AT+CSGT - Greeting Text**

Configures and activates/deactivates the greeting text.
The configuration change in the greeting text will be applied at the subsequent boot.
When active, the greeting text is sent at boot once. The default greeting text is +STARTUP.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CSGT=<greeting_mode>[,<text>]` | Set the greeting text and mode.<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |
| `AT+CSGT?` | Read the greeting text. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+CSGT:<greeting_mode>,<text>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| greeting\_mode | enumerator | Valid values:<br>0: Turn off the greeting text.<br>1: Turn on the greeting text. |
| text | string | The greeting text.<br>Note: Can not be an empty string.<br><br><br>Valid length: 1..49 |

<a name="u_32-unsolicited-response-codes" id="u_32-unsolicited-response-codes"></a>
## **3.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+STARTUP](#startup) | Startup indication |

<a name="startup" id="startup"></a>
### **3.2.1 +STARTUP - Startup indication**

Indicates the startup of the device and that it is ready to receive commands.


**Syntax**<br>
```+STARTUP```


**Notes**<br>
The +STARTUP URC can be customized using the AT+CSGT command.

<a name="system" id="system"></a>
# **4 System**

System AT commands

<a name="u_41-at-commands" id="u_41-at-commands"></a>
## **4.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+CPWROFF](#atcpwroff) | Module switch off |
| [AT+USYFWUS](#atusyfwus) | Firmware Update using serial port |
| [AT+USYBL](#atusybl) | Start the boot loader command line interface |
| [AT&W](#atw) | Store current configuration |
| [AT+USYLA](#atusyla) | Local Address |
| [AT+USYFR](#atusyfr) | Factory Restore |
| [AT+USYDS](#atusyds) | Default Settings |
| [AT+USYUS](#atusyus) | Uart Settings |
| [AT+USYEC](#atusyec) | Error Code |
| [AT+USYEE](#atusyee) | Extended Error codes on/off |
| [ATE](#ate) | Echo On/Off |
| [ATS](#ats) | S-registers |
| [AT+UTMES](#atutmes) | Transparent mode escape sequence settings |
| [AT+USCT](#atusct) | Chip Die Temperature |

<a name="atcpwroff" id="atcpwroff"></a>
### **4.1.1 AT+CPWROFF - Module switch off**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CPWROFF` | Reboot the DCE. |

<a name="atusyfwus" id="atusyfwus"></a>
### **4.1.2 AT+USYFWUS - Firmware Update using serial port**

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
| flow\_control | integer | Valid values: 0 or 1<br><br>Default value: 0 |
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200, 2400, 4800, 9600, 14400, 28800, 31250, 38400, 56000, 57600, 76800, 115200, 230400, 250000, 460800, 921600, 1000000<br><br>Default value: U_CONFIG_DEFAULT_BAUDRATE |

<a name="atusybl" id="atusybl"></a>
### **4.1.3 AT+USYBL - Start the boot loader command line interface**

Force start of the boot loader. The boot loader will start at the defined baud rate.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYBL=<baud_rate>[,<flow_control>]` | Force start of the boot loader. |
| `AT+USYBL` | Force start of the boot loader with default settings. Baudrate 115200 and flow control off. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| flow\_control | integer | Valid values: 0 or 1<br><br>Default value: 0 |
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200, 2400, 4800, 9600, 14400, 28800, 31250, 38400, 56000, 57600, 76800, 115200, 230400, 250000, 460800, 921600, 1000000<br><br>Default value: U_CONFIG_DEFAULT_BAUDRATE |

<a name="atw" id="atw"></a>
### **4.1.4 AT&W - Store current configuration**

Store the current configuration to flash


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT&W` | Write the current configuration to flash. The configuration is stored immediately when AT&W is issued. |

<a name="atusyla" id="atusyla"></a>
### **4.1.5 AT+USYLA - Local Address**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYLA=<interface_id>` | Get interface address |
| `AT+USYLA=<interface_id>,<address>` | Set interface address<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USYLA:<address>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| interface\_id | enumerator | Valid values:<br>0: Bluetooth |
| address | mac\_addr | MAC address of the interface id. If the address is set to 000000000000, the local address will be restored to factory-programmed value. The least significant bit of the first octet of the address must be 0. |

<a name="atusyfr" id="atusyfr"></a>
### **4.1.6 AT+USYFR - Factory Restore**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYFR` | The module is completely restored to factory defaults. All settings are reset to default values.<br>All certificates and Bluetooth bonding information will be removed.<br><br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

<a name="atusyds" id="atusyds"></a>
### **4.1.7 AT+USYDS - Default Settings**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYDS` | Reset all settings to default values.<br>Certificates and Bluetooth bonding information will be left untouched.<br><br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

<a name="atusyus" id="atusyus"></a>
### **4.1.8 AT+USYUS - Uart Settings**


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
| flow\_control | integer | 0: (Factory default) No flow control<br>1: Use CTS/RTS flow control<br><br><br>Valid values: 0 or 1 |
| change\_after\_confirm | integer | 0: Switch baudrate after reboot. When set [AT&W](#atw) must be called.<br>1: Switch baudrate directly after status OK have been sent.<br><br><br>Valid values: 0 or 1 |
| baud\_rate | integer | Baudrate<br><br>Valid values: 1200, 2400, 4800, 9600, 14400, 28800, 31250, 38400, 56000, 57600, 76800, 115200, 230400, 250000, 460800, 921600, 1000000<br><br>Default value: U_CONFIG_DEFAULT_BAUDRATE |

<a name="atusyec" id="atusyec"></a>
### **4.1.9 AT+USYEC - Error Code**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYEC?` | Read the last error code |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USYEC:<error_code>` | Latest error code |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| error\_code | integer | Error code |

<a name="atusyee" id="atusyee"></a>
### **4.1.10 AT+USYEE - Extended Error codes on/off**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYEE=<extended_errors>` | Enable or disable extended error codes<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USYEE?` | Read extended error codes enabled/disabled |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USYEE:<extended_errors>` | Extended error codes setting |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| extended\_errors | enumerator | Extended error codes setting<br><br>Valid values:<br>0: (Factory default) Extended error codes will not be displayed<br>1: Extended error code will be displayed on every error |

<a name="ate" id="ate"></a>
### **4.1.11 ATE - Echo On/Off**

This command configures whether or not the module echoes the characters received from the host.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `ATE0` | Set echo off<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `ATE1` | Set echo on<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `ATE?` | Read current echo setting |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<echo_on>` | Current echo setting |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| echo\_on | enumerator | Valid values:<br>0: Module does not echo the characters<br>1: (Factory default) Module echoes the characters |

<a name="ats" id="ats"></a>
### **4.1.12 ATS - S-registers**

Used to set different configuration parameters


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `ATS2=<escape_char>` | Write escape character. This settings change the decimal value of the escape character used by some modes, such as transparent mode for example, to detect an escape sequence and exit.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `ATS2?` | Read escape character |
| `ATS3=<line_term>` | Write line termination character. This setting changes the decimal value of the character recognized by the DCE from the DTE to terminate an incoming command line. It is also generated by the DCE as part of the header, trailer, and terminator for result codes and information text along with the S4 parameter. The previous value of S3 is used to determine the command line termination character for entry of the command line containing the S3 setting command. However, the result code issued shall use the value of S3 as set during the processing of the command line. For example, if S3 was previously set to 13 and the command line "ATS3=30" is issued, the command line shall be terminated with a CR, character (13), but the result code issued will use the character with the ordinal value 30 instead of the CR.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `ATS3?` | Read line termination character |
| `ATS4=<resp_format>` | Write response format character. This setting changes the decimal value of the character generated by the DCE as part of the header, trailer, and terminator for result codes and information text, along with the S3 parameter. If the value of S4 is changed in a command line, the result code issued in response to that command line will use the new value of S4.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `ATS4?` | Read response format character |
| `ATS5=<backspace>` | Writes backspace character. This setting changes the decimal value of the character recognized by the DCE as a request to delete from the command line, the immediately preceding character.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `ATS5?` | Read backspace character |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<escape_char>` | Current escape character |
| `<line_term>` | Current line termination character |
| `<resp_format>` | Current response format character |
| `<backspace>` | Current backspace character |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| line\_term | integer | Command line termination character. Factory default: 13<br><br>Valid values: 0..127 |
| resp\_format | integer | Response format character. Factory default: 10<br><br>Valid values: 0..127 |
| backspace | integer | Backspace character. Factory default: 8<br><br>Valid values: 0..127 |
| escape\_char | integer | Escape character. Factory default: 43<br><br>Valid values: 0..127 |

<a name="atutmes" id="atutmes"></a>
### **4.1.13 AT+UTMES - Transparent mode escape sequence settings**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UTMES=<pre_timeout>,<post_timeout>,<escape_timeout>` | Configures the transparent mode escape sequence settings. |
| `AT+UTMES?` | Reads current transparent mode escape sequence settings. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UTMES:<pre_timeout>,<post_timeout>,<escape_timeout>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| pre\_timeout | integer | Minimum time (ms) of no data activity required before the escape sequence is sent. Factory default: 1000<br><br>Valid values: 50..5000 |
| post\_timeout | integer | Minimum time (ms) of no data activity required after the escape sequence is sent. Factory default: 1000<br><br>Valid values: 50..5000 |
| escape\_timeout | integer | Maximum time interval (ms) between escape characters. Factory default: 200<br><br>Valid values: 50..5000 |

<a name="atusct" id="atusct"></a>
### **4.1.14 AT+USCT - Chip Die Temperature (experimental)**

> **Experimental:** This AT command is experimental and may change or be removed in a future release.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USCT?` | Read chip die temperature. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USCT:<temperature>` | Chip die temperature response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| temperature | integer | Chip die temperature in tenth of Celsius degrees. Divide by 10 to get degrees. |

<a name="bluetooth" id="bluetooth"></a>
# **5 Bluetooth**

Bluetooth commands

NORA-B27 supports up to 0 connections as BLE central and 1 as peripheral.


<a name="u_51-at-commands" id="u_51-at-commands"></a>
## **5.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UBTM](#atubtm) | Bluetooth Mode |
| [AT+UBTDC](#atubtdc) | Bluetooth Disconnect |
| [AT+UBTLN](#atubtln) | Bluetooth Local Name |
| [AT+UBTRSS](#atubtrss) | Bluetooth RSSI |
| [AT+UBTCL](#atubtcl) | Bluetooth Connection List |
| [AT+UBTCST](#atubtcst) | Bluetooth Connection Status |
| [AT+UBTA](#atubta) | Read which advertisements are currently running |
| [AT+UBTADL](#atubtadl) | Bluetooth Advertisement Data Legacy |
| [AT+UBTADLC](#atubtadlc) | Bluetooth Advertising Data Legacy Clear |
| [AT+UBTADE](#atubtade) | Bluetooth Advertising Data Extended |
| [AT+UBTADEC](#atubtadec) | Bluetooth Advertising Data Extended Clear |
| [AT+UBTAE](#atubtae) | Bluetooth Advertise Extended |
| [AT+UBTAED](#atubtaed) | Bluetooth Advertise Extended Disable |
| [AT+UBTASD](#atubtasd) | Bluetooth Advertisement Scan Data |
| [AT+UBTASDC](#atubtasdc) | Bluetooth Scan Data Clear |
| [AT+UBTAL](#atubtal) | Bluetooth Advertise Legacy Enable |
| [AT+UBTALD](#atubtald) | Bluetooth Advertise Legacy Disable |
| [AT+UBTAD](#atubtad) | Bluetooth Directed Advertisement |
| [AT+UBTADD](#atubtadd) | Bluetooth Advertise Directed Disable |
| [AT+UBTCS](#atubtcs) | Bluetooth Connection Settings |
| [AT+UBTALS](#atubtals) | Bluetooth Advertisement Legacy Settings |
| [AT+UBTIOC](#atubtioc) | Bluetooth I/O Capabilities |
| [AT+UBTBSM](#atubtbsm) | Bluetooth Bond Security Mode |
| [AT+UBTPM](#atubtpm) | Bluetooth Pairing Mode |
| [AT+UBTUC](#atubtuc) | Bluetooth User Confirmation |
| [AT+UBTUPE](#atubtupe) | User passkey entry |
| [AT+UBTB](#atubtb) | Bluetooth Bond |
| [AT+UBTUB](#atubtub) | Bluetooth Unbond |
| [AT+UBTBDL](#atubtbdl) | Bluetooth Bonded Devices List |
| [AT+UBTDIS](#atubtdis) | Bluetooth Device Information Service |
| [AT+UBTPHYR](#atubtphyr) | Bluetooth PHY Request |
| [AT+UBTMOP](#atubtmop) | Bluetooth Max Output Power |
| [AT+UBTMOPC](#atubtmopc) | Bluetooth Max Output Power Clear |

<a name="atubtm" id="atubtm"></a>
### **5.1.1 AT+UBTM - Bluetooth Mode**

Set and read Bluetooth Mode.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTM=<mode>` | Set Bluetooth Mode.<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |
| `AT+UBTM?` | Read Bluetooth Mode. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTM:<mode>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mode | enumerator | Valid values:<br>0: Disabled.<br>1: Bluetooth Low Energy Central.<br>In this mode, starting advertisements, direct advertisements and other functions associated<br>with the Peripheral role is not possible.<br><br>2: Bluetooth Low Energy Peripheral.<br>In this mode, initiating connections, discovery and other functions associated with<br>the Central role is not possible.<br><br>3: Bluetooth Low Energy Simultaneous Central and Peripheral. This is the factory default. |

<a name="atubtdc" id="atubtdc"></a>
### **5.1.2 AT+UBTDC - Bluetooth Disconnect**

Used to close an ACL connection.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTDC=<conn_handle>` | Close an existing ACL connection. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |

<a name="atubtln" id="atubtln"></a>
### **5.1.3 AT+UBTLN - Bluetooth Local Name**

Set the BLE local name used in the default scan response data and in the Generic Access Profile service.


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
| device\_name | string | Default local name is the MODEL-xxxxxx where xxxxxx are the last 3 bytes of the device MAC address in hexadecimal format. If the local name is set to "" it is cleared but will revert to the default name after a restart.<br><br>Valid length: 0..29 |

<a name="atubtrss" id="atubtrss"></a>
### **5.1.4 AT+UBTRSS - Bluetooth RSSI**

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

<a name="atubtcl" id="atubtcl"></a>
### **5.1.5 AT+UBTCL - Bluetooth Connection List**

List all active Bluetooth low energy ACl connections.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCL` | List all Bluetooth low energy ACL connections. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTCL:<conn_handle>,<bd_addr>` | Sent for every connection. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtcst" id="atubtcst"></a>
### **5.1.6 AT+UBTCST - Bluetooth Connection Status**

Read negotiated properties of a Bluetooth low energy ACL connection.
Some of the properties are a result of negotiation when a connections is set up, and this command gives the possibility
to see what properties the connection actually uses.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCST=<conn_handle>` | Read all properties of an existing Bluetooth low energy ACL connection. |
| `AT+UBTCST=<conn_handle>,<prop_id>` | Read a specific property of an existing Bluetooth low energy ACL connection. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTCST:<prop_id>,<status_val>` | One response for each prop_id. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| status\_val | integer | Value of the preceding property. |
| prop\_id | enumerator | Valid values:<br>0: Connection interval used on this connection.<br> Range: 6 to 3200<br> Time = status_val * 1.25 ms<br> Time range: 7.5 ms to 4000 ms<br><br>1: Peripheral latency for the connection in number of connection events. Range: 0 to 499<br>2: Supervision timeout (in ms) for this connections. Range: 100 ms to 32000 ms<br>3: MTU size for this connections.<br>4: Data Channel TX PDU Payload Length.<br>5: Data Channel RX PDU Payload Length.<br>6: Data Length Extension state. 0: Data Length Extension Off \ 1: Data Length Extension On<br>7: Local role in this connection. 1: Low Energy Central \ 2: Low Energy Peripheral<br>8: TX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: Coded<br><br>9: RX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: Coded<br> |
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |

<a name="atubta" id="atubta"></a>
### **5.1.7 AT+UBTA - Read which advertisements are currently running**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTA?` | Read the current advertisements |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTA:<legacy_adv>,<directed_adv>,<extended_adv_list>` | Successful read |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| legacy\_adv | enumerator | Valid values:<br>0: Legacy Advertisement Not Running<br>1: Legacy Advertisement Running |
| directed\_adv | enumerator | Valid values:<br>0: Directed Advertisement Not Running<br>1: Directed Advertisement Running |
| extended\_adv\_list | int\_list | List of indexes currently being used for extended advertisements<br><br>Valid length: 0 or 1 |

<a name="atubtadl" id="atubtadl"></a>
### **5.1.8 AT+UBTADL - Bluetooth Advertisement Data Legacy**

Command for setting custom legacy advertise data in Bluetooth low energy. Maximum of 28 bytes.
Any custom advertising data will be appended to the default mandatory flags field.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADL=<adv_data>` | Write custom advertising data.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTADL?` | Read custom advertising data. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTADL:<adv_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| adv\_data | byte\_array | Valid length: 3..28 |

<a name="atubtadlc" id="atubtadlc"></a>
### **5.1.9 AT+UBTADLC - Bluetooth Advertising Data Legacy Clear**

Clear the custom advertise data, i.e.use the default value when advertising


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADLC` | Clear the custom legacy advertise data. |

<a name="atubtade" id="atubtade"></a>
### **5.1.10 AT+UBTADE - Bluetooth Advertising Data Extended**

Command for setting extended advertising data in Bluetooth low energy. Maximum of 226 bytes.
Any custom advertising data will be appended to the default mandatory flags field.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADE=<index>,<adv_data>` | Write custom advertising data for configuration index.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTADE=<index>` | Read custom advertising data for configuration index. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTADE:<index>,<adv_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| index | integer | Valid values: 0 only |
| adv\_data | byte\_array | Valid length: 3..226 |

<a name="atubtadec" id="atubtadec"></a>
### **5.1.11 AT+UBTADEC - Bluetooth Advertising Data Extended Clear**

Clear the custom extended advertise data, i.e. use to the default value during extended advertising


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADEC=<index>` | Clear the extended advertise data for the specified index. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| index | integer | Valid values: 0 only |

<a name="atubtae" id="atubtae"></a>
### **5.1.12 AT+UBTAE - Bluetooth Advertise Extended**

Start extended advertisement for the specified configuration


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAE=<indexes_to_advertise>` | Start advertisements for the specified index(es).<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| indexes\_to\_advertise | int\_list | Valid length: 1 or 2 |

<a name="atubtaed" id="atubtaed"></a>
### **5.1.13 AT+UBTAED - Bluetooth Advertise Extended Disable**

Stop extended advertisements


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAED` | Stop any running extended advertisements |
| `AT+UBTAED=<index>` | Stop extended advertisements for the specified index<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| index | integer | Valid values: 0 only |

<a name="atubtasd" id="atubtasd"></a>
### **5.1.14 AT+UBTASD - Bluetooth Advertisement Scan Data**

Command for setting custom scan response data in Bluetooth low energy. Any custom scan response data will override the default scan response data. By default, the local name is part of the scan response data.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTASD=<scan_rsp_data>` | Write custom scan response data.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTASD?` | Read custom scan response data. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTASD:<scan_rsp_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| scan\_rsp\_data | byte\_array | Valid length: 1..31 |

<a name="atubtasdc" id="atubtasdc"></a>
### **5.1.15 AT+UBTASDC - Bluetooth Scan Data Clear**

Clear the custom scan response data, i.e. use the default value when advertising


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTASDC` | Clear the custom scan response data. |

<a name="atubtal" id="atubtal"></a>
### **5.1.16 AT+UBTAL - Bluetooth Advertise Legacy Enable**

Start legacy advertisement if not started


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAL` | Start legacy advertisement if not started.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="atubtald" id="atubtald"></a>
### **5.1.17 AT+UBTALD - Bluetooth Advertise Legacy Disable**

Stop legacy advertisement if started


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTALD` | Stop legacy advertisement if started.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="atubtad" id="atubtad"></a>
### **5.1.18 AT+UBTAD - Bluetooth Directed Advertisement**

Start a directed advertisement to a given Bluetooth Address


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAD=<bd_addr>[,<timeout>]` | Starts directed advertisements to Bluetooth Address.<br>By default the timeout is 1280 ms, and uses High Duty Cycle Advertising. A timeout greater than this will result in<br>Low Duty Cycle Advertising as High Duty Cycle Advertising has a limited use of only 1280 ms. Setting timeout to 0 will let the<br>device advertise indefinitely in Low Duty Cycle mode.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| timeout | integer | Timeout for Directed Advertisements.<br><br>Default value: 1280 |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtadd" id="atubtadd"></a>
### **5.1.19 AT+UBTADD - Bluetooth Advertise Directed Disable**

Stop any ongoing directed advertisement


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTADD` | Stop directed advertisements.<br> |

<a name="atubtcs" id="atubtcs"></a>
### **5.1.20 AT+UBTCS - Bluetooth Connection Settings**

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
| connection\_interval\_minimum | integer | Connection interval minimum (must be <= Connection interval maximum). Final results will be a result of negotiation between devices.<br> Default: 24.<br> Calculation: connection_interval_minimum * 1.25. ms<br><br>Valid values: 6..3200<br><br>Default value: 24 |
| connection\_interval\_maximum | integer | Connection interval maximum (must be >= Connection interval minimum). Final results will be a result of negotiation between devices.<br> Default: 40.<br> Calculation: connection_interval_maximum * 1.25 ms.<br><br>Valid values: 6..3200<br><br>Default value: 40 |
| connection\_peripheral\_latency | integer | Connection peripheral latency.<br> Default: 0<br> Calculation: Number of connection events.<br><br>Valid values: 0..500<br><br>Default value: 0 |
| connection\_linkloss\_timeout | integer | Connection linkloss timeout.<br> Default: 2000<br> Calculation: connection_linkloss_timeout ms<br><br>Valid values: 100..32000<br><br>Default value: 2000 |
| preferred\_tx\_phy | integer | Preferred Transmitter PHY<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br>Bit 3: Coded PHY type. 0: Use S8 coding, 1: Use S2 coding<br><br>Valid values: 0..15<br><br>Default value: 0 |
| preferred\_rx\_phy | integer | Preferred PHY for Receiver<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br><br>Valid values: 0..15<br><br>Default value: 0 |
| param | enumerator | Connection parameter.<br><br>Valid values:<br>0: Connection interval minimum.<br>1: Connection interval maximum.<br>2: Connection peripheral latency.<br>3: Connection linkloss timeout.<br>4: Preferred Transmitter PHY<br>5: Preferred Receiver PHY |
| value | integer | Value of connection parameter.<br><br>Valid values: 0..65535 |

<a name="atubtals" id="atubtals"></a>
### **5.1.21 AT+UBTALS - Bluetooth Advertisement Legacy Settings**

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
| advertisement\_interval\_minimum | integer | Advertising interval minimum (must be <= Advertising interval maximum. <br> Default: 1600.<br> Calculation: advertisement_interval_minimum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 1600 |
| advertisement\_interval\_maximum | integer | Advertising interval maximum (must be >= Advertising interval minimum. <br> Default: 2000.<br> Calculation: advertisement_interval_maximum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 2000 |

<a name="atubtioc" id="atubtioc"></a>
### **5.1.22 AT+UBTIOC - Bluetooth I/O Capabilities**

Set Bluetooth I/O Capabilities, this impacts the possible bonding procedure between devices.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTIOC=<io_cap>` | Set I/O Capabilities<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTIOC?` | Read I/O Capabilities |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTIOC:<io_cap>` | Successful read response for AT+UBTIOC?. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| io\_cap | enumerator | Valid values:<br>0: Set I/O Capabilities to No Input No Output.<br>1: Set I/O Capabilities to Display Only.<br>2: Set I/O Capabilities to Display Yes/No<br>3: Set I/O Capabilities to Keyboard Only.<br>4: Set I/O Capabilities to Keyboard Display.<br><br>Default value: 0 |

<a name="atubtbsm" id="atubtbsm"></a>
### **5.1.23 AT+UBTBSM - Bluetooth Bond Security Mode**

Set the minimum security mode required when bonding. This command works together with [AT+UBTIOC](#atubtioc) to determine the bonding procedure used.
The module will try to use the highest level possible based on the settings of this command, [AT+UBTIOC](#atubtioc) and the capabilities of the remote device.
If the remote device does not support the required security level, the bonding procedure will fail.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTBSM=<security_mode>` | Writes the security mode<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTBSM?` | Reads the security mode |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTBSM:<security_mode>` | Successful read response for AT+UBTBSM? |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| security\_mode | enumerator | Valid values:<br>0: Security not required. No encryption enforced.<br>1: Require at least unauthenticated bonding.<br>2: Require authenticated bonding. No secure connections.<br>3: Require authenticated bonding. Support secure connections. Fallback to simple pairing if the remote side does not support secure connections.<br>4: Require authenticated bonding. Strictly uses secure connections.<br><br>Default value: 0 |

<a name="atubtpm" id="atubtpm"></a>
### **5.1.24 AT+UBTPM - Bluetooth Pairing Mode**

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

<a name="atubtuc" id="atubtuc"></a>
### **5.1.25 AT+UBTUC - Bluetooth User Confirmation**

The user confirmation is used together with IO capability DisplayYesNo to respond to a user confirmation request ([+UEBTUC](#uebtuc)). The command shall be used only after [+UEBTUC](#uebtuc) has been received.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTUC=<bd_addr>,<confirm>` | Respond to +UEUBTUC and confirm/deny bonding. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| confirm | enumerator | Valid values:<br>0: Deny bonding.<br>1: Confirm bonding. |

<a name="atubtupe" id="atubtupe"></a>
### **5.1.26 AT+UBTUPE - User passkey entry**

The user passkey entry is used together with IO capability KeyboardOnly to respond on a user passkey entry request ([+UEBTUPE](#uebtupe)). This command shall be used only after [+UEBTUPE](#uebtupe) has been received.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTUPE=<bd_addr>,<confirm>[,<passkey>]` | Respond to +UEBTUPE event and confirm/deny bonding. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| passkey | integer | Passkey used to confirm bonding, if confirm is set to no, this can be omitted.<br><br>Valid values: 0..999999 |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| confirm | enumerator | Valid values:<br>0: Deny bonding.<br>1: Confirm bonding. |

<a name="atubtb" id="atubtb"></a>
### **5.1.27 AT+UBTB - Bluetooth Bond**

Performs a GAP bond procedure with another Bluetooth device. For some I/O Capabilities, user interaction is required during the bonding procedure. The procedure to use is determined by the I/O Capabilities and security mode. The maximum number of stored bonds is 10 for NORA-B27.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTB=<bd_addr>` | Initiate bonding. To perform the bonding, the remote device must be in a pairable and connectable mode. Bond Event [+UEBTB](#uebtb) is generated once the bond is complete. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtub" id="atubtub"></a>
### **5.1.28 AT+UBTUB - Bluetooth Unbond**

Unbond from a previously bonded device.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTUB=<bd_addr>` | Removes a single previously bonded device. |
| `AT+UBTUB` | Removes all previously bonded devices. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |


**Notes**<br>
These AT commands will remove the bond from the local device only.

<a name="atubtbdl" id="atubtbdl"></a>
### **5.1.29 AT+UBTBDL - Bluetooth Bonded Devices List**

Reads the list of bonded devices.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTBDL` | Read list of bonded devices. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTBDL:<bd_addr>` | This response is sent for every found device. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtdis" id="atubtdis"></a>
### **5.1.30 AT+UBTDIS - Bluetooth Device Information Service**

Write and read the module's Device Information Service (DIS) characteristics.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTDIS=<char_id>,<char_value>` | Set a characteristic value.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTDIS=<char_id>` | Read a characteristic value. |
| `AT+UBTDIS?` | Read all individual characteristic of the Device Information Service characteristics. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTDIS:<char_id>,<char_value>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| char\_id | enumerator | Valid values:<br>0: Manufacturer name string. Maximum length of the custom string is 31 characters.<br>1: Model name string. Maximum length of the custom string is 20 characters.<br>2: Firmware revision string. Maximum length of the custom string is 20 characters.<br>3: Software revision string. Maximum length of the custom string is 20 characters. |
| char\_value | string | Value of Device Information Service characteristic. |

<a name="atubtphyr" id="atubtphyr"></a>
### **5.1.31 AT+UBTPHYR - Bluetooth PHY Request**

Request a new PHY configuration for a connection. If tx PHY or rx PHY is 0, the module will select PHYs
based on the peer requirements on that specific direction. If the peer does not support the PHY update procedure,
then the resulting [+UEBTPHYU](#uebtphyu) event will have a error status other than success.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTPHYR=<conn_handle>,<tx_phy>,<rx_phy>` | Requests a Bluetooth Low Energy PHY update. |
| `AT+UBTPHYR=<conn_handle>` | Reads current PHYs for a connection. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTPHYR:<conn_handle>,<tx_phy>,<rx_phy>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| tx\_phy | integer | Requested PHY for Transmitter:<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br>Bit 3: Coded PHY type. 0: Use S8 coding, 1: Use S2 coding<br><br>Valid values: 0..15 |
| rx\_phy | integer | Requested PHY for Receiver<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br><br>Valid values: 0..7 |

<a name="atubtmop" id="atubtmop"></a>
### **5.1.32 AT+UBTMOP - Bluetooth Max Output Power**

Set or read the Bluetooth Max Output Power for all operations including advertising, scanning, and connections.
The output power is specified in dBm.
The valid range is from -20 dBm to +20 dBm but the actual supported range may vary between different products.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTMOP=<int_dBm>` | Set the Bluetooth Max Output Power level.<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |
| `AT+UBTMOP?` | Read current Bluetooth Max Output Power level. Will return error if the Bluetooth Max Output Power has not been set<br>and the default power level is used.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTMOP:<int_dBm>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| int\_dBm | integer | TX power level in dBm, integer part.<br><br>Valid values: -20..20 |

<a name="atubtmopc" id="atubtmopc"></a>
### **5.1.33 AT+UBTMOPC - Bluetooth Max Output Power Clear**

Clear any previously set Bluetooth Max Output Power level, and revert to the default Max Output Power level.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTMOPC` | Clear any previously set max Bluetooth Max Output Power level.<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

<a name="u_52-unsolicited-response-codes" id="u_52-unsolicited-response-codes"></a>
## **5.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEBTC](#uebtc) | Event Bluetooth Connected |
| [+UEBTDC](#uebtdc) | Event Bluetooth Disconnected |
| [+UEBTB](#uebtb) | Event Bluetooth Bond status |
| [+UEBTUC](#uebtuc) | Event Bluetooth User Confirmation |
| [+UEBTUPD](#uebtupd) | Event Bluetooth Passkey entry |
| [+UEBTUPE](#uebtupe) | Event Bluetooth Passkey request |
| [+UEBTPHYU](#uebtphyu) | Event Bluetooth PHY update |

<a name="uebtc" id="uebtc"></a>
### **5.2.1 +UEBTC - Event Bluetooth Connected**

Event indicating successful Bluetooth connection.


**Syntax**<br>
```+UEBTC:<conn_handle>,<bd_addr>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="uebtdc" id="uebtdc"></a>
### **5.2.2 +UEBTDC - Event Bluetooth Disconnected**

Event indicating a disconnected Bluetooth connection.


**Syntax**<br>
```+UEBTDC:<conn_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |

<a name="uebtb" id="uebtb"></a>
### **5.2.3 +UEBTB - Event Bluetooth Bond status**

Event indicates that a bonding procedure is completed.


**Syntax**<br>
```+UEBTB:<bd_addr>,<bond_status>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| bond\_status | enumerator | Bonding status<br><br>Valid values:<br>0: Bonding procedure succeeded.<br>1: Bonding procedure failed due to page timeout.<br>2: Bonding failed because of authentication or pairing failed. This could be due to incorrect PIN/passkey.<br>3: Bonding failed because the protection against Man-In-The-Middle attack could not be guaranteed; the generated link key was too weak.<br>4: Bonding failed because peer have lost the bonding info. Use [AT+UBTUB](#atubtub) to delete the local bond to allow re-bonding. |

<a name="uebtuc" id="uebtuc"></a>
### **5.2.4 +UEBTUC - Event Bluetooth User Confirmation**

This event is used while bonding with IO capability DisplayYesNo. This event indicates that the user confirmation of a numeric value is required.


**Syntax**<br>
```+UEBTUC:<bd_addr>,<numeric_value>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| numeric\_value | integer | Numeric value.<br><br>Valid values: 0..999999 |

<a name="uebtupd" id="uebtupd"></a>
### **5.2.5 +UEBTUPD - Event Bluetooth Passkey entry**

This event is used to indicate to the user that a passkey has to be entered on the remote device during a bonding procedure with the IO capability DisplayOnly.


**Syntax**<br>
```+UEBTUPD:<bd_addr>,<numeric_value>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| numeric\_value | integer | Numeric value.<br><br>Valid values: 0..999999 |

<a name="uebtupe" id="uebtupe"></a>
### **5.2.6 +UEBTUPE - Event Bluetooth Passkey request**

This event is used during bonding with IO capability KeyboardOnly to indicate that a passkey is required from the user. User should respond to this event with the [AT+UBTUPE](#atubtupe) command.


**Syntax**<br>
```+UEBTUPE:<bd_addr>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="uebtphyu" id="uebtphyu"></a>
### **5.2.7 +UEBTPHYU - Event Bluetooth PHY update**

This event informs the result of a PHY update procedure. It may be generated as a result of the command [AT+UBTPHYR](#atubtphyr) or as a successful event, if the operation has been initiated by the remote peer.


**Syntax**<br>
```+UEBTPHYU:<conn_handle>,<phy_status>,<tx_phy>,<rx_phy>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| phy\_status | integer | Bluetooth status codes:<br>0: Success<br>0x01-0xFF: Error, see Bluetooth Core Specifications, Vol 2, Part D.<br><br><br>Valid values: 0..255 |
| tx\_phy | integer | Requested PHY for Transmitter:<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br>Bit 3: Coded PHY type. 0: Use S8 coding, 1: Use S2 coding<br><br>Valid values: 0..15 |
| rx\_phy | integer | Requested PHY for Receiver<br>0: Let other side decide<br>OR a bit field with bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY<br><br>Valid values: 0..7 |

<a name="gatt-server" id="gatt-server"></a>
# **6 GATT Server**

GATT Server

<a name="u_61-at-commands" id="u_61-at-commands"></a>
## **6.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UBTGS](#atubtgs) | GATT Service define |
| [AT+UBTGC](#atubtgc) | GATT Characteristic define |
| [AT+UBTGHCC](#atubtghcc) | GATT Host Controlled Characteristic |
| [AT+UBTGD](#atubtgd) | GATT Descriptor define |
| [AT+UBTGSA](#atubtgsa) | GATT Service Activate |
| [AT+UBTGRRR](#atubtgrrr) | GATT Read Request Respond |
| [AT+UBTGNS](#atubtgns) | GATT Notification Send |
| [AT+UBTGIS](#atubtgis) | GATT Indication Send |
| [AT+UBTGAV](#atubtgav) | GATT Attribute Value |
| [AT+UBTGRRRE](#atubtgrrre) | GATT Read Request Respond with error code |
| [AT+UBTGWRE](#atubtgwre) | GATT Write Respond with Error code |
| [AT+UBTGWRR](#atubtgwrr) | GATT Write Request Respond |

<a name="atubtgs" id="atubtgs"></a>
### **6.1.1 AT+UBTGS - GATT Service define**

Command to define a GATT service according to a 16-bit Service Assigned Number from Bluetooth SIG or a 128-bit user defined service number.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGS=<uuid>` | Defines a service. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGS:<ser_handle>` | Successful write response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| uuid | byte\_array | UUID of service. This can be either 16 bit or 128 bit. |
| ser\_handle | integer | Handle of the created service. |

<a name="atubtgc" id="atubtgc"></a>
### **6.1.2 AT+UBTGC - GATT Characteristic define**

Command to add a GATT characteristic to the most recent GATT service record created with [AT+UBTGS](#atubtgs).


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGC=<uuid>,<properties>,<read_security>,<write_security>,<value>[,<max_length>]` | Create a new characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGC:<value_handle>,<cccd_handle>` | Successful write response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| uuid | byte\_array | UUID of characteristic. This can be either 16 bit or 128 bit. |
| value | byte\_array | Default characteristic value before any value is pushed to it. A characteristic value can be 244 bytes long. |
| max\_length | integer | Maximum length of the characteristic in bytes. The maximum value is 244 bytes.<br><br>Valid values: 1..244 |
| value\_handle | integer | Added characteristic handle. |
| cccd\_handle | integer | CCCD characteristic handle. This value is zero if there is no CCCD. |
| properties | byte\_array | Property value (a bit field):<br>Broadcast: 0x01 - If set, it allows broadcasts of the Characteristic Value using Characteristic Configuration Descriptor.<br>Read: 0x02 - If set, it allows reads of the Characteristic Value.<br>Write Without Response: 0x04 - If set, it allows writing of the Characteristic Value without response.<br>Write: 0x08 - If set, it allows writing of the Characteristic Value with response.<br>Notify: 0x10 - If set, it allows notifications of a characteristic value.<br>Indicate: 0x20 - If set, it allows indication of a characteristic value with acknowledgement.<br>Authenticated Signed Writes: 0x40 - If set, it allows signed writes to the characteristic value.<br>Reserved Bit: 0x80 - Do not use. Reserved for future use.<br><br><br>Valid length: 1 only |
| read\_security | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |
| write\_security | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |

<a name="atubtghcc" id="atubtghcc"></a>
### **6.1.3 AT+UBTGHCC - GATT Host Controlled Characteristic**

Create a new host controlled characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGHCC=<uuid>,<properties>,<read_security>,<write_security>` | Define a characteristic. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGHCC:<value_handle>,<cccd_handle>` | Successful write response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| uuid | byte\_array | UUID of characteristic. This can be either 16 bit or 128 bit. |
| value\_handle | integer | Value handle of the added characteristic. |
| cccd\_handle | integer | Client Characteristic Configuration Descriptor (CCCD) handle of the added characteristic. This value is zero if there is no CCCD. |
| properties | byte\_array | Property value (a bit field):<br>Broadcast: 0x01 - If set, it allows broadcasts of the Characteristic Value using Characteristic Configuration Descriptor.<br>Read: 0x02 - If set, it allows reads of the Characteristic Value.<br>Write Without Response: 0x04 - If set, it allows writing of the Characteristic Value without response.<br>Write: 0x08 - If set, it allows writing of the Characteristic Value with response.<br>Notify: 0x10 - If set, it allows notifications of a characteristic value.<br>Indicate: 0x20 - If set, it allows indication of a characteristic value with acknowledgement.<br>Authenticated Signed Writes: 0x40 - If set, it allows signed writes to the characteristic value.<br>Reserved Bit: 0x80 - Do not use. Reserved for future use.<br><br><br>Valid length: 1 only |
| read\_security | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |
| write\_security | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |

<a name="atubtgd" id="atubtgd"></a>
### **6.1.4 AT+UBTGD - GATT Descriptor define**

Define a vendor defined descriptor. Standard Bluetooth low energy descriptors such as CCCD are created while creating the characteristic in [AT+UBTGC](#atubtgc) command.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGD=<uuid>,<read_security>,<write_security>,<value>[,<max_length>]` | Define descriptor. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGD:<desc_handle>` | Successful write response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| uuid | byte\_array | UUID of characteristic. This can be either 16 bit or 128 bit. |
| value | byte\_array | Descriptor value. This can be 23 bytes long. |
| max\_length | integer | Maximum length of the descriptor in bytes. The maximum value is 23 bytes.<br><br>Valid values: 1..23 |
| desc\_handle | integer | Handle of the created descriptor. |
| read\_security | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |
| write\_security | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |

<a name="atubtgsa" id="atubtgsa"></a>
### **6.1.5 AT+UBTGSA - GATT Service Activate**

Activate the service defined with the [AT+UBTGS](#atubtgs) command. After this command is issued, it is not possible to add more characteristics or descriptors to the service.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGSA` | Activate current defined service. |

<a name="atubtgrrr" id="atubtgrrr"></a>
### **6.1.6 AT+UBTGRRR - GATT Read Request Respond**

Respond to an unsolicited request to read (see [+UEBTGRR](#uebtgrr)) from a remote GATT client.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGRRR=<conn_handle>,<value>` | Responds to read request. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of the connected device. |
| value | byte\_array | Characteristic value. This can be 244 bytes long. |

<a name="atubtgns" id="atubtgns"></a>
### **6.1.7 AT+UBTGNS - GATT Notification Send**

Send notifications to a remote client. This also updates the value of the characteristic.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGNS=<conn_handle>,<char_handle>,<value>` | Send notification |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of the connected device. |
| char\_handle | integer | Characteristic value handle. |
| value | byte\_array | Characteristic value. The maximum length is the current MTU size - 3. |

<a name="atubtgis" id="atubtgis"></a>
### **6.1.8 AT+UBTGIS - GATT Indication Send**

Send indication to a remote client. This also updates the value of the characteristic.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGIS=<conn_handle>,<char_handle>,<value>` | Send notification |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of the connected device. |
| char\_handle | integer | Characteristic value handle. |
| value | byte\_array | Characteristic value. The maximum length is the current MTU size - 3. |

<a name="atubtgav" id="atubtgav"></a>
### **6.1.9 AT+UBTGAV - GATT Attribute Value**

Update the value of an attribute. In case of characteristics which allow indications and notifications, this command will update the value without sending any indications or notifications to the remote side.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGAV=<attr_handle>,<value>` | Set attribute value. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| attr\_handle | integer | Attribute handle. |
| value | byte\_array | Characteristic value. This can be 244 bytes long. |

<a name="atubtgrrre" id="atubtgrrre"></a>
### **6.1.10 AT+UBTGRRRE - GATT Read Request Respond with error code**

Respond to read request with application error code.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGRRRE=<conn_handle>,<error_code>` | Respond with error code. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of connected device. |
| error\_code | byte\_array | Application error code. Allowed value range: 0x80-0x9F<br><br>Valid length: 1 only |

<a name="atubtgwre" id="atubtgwre"></a>
### **6.1.11 AT+UBTGWRE - GATT Write Respond with Error code**

Respond to write operation with application error code.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGWRE=<conn_handle>,<error_code>` | Respond with error code. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of connected device. |
| error\_code | byte\_array | Application error code. Allowed value range: 0x80-0x9F<br><br>Valid length: 1 only |

<a name="atubtgwrr" id="atubtgwrr"></a>
### **6.1.12 AT+UBTGWRR - GATT Write Request Respond**

Accept write request from GATT client.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGWRR=<conn_handle>` | Respond to write request. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of connected device. |

<a name="u_62-unsolicited-response-codes" id="u_62-unsolicited-response-codes"></a>
## **6.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEBTGCW](#uebtgcw) | Event GATT Server Write |
| [+UEBTGRR](#uebtgrr) | Event GATT Server Read Response |
| [+UEBTGIC](#uebtgic) | Event GATT Server Indication Confirmation |

<a name="uebtgcw" id="uebtgcw"></a>
### **6.2.1 +UEBTGCW - Event GATT Server Write**

Unsolicited response code for GATT Server. This event occurs when a remote client writes to an attribute.


**Syntax**<br>
```+UEBTGCW:<conn_handle>,<value_handle>,<value>,<options>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP connection handle. |
| value\_handle | integer | Characteristic value handle. |
| value | byte\_array | The data as hex string. For example, 070809AABBCC |
| options | enumerator | Valid values:<br>0: Write without Response performed<br>1: Write with Response performed<br>2: Write long performed |

<a name="uebtgrr" id="uebtgrr"></a>
### **6.2.2 +UEBTGRR - Event GATT Server Read Response**

Unsolicited response code for GATT Server. This event occurs when a remote client reads an attribute over the air. The event should be responded with [AT+UBTGRRR](#atubtgrrr).


**Syntax**<br>
```+UEBTGRR:<conn_handle>,<value_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Handle of the connected device. |
| value\_handle | integer | Handle of the characteristic value. |

<a name="uebtgic" id="uebtgic"></a>
### **6.2.3 +UEBTGIC - Event GATT Server Indication Confirmation**

Unsolicited response code for GATT Server. This event occurs when a remote GATT client acknowledges the receipt of an indication message sent using [AT+UBTGIS](#atubtgis).


**Syntax**<br>
```+UEBTGIC:<conn_handle>,<char_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connected device handle. |
| char\_handle | integer | Characteristic value handle. |

<a name="sps" id="sps"></a>
# **7 SPS**

SPS - Serial Port Service

<a name="u_71-at-commands" id="u_71-at-commands"></a>
## **7.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+USPS](#atusps) | SPS - Enable/Disable Service |
| [AT+USPSWS](#atuspsws) | SPS Write String |
| [AT+USPSWB](#atuspswb) | SPS Write Binary |
| [AT+USPSRM](#atuspsrm) | SPS Receive Mode |
| [AT+USPSRS](#atuspsrs) | SPS Read String |
| [AT+USPSRB](#atuspsrb) | SPS Read Binary |

<a name="atusps" id="atusps"></a>
### **7.1.1 AT+USPS - SPS - Enable/Disable Service**

Enable or disable the SPS service. SPS Service will use the security mode set in [AT+UBTBSM](#atubtbsm)


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPS=<service_option>` | Enables or disable the SPS Service.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USPS?` | Read if the SPS service is enabled or disabled. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPS:<service_option>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| service\_option | enumerator | Valid values:<br>0: This option disables the SPS service after saving the configuration and restarting the device. (Default)<br>1: This option enables the SPS service directly.<br>If this option is set, and the configuration is saved,<br>SPS will be enabled after reboot.<br> |

<a name="atuspsws" id="atuspsws"></a>
### **7.1.2 AT+USPSWS - SPS Write String**

Write to a peer through SPS


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPSWS=<conn_handle>,<string_data>` | Write SPS data |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPSWS:<conn_handle>,<written_length>` | Successful write response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer which has SPS enabled |
| string\_data | string | Data encoded as ascii chars.<br><br>Valid length: 1..1000 |
| written\_length | integer | Data length that was written. |

<a name="atuspswb" id="atuspswb"></a>
### **7.1.3 AT+USPSWB - SPS Write Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPSWB=<conn_handle>{binary_data}` | Writes the specified amount of data to the specified SPS connection in binary mode. Max 1000 bytes.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPSWB:<conn_handle>,<written_length>` | Successful write response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer which has SPS enabled |
| binary\_data | binary | The data to write. |
| written\_length | integer | Data length that was written. |

<a name="atuspsrm" id="atuspsrm"></a>
### **7.1.4 AT+USPSRM - SPS Receive Mode**


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
| read\_mode | enumerator | Modes to read data in AT<br><br>Valid values:<br>0: Buffered mode<br>1: Direct String mode<br>2: Direct Binary Mode |

<a name="atuspsrs" id="atuspsrs"></a>
### **7.1.5 AT+USPSRS - SPS Read String**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPSRS=<conn_handle>,<length>` | Reads the specified amount of data from given connection handle.<br>Note that the data should include no null terminator characters.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPSRS:<conn_handle>,<length>,<string_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| length | integer | Data bytes to read.<br><br>Valid values: 0..1000 |
| conn\_handle | integer | Connection handle of remote peer |
| string\_data | string | SPS data in string format |

<a name="atuspsrb" id="atuspsrb"></a>
### **7.1.6 AT+USPSRB - SPS Read Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPSRB=<conn_handle>,<length>` | Reads the specified amount of data from the specified connection handle in binary mode.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPSRB:<conn_handle>{binary_data}` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| length | integer | Data bytes to read.<br><br>Valid values: 0..1000 |
| binary\_data | binary | The available data. Please note that the number of bytes may be less than requested. |
| conn\_handle | integer | Connection handle of remote peer |

<a name="u_72-unsolicited-response-codes" id="u_72-unsolicited-response-codes"></a>
## **7.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UESPSC](#uespsc) | Event SPS Connection |
| [+UESPSDC](#uespsdc) | Event SPS Disconnection |
| [+UESPSDS](#uespsds) | Event SPS Data String |
| [+UESPSDB](#uespsdb) | Event SPS Data Binary |
| [+UESPSDA](#uespsda) | Event SPS Data Available |

<a name="uespsc" id="uespsc"></a>
### **7.2.1 +UESPSC - Event SPS Connection**

Event response for SPS Connect. Upon a successful SPS connection, conn_handle will contain the connection handle of the remote peer.


**Syntax**<br>
```+UESPSC:<conn_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |

<a name="uespsdc" id="uespsdc"></a>
### **7.2.2 +UESPSDC - Event SPS Disconnection**

Event response for SPS Connect. Upon a SPS disconnection, conn_handle will contain the connection handle of the remote peer.


**Syntax**<br>
```+UESPSDC:<conn_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |

<a name="uespsds" id="uespsds"></a>
### **7.2.3 +UESPSDS - Event SPS Data String**

Unsolicited event containing SPS data as a string received from remote peer.


**Syntax**<br>
```+UESPSDS:<conn_handle>,<string_data>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |
| string\_data | string | SPS data in string format |

<a name="uespsdb" id="uespsdb"></a>
### **7.2.4 +UESPSDB - Event SPS Data Binary**

Unsolicited event containing SPS data in binary format.


**Syntax**<br>
```+UESPSDB:<conn_handle>{binary_data}```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The received data. |
| conn\_handle | integer | Connection handle of remote peer |

<a name="uespsda" id="uespsda"></a>
### **7.2.5 +UESPSDA - Event SPS Data Available**

Unsolicited event containing the number of received bytes to read.


**Syntax**<br>
```+UESPSDA:<conn_handle>,<number_bytes>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| number\_bytes | integer | Number of bytes available to read. |
| conn\_handle | integer | Connection handle of remote peer |

<a name="power" id="power"></a>
# **8 Power**

<a name="u_81-at-commands" id="u_81-at-commands"></a>
## **8.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UPMDS](#atupmds) | Power Management Deep Sleep |
| [AT+UPMS](#atupms) | Power Management Sleep |

<a name="atupmds" id="atupmds"></a>
### **8.1.1 AT+UPMDS - Power Management Deep Sleep**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UPMDS` | Enter Deep Sleep Mode with GPIO wakeup. |
| `AT+UPMDS=<wakeup_mode>` | Enter Deep Sleep Mode with specified wakeup mode. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wakeup\_mode | enumerator | Selects how to wake up from deep sleep.<br><br>Valid values:<br>0: Wakeup by pulling the module wakeup pin low.<br>1: Wakeup by module reset pin.<br>2: Wakeup by module UART RX pin.<br><br>Default value: 0 |

<a name="atupms" id="atupms"></a>
### **8.1.2 AT+UPMS - Power Management Sleep**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UPMS` | Enters sleep mode. During this mode connection will be kept and the host continues to receive events from the module, but the module will not respond to any AT commands.<br>On connection event, module will wake up, send URC, and go back to sleep.<br>To exit sleep mode, pull WAKE_UP GPIO low or send a character on the UART and wait 50ms.<br> |

<a name="transparent" id="transparent"></a>
# **9 Transparent**

Transparent Mode AT commands. In transparent mode all data that is sent from the host to the UART is
forwarded to the socket or SPS link that is configured for transparent mode, and the all data that arrives
on this link is sent to the UART.
Transparent mode is limited to one link at a time.


<a name="u_91-at-commands" id="u_91-at-commands"></a>
## **9.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UTM](#atutm) | Transparent Mode |

<a name="atutm" id="atutm"></a>
### **9.1.1 AT+UTM - Transparent Mode**

Use this command to directly switch to transparent mode for a specific SPS link or a socket.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UTM=<link_type>,<handle>` | Enter Transparent Mode |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| handle | integer | For SPS links, set this to the connection handle<br>For sockets, set this to the socket handle<br> |
| link\_type | enumerator | Valid values:<br>0: BLE SPS Link<br>1: Socket |

