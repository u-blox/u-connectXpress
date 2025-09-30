# NORA-W36 AT Command Manual

Firmware version: v1.2.0

# Contents

[1 General](#general)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1 AT Commands](#u_11-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.1 AT \- Attention](#at)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.2 AT\+CGMI \- Manufacturer identification](#atcgmi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.3 AT\+GMI \- Manufacturer identification](#atgmi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.4 AT\+CGMM \- Model identification](#atcgmm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.5 AT\+GMM \- Model identification](#atgmm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.6 AT\+CGMR \- Software version identification](#atcgmr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.7 AT\+GMR \- Software version identification](#atgmr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.8 AT\+CGSN \- Serial number](#atcgsn)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.9 AT\+GSN \- Serial number](#atgsn)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.10 ATI \- Identification information](#ati)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1\.1\.11 AT\+CSGT \- Greeting Text](#atcsgt)<br>
[2 System](#system)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1 AT Commands](#u_21-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.1 AT\+CPWROFF \- Module switch off](#atcpwroff)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.2 AT&W \- Store current configuration\.](#atw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.3 AT\+USYLA \- Local Address](#atusyla)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.4 AT\+USYFR \- Factory Restore](#atusyfr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.5 AT\+USYDS \- Default Settings](#atusyds)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.6 AT\+USYUS \- Uart Settings](#atusyus)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.7 AT\+USYFWUS \- Firmware Update using serial port](#atusyfwus)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.8 AT\+USYBL \- Start the boot loader command line interface](#atusybl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.9 AT\+USYEC \- Error Code](#atusyec)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.10 AT\+USYEE \- Extended Error codes on/off](#atusyee)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.11 ATE \- Echo On/Off](#ate)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.12 ATS \- S\-registers](#ats)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2\.1\.13 AT\+UTMES \- Transparent mode escape sequence settings](#atutmes)<br>
[3 Bluetooth](#bluetooth)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1 AT Commands](#u_31-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.1 AT\+UBTM \- Bluetooth Mode](#atubtm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.2 AT\+UBTC \- Bluetooth Connect](#atubtc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.3 AT\+UBTP \- Bluetooth Persistent](#atubtp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.4 AT\+UBTPR \- Bluetooth Persistent Remove](#atubtpr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.5 AT\+UBTPL \- Bluetooth Persistent List](#atubtpl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.6 AT\+UBTDC \- Bluetooth Disconnect](#atubtdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.7 AT\+UBTLN \- Bluetooth Local Name](#atubtln)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.8 AT\+UBTD \- Bluetooth Discovery](#atubtd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.9 AT\+UBTBGD \- Bluetooth Background Discovery](#atubtbgd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.10 AT\+UBTRSS \- Bluetooth RSSI](#atubtrss)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.11 AT\+UBTCL \- Bluetooth Connection List](#atubtcl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.12 AT\+UBTCST \- Bluetooth Connection Status](#atubtcst)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.13 AT\+UBTAD \- Bluetooth Advertising Data](#atubtad)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.14 AT\+UBTSD \- Bluetooth Scan Data](#atubtsd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.15 AT\+UBTA \- Bluetooth Advertisements](#atubta)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.16 AT\+UBTDA \- Bluetooth Directed Advertisement](#atubtda)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.17 AT\+UBTCS \- Bluetooth Connection Settings](#atubtcs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.18 AT\+UBTAS \- Bluetooth Advertisement Settings\.](#atubtas)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.19 AT\+UBTIOC \- Bluetooth I/O Capabilities](#atubtioc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.20 AT\+UBTBSM \- Bluetooth Bond Security Mode](#atubtbsm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.21 AT\+UBTPM \- Bluetooth Pairing Mode](#atubtpm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.22 AT\+UBTUC \- Bluetooth User Confirmation](#atubtuc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.23 AT\+UBTUPE \- User passkey entry](#atubtupe)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.24 AT\+UBTB \- Bluetooth Bond](#atubtb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.25 AT\+UBTUB \- Bluetooth Unbond](#atubtub)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.26 AT\+UBTBDL \- Bluetooth Bonded Devices List](#atubtbdl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.27 AT\+UBTDIS \- Bluetooth Device Information Service](#atubtdis)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.1\.28 AT\+UBTPHYR \- Bluetooth PHY Request](#atubtphyr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2 Unsolicited Response Codes](#u_32-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.1 \+UEBTC \- Event Bluetooth Connected](#uebtc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.2 \+UEBTDC \- Event Bluetooth Disconnected](#uebtdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.3 \+UEBTB \- Event Bluetooth Bond status](#uebtb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.4 \+UEBTUC \- Event Bluetooth User Confirmation](#uebtuc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.5 \+UEBTUPD \- Event Bluetooth Passkey entry](#uebtupd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.6 \+UEBTUPE \- Event Bluetooth Passkey request](#uebtupe)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3\.2\.7 \+UEBTPHYU \- Event Bluetooth PHY update](#uebtphyu)<br>
[4 GATT client](#gatt-client)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1 AT Commands](#u_41-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.1 AT\+UBTGPSD \- GATT Primary Services Discover](#atubtgpsd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.2 AT\+UBTGPSDU \- GATT Primary Services Discover by UUID](#atubtgpsdu)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.3 AT\+UBTGSCD \- GATT Service Characteristics Discover](#atubtgscd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.4 AT\+UBTGCDD \- GATT Characteristic Descriptors Discover](#atubtgcdd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.5 AT\+UBTGR \- GATT Read](#atubtgr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.6 AT\+UBTGRU \- GATT Read characteristic by UUID](#atubtgru)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.7 AT\+UBTGW \- GATT Write](#atubtgw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.8 AT\+UBTGCCW \- GATT Client Configuration Write](#atubtgccw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.9 AT\+UBTGWNR \- GATT Write with No Response](#atubtgwnr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.1\.10 AT\+UBTGWL \- GATT Write long](#atubtgwl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.2 Unsolicited Response Codes](#u_42-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.2\.1 \+UEBTGCN \- Event GATT Client Notification](#uebtgcn)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4\.2\.2 \+UEBTGCI \- Event GATT Client Indication](#uebtgci)<br>
[5 GATT Server](#gatt-server)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1 AT Commands](#u_51-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.1 AT\+UBTGS \- GATT Service define](#atubtgs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.2 AT\+UBTGC \- GATT Characteristic define](#atubtgc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.3 AT\+UBTGHCC \- GATT Host Controlled Characteristic](#atubtghcc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.4 AT\+UBTGD \- GATT Descriptor define](#atubtgd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.5 AT\+UBTGSA \- GATT Service Activate\.](#atubtgsa)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.6 AT\+UBTGRRR \- GATT Read Request Respond](#atubtgrrr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.7 AT\+UBTGNS \- GATT Notification Send](#atubtgns)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.8 AT\+UBTGIS \- GATT Indication Send](#atubtgis)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.9 AT\+UBTGAV \- GATT Attribute Value](#atubtgav)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.10 AT\+UBTGRRRE \- GATT Read Request Respond with error code](#atubtgrrre)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.11 AT\+UBTGWRE \- GATT Write Respond with Error code](#atubtgwre)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.12 AT\+UBTGWRR \- GATT Write Request Respond](#atubtgwrr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.1\.13 AT\+UBTGSCI \- GATT Service Changed Indication](#atubtgsci)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2 Unsolicited Response Codes](#u_52-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.1 \+UEBTGCW \- Event GATT Server Write](#uebtgcw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.2 \+UEBTGRR \- Event GATT Server Read Response](#uebtgrr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5\.2\.3 \+UEBTGIC \- Event GATT Server Indication Confirmation](#uebtgic)<br>
[6 SPS](#sps)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1 AT Commands](#u_61-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.1 AT\+USPSC \- SPS Connect](#atuspsc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.2 AT\+USPS \- SPS \- Enable/Disable Service](#atusps)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.3 AT\+USPSWS \- SPS Write String](#atuspsws)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.4 AT\+USPSWB \- SPS Write Binary](#atuspswb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.5 AT\+USPSRM \- SPS Receive Mode](#atuspsrm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.6 AT\+USPSRS \- SPS Read String](#atuspsrs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.1\.7 AT\+USPSRB \- SPS Read Binary](#atuspsrb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2 Unsolicited Response Codes](#u_62-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.1 \+UESPSC \- Event SPS Connection](#uespsc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.2 \+UESPSDC \- Event SPS Disconnection](#uespsdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.3 \+UESPSDS \- Event SPS Data String](#uespsds)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.4 \+UESPSDB \- Event SPS Data Binary](#uespsdb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6\.2\.5 \+UESPSDA \- Event SPS Data Available](#uespsda)<br>
[7 Wi\-Fi](#wi-fi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1 AT Commands](#u_71-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.1 AT\+UWHN \- Wi\-Fi Host Name](#atuwhn)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.2 AT\+UWSSE \- Wi\-Fi Station Enterprise security](#atuwsse)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.3 AT\+UWSS \- Wi\-Fi Security Config](#atuwss)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.4 AT\+UWSSP \- Wi\-Fi Station PEAP security](#atuwssp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.5 AT\+UWSSW \- Wi\-Fi Station Security WPA](#atuwssw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.6 AT\+UWSSO \- Wi\-Fi Station Security Open](#atuwsso)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.7 AT\+UWSCP \- Wi\-Fi Station Connection Parameters](#atuwscp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.8 AT\+UWSIPS \- Wi\-Fi Station IP Static configuration](#atuwsips)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.9 AT\+UWSIPD \- Wi\-Fi Station IP with DHCP](#atuwsipd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.10 AT\+UWSIP \- Wi\-Fi Station IP configuration](#atuwsip)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.11 AT\+UWSC \- Wi\-Fi Station Connect](#atuwsc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.12 AT\+UWSDC \- Wi\-Fi Station Disconnect](#atuwsdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.13 AT\+UWSNST \- Wi\-Fi Station Network Status](#atuwsnst)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.14 AT\+UWRD \- Wi\-Fi Regulatory Domain](#atuwrd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.15 AT\+UWSSC \- Wi\-Fi Station Scan](#atuwssc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.16 AT\+UWSST \- Wi\-Fi Station Status](#atuwsst)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.17 AT\+UWAPA \- Wi\-Fi Access Point Activate](#atuwapa)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.18 AT\+UWAPD \- Wi\-Fi Access Point Deactivate](#atuwapd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.19 AT\+UWAPCP \- Wi\-Fi AP Connection Parameters](#atuwapcp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.20 AT\+UWAPSW \- Wi\-Fi AP Security WPA](#atuwapsw)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.21 AT\+UWAPSO \- Wi\-Fi AP Security Open](#atuwapso)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.22 AT\+UWAPS \- Wi\-Fi AP Security](#atuwaps)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.23 AT\+UWAPCS \- Wi\-Fi Access Point Connected Stations](#atuwapcs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.1\.24 AT\+UWAPNST \- Wi\-Fi Access Point Network Status](#atuwapnst)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2 Unsolicited Response Codes](#u_72-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.1 \+UEWLU \- Event Wi\-Fi Link Up](#uewlu)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.2 \+UEWLD \- Event Wi\-Fi Link Down](#uewld)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.3 \+UEWSNU \- Event Wi\-Fi Station Network Up](#uewsnu)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.4 \+UEWSND \- Event Wi\-Fi Station Network Down](#uewsnd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.5 \+UEWSRSI \- Event Wi\-Fi Station Roaming Switch Initiated](#uewsrsi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.6 \+UEWSRSF \- Event Wi\-Fi Station Roaming Switch Failed](#uewsrsf)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.7 \+UEWSRSC \- Event Wi\-Fi Station Roaming Switch Completed](#uewsrsc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.8 \+UEWAPNU \- Event Wi\-Fi Access Point Network Up](#uewapnu)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.9 \+UEWAPND \- Event Wi\-Fi Access Point Network Down](#uewapnd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.10 \+UEWAPU \- Event Wi\-Fi Access Point Up](#uewapu)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.11 \+UEWAPD \- Event Wi\-Fi Access Point Down](#uewapd)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.12 \+UEWAPSA \- Event Wi\-Fi Access Point Station Associated](#uewapsa)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7\.2\.13 \+UEWAPSDA \- Event Wi\-Fi Access Point Station Disassociated](#uewapsda)<br>
[8 Socket](#socket)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1 AT Commands](#u_81-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.1 AT\+USOCR \- Create Socket](#atusocr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.2 AT\+USOPCR \- Create Persistent Socket](#atusopcr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.3 AT\+USOTLS \- Socket TLS](#atusotls)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.4 AT\+USOC \- Socket Connect](#atusoc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.5 AT\+USOP \- Socket Persistent](#atusop)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.6 AT\+USOPR \- Socket Persistent Remove](#atusopr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.7 AT\+USOPL \- Socket Persistent List](#atusopl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.8 AT\+USORM \- Socket Receive Mode](#atusorm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.9 AT\+USOWS \- Socket Write String](#atusows)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.10 AT\+USOWB \- Socket Write Binary](#atusowb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.11 AT\+USOCL \- Close socket](#atusocl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.12 AT\+USORS \- Read Socket String](#atusors)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.13 AT\+USORB \- Socket Read Binary](#atusorb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.14 AT\+USOE \- Socket Error](#atusoe)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.15 AT\+USOL \- Socket Listen](#atusol)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.16 AT\+USORF \- Socket Read From](#atusorf)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.17 AT\+USOPA \- Socket Peer Address](#atusopa)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.18 AT\+USOST \- Socket Status](#atusost)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.19 AT\+USOO \- Socket Options](#atusoo)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.1\.20 AT\+USOH \- Socket Host by Name](#atusoh)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2 Unsolicited Response Codes](#u_82-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.1 \+UESOC \- Event Socket Connection](#uesoc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.2 \+UESODA \- Event Socket Data Available](#uesoda)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.3 \+UESODS \- Event Socket Data String](#uesods)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.4 \+UESODSF \- Event Socket Data String From](#uesodsf)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.5 \+UESODB \- Event Socket Data Binary](#uesodb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.6 \+UESODBF \- Event Socket Data Binary From](#uesodbf)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.7 \+UESOCL \- Event Socket Closed](#uesocl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8\.2\.8 \+UESOIC \- Event Socket Incoming Connection](#uesoic)<br>
[9 MQTT](#mqtt)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1 AT Commands](#u_91-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.1 AT\+UMQCP \- MQTT Connection Parameters](#atumqcp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.2 AT\+UMQC \- MQTT Connect to Broker](#atumqc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.3 AT\+UMQKA \- MQTT Keep Alive](#atumqka)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.4 AT\+UMQLWT \- MQTT Last Will and Testament](#atumqlwt)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.5 AT\+UMQTLS \- MQTT TLS Configuration](#atumqtls)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.6 AT\+UMQDC \- MQTT Disconnect](#atumqdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.7 AT\+UMQPS \- MQTT Publish String](#atumqps)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.8 AT\+UMQPB \- MQTT Publish Binary](#atumqpb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.9 AT\+UMQS \- MQTT Subscribe](#atumqs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.10 AT\+UMQRS \- MQTT Read String](#atumqrs)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.1\.11 AT\+UMQRB \- MQTT Read Binary](#atumqrb)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.2 Unsolicited Response Codes](#u_92-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.2\.1 \+UEMQC \- Event MQTT Connected](#uemqc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.2\.2 \+UEMQDC \- Event MQTT Disconnected](#uemqdc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9\.2\.3 \+UEMQDA \- Event MQTT Data Available](#uemqda)<br>
[10 Security](#security)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1 AT Commands](#u_101-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1\.1 AT\+USECR \- Security Certificate Remove](#atusecr)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1\.2 AT\+USECUB \- Security Certificate Upload Binary](#atusecub)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1\.3 AT\+USECL \- Security Certificates List](#atusecl)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1\.4 AT\+USETE \- Security TLS Extensions](#atusete)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1\.5 AT\+USETE0 \- Security TLS Extensions Server Name Indication](#atusete0)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10\.1\.6 AT\+USETE1 \- Security TLS Extensions Handshake Fragmentation](#atusete1)<br>
[11 Power](#power)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[11\.1 AT Commands](#u_111-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[11\.1\.1 AT\+UPMDS \- Power Management Deep Sleep](#atupmds)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[11\.1\.2 AT\+UPMPSTO \- Power Management Power Save Timeout](#atupmpsto)<br>
[12 Transparent](#transparent)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[12\.1 AT Commands](#u_121-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[12\.1\.1 AT\+UTM \- Transparent Mode](#atutm)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[12\.1\.2 AT\+UTMP \- Transparent Mode Persistent](#atutmp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[12\.1\.3 AT\+UTMPC \- Transparent Mode Persistent Clear](#atutmpc)<br>
[13 Diagnostics](#diagnostics)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.1 AT Commands](#u_131-at-commands)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.1\.1 AT\+UDGP \- Diagnostics Ping](#atudgp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.1\.2 AT\+UDGSP \- Stop an ongoing Ping](#atudgsp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.1\.3 AT\+UDGI \- Diagnostics Iperf](#atudgi)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.2 Unsolicited Response Codes](#u_132-unsolicited-response-codes)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.2\.1 \+UEDGPC \- Ping Complete Event](#uedgpc)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.2\.2 \+UEDGP \- Event Ping Response](#uedgp)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[13\.2\.3 \+UEDGI \- Event Iperf output](#uedgi)<br>

<a name="general" id="general"></a>
# **1 General**

<a name="u_11-at-commands" id="u_11-at-commands"></a>
## **1.1 AT Commands**

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
### **1.1.1 AT - Attention**

Attention command that determines the presence of a Data Communication Equipment (DCE).


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT` | Attention command. |

<a name="atcgmi" id="atcgmi"></a>
### **1.1.2 AT+CGMI - Manufacturer identification**

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
### **1.1.3 AT+GMI - Manufacturer identification**

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
### **1.1.4 AT+CGMM - Model identification**

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
### **1.1.5 AT+GMM - Model identification**

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
### **1.1.6 AT+CGMR - Software version identification**

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
### **1.1.7 AT+GMR - Software version identification**

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
### **1.1.8 AT+CGSN - Serial number**

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
### **1.1.9 AT+GSN - Serial number**

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
### **1.1.10 ATI - Identification information**

Read identification information.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `ATI9` | Read identification information. |
| `ATI10` | Read MCU ID. |
| `ATI0` | Read type code. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `<application_version>,<unique_identifier>` | Successful read response.<br>Note: The application_version and unique_identifier strings are returned without any response prefix.<br> |
| `<mcu_id>` | Successful read response.<br>Note: The mcu_id string is returned without any response prefix.<br> |
| `<type_code>` | Successful read response.<br>Note: The type_code string is returned without any response prefix.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| application\_version | string | Application version. |
| unique\_identifier | string | Unique identifier. |
| mcu\_id | string | Two byte hex string representing the MCU ID. |
| type\_code | string | Type code for the module. |

<a name="atcsgt" id="atcsgt"></a>
### **1.1.11 AT+CSGT - Greeting Text**

Configures and activates/deactivates the greeting text.
The configuration change in the greeting text will be applied at the subsequent boot.
When active, the greeting text is sent at boot once.



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

<a name="system" id="system"></a>
# **2 System**

System AT commands

<a name="u_21-at-commands" id="u_21-at-commands"></a>
## **2.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+CPWROFF](#atcpwroff) | Module switch off |
| [AT&W](#atw) | Store current configuration. |
| [AT+USYLA](#atusyla) | Local Address |
| [AT+USYFR](#atusyfr) | Factory Restore |
| [AT+USYDS](#atusyds) | Default Settings |
| [AT+USYUS](#atusyus) | Uart Settings |
| [AT+USYFWUS](#atusyfwus) | Firmware Update using serial port |
| [AT+USYBL](#atusybl) | Start the boot loader command line interface |
| [AT+USYEC](#atusyec) | Error Code |
| [AT+USYEE](#atusyee) | Extended Error codes on/off |
| [ATE](#ate) | Echo On/Off |
| [ATS](#ats) | S-registers |
| [AT+UTMES](#atutmes) | Transparent mode escape sequence settings |

<a name="atcpwroff" id="atcpwroff"></a>
### **2.1.1 AT+CPWROFF - Module switch off**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+CPWROFF` | Reboot the DCE. |

<a name="atw" id="atw"></a>
### **2.1.2 AT&W - Store current configuration.**

Store the current configuration to flash


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT&W` | Write the current configuration to flash. The configuration is stored immediately when AT&W is issued. |

<a name="atusyla" id="atusyla"></a>
### **2.1.3 AT+USYLA - Local Address**


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
| interface\_id | enumerator | Valid values:<br>0: Bluetooth<br>1: Wi-Fi station<br>2: Wi-Fi Access point |
| address | mac\_addr | MAC address of the interface id. If the address is set to 000000000000, the local address will be restored to factory-programmed value. The least significant bit of the first octet of the <address> must be 0. |

<a name="atusyfr" id="atusyfr"></a>
### **2.1.4 AT+USYFR - Factory Restore**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYFR` | The module is completely restored to factory defaults. All settings are reset to default values.<br>All certificates and Bluetooth bonding information will be removed.<br><br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

<a name="atusyds" id="atusyds"></a>
### **2.1.5 AT+USYDS - Default Settings**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYDS` | Reset all settings to default values.<br>Certificates and Bluetooth bonding information will be left untouched.<br><br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

<a name="atusyus" id="atusyus"></a>
### **2.1.6 AT+USYUS - Uart Settings**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYUS=<baud_rate>[,<flow_control>[,<change_after_confirm>]]` | Configure new UART settings that will be used after restart. Baudrates above 4000000 bps can be set, but are unsupported.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USYUS?` | Reads current UART settings from the module |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USYUS:<baud_rate>,<flow_control>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| baud\_rate | integer | Baudrate<br><br>Valid values: 110..6000000<br><br>Default value: 115200 |
| flow\_control | integer | 0: No flow control<br>1: Use CTS/RTS flow control<br><br><br>Valid values: 0 or 1 |
| change\_after\_confirm | integer | 0: Switch baudrate after reboot. When set [AT&W](#atw) must be called.<br>1: Switch baudrate directly after status OK have been sent.<br><br><br>Valid values: 0 or 1 |

<a name="atusyfwus" id="atusyfwus"></a>
### **2.1.7 AT+USYFWUS - Firmware Update using serial port**

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
| baud\_rate | integer | Valid values: 110..6000000<br><br>Default value: 115200 |
| flow\_control | integer | Valid values: 0 or 1<br><br>Default value: 0 |

<a name="atusybl" id="atusybl"></a>
### **2.1.8 AT+USYBL - Start the boot loader command line interface**

Force start of the boot loader. The boot loader will start at the defined baud rate.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USYBL=<baud_rate>[,<flow_control>]` | Force start of the boot loader. |
| `AT+USYBL` | Force start of the boot loader with default settings. Baudrate 115200 and flow control off. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| baud\_rate | integer | Valid values: 110..6000000<br><br>Default value: 115200 |
| flow\_control | integer | Valid values: 0 or 1<br><br>Default value: 0 |

<a name="atusyec" id="atusyec"></a>
### **2.1.9 AT+USYEC - Error Code**


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
### **2.1.10 AT+USYEE - Extended Error codes on/off**


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
### **2.1.11 ATE - Echo On/Off**

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
### **2.1.12 ATS - S-registers**

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
### **2.1.13 AT+UTMES - Transparent mode escape sequence settings**


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

<a name="bluetooth" id="bluetooth"></a>
# **3 Bluetooth**

Bluetooth commands

<a name="u_31-at-commands" id="u_31-at-commands"></a>
## **3.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UBTM](#atubtm) | Bluetooth Mode |
| [AT+UBTC](#atubtc) | Bluetooth Connect |
| [AT+UBTP](#atubtp) | Bluetooth Persistent |
| [AT+UBTPR](#atubtpr) | Bluetooth Persistent Remove |
| [AT+UBTPL](#atubtpl) | Bluetooth Persistent List |
| [AT+UBTDC](#atubtdc) | Bluetooth Disconnect |
| [AT+UBTLN](#atubtln) | Bluetooth Local Name |
| [AT+UBTD](#atubtd) | Bluetooth Discovery |
| [AT+UBTBGD](#atubtbgd) | Bluetooth Background Discovery |
| [AT+UBTRSS](#atubtrss) | Bluetooth RSSI |
| [AT+UBTCL](#atubtcl) | Bluetooth Connection List |
| [AT+UBTCST](#atubtcst) | Bluetooth Connection Status |
| [AT+UBTAD](#atubtad) | Bluetooth Advertising Data |
| [AT+UBTSD](#atubtsd) | Bluetooth Scan Data |
| [AT+UBTA](#atubta) | Bluetooth Advertisements |
| [AT+UBTDA](#atubtda) | Bluetooth Directed Advertisement |
| [AT+UBTCS](#atubtcs) | Bluetooth Connection Settings |
| [AT+UBTAS](#atubtas) | Bluetooth Advertisement Settings. |
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

<a name="atubtm" id="atubtm"></a>
### **3.1.1 AT+UBTM - Bluetooth Mode**

Set and read Bluetooth Mode.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTM=<bt_mode>` | Set Bluetooth Mode.<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |
| `AT+UBTM?` | Read Bluetooth Mode. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTM:<bt_mode>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bt\_mode | enumerator | Valid values:<br>0: Disabled.<br>1: Bluetooth Low Energy Central.<br>In this mode, starting advertisements, direct advertisements and other functions associated<br>with the Peripheral role is not possible.<br><br>2: Bluetooth Low Energy Peripheral.<br>In this mode, initiating connections, discovery and other functions associated with<br>the Central role is not possible.<br><br>3: Bluetooth Low Energy Simultaneous Central and Peripheral. This is the factory default for NORA-W36. |

<a name="atubtc" id="atubtc"></a>
### **3.1.2 AT+UBTC - Bluetooth Connect**

Make an ACL connection to a remote device with defined protocol type. Unsolicited events [+UEBTC](#uebtc) or [+UEBTDC](#uebtdc) will be sent out to confirm the connection establishment.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTC=<bd_addr>` | Initiate connection. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtp" id="atubtp"></a>
### **3.1.3 AT+UBTP - Bluetooth Persistent**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTP=<bd_addr>,<connect_sps>` | Configure an ACL link with automatic re-connection. As opposed to [AT+UBTC](#atubtc), this command will not initiate<br>a connection directly but is used for storing a connection configuration persistently so that the link is<br>automatically setup on boot.<br>See also [AT+USOP](#atusop)<br><br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTP:<config_id>` | Successful write response, returning a configuration id identifying the configuration |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| connect\_sps | integer | Should start a SPS connection when ACL link is up. <br>Integer Boolean flag  0 = No, 1 = Yes<br><br><br>Valid values: 0 or 1 |
| config\_id | integer | Configuration id<br><br>Valid values: 200 only |

<a name="atubtpr" id="atubtpr"></a>
### **3.1.4 AT+UBTPR - Bluetooth Persistent Remove**

Remove a Persistent Bluetooth Connection configuration


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTPR=<config_id>` | Removes a persistent bluetooth connection configuration<br><br>Notes:<br>The corresponding link will be automatically disconnected<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| config\_id | integer | Configuration id<br><br>Valid values: 200 only |

<a name="atubtpl" id="atubtpl"></a>
### **3.1.5 AT+UBTPL - Bluetooth Persistent List**

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
| config\_id | integer | Configuration id<br><br>Valid values: 200 only |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| connect\_sps | integer | Should start a SPS connection when ACL link is up. <br>Integer Boolean flag  0 = No, 1 = Yes<br><br><br>Valid values: 0 or 1 |

<a name="atubtdc" id="atubtdc"></a>
### **3.1.6 AT+UBTDC - Bluetooth Disconnect**

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
### **3.1.7 AT+UBTLN - Bluetooth Local Name**

Set the local name used as device name for Bluetooth Classic, in the advertising data of the device and in the Device Information service for Bluetooth low energy.


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
| device\_name | string | For Bluetooth low energy the maximum size is 29 characters.<br><br>Valid length: 0..29 |

<a name="atubtd" id="atubtd"></a>
### **3.1.8 AT+UBTD - Bluetooth Discovery**

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
| discovery\_type | enumerator | Valid values:<br>0: All with no filter. Displays all found devices; devices can be displayed multiple times.<br>1: General inquiry. Displays devices in General or Limited discoverability mode; each device is displayed only once. |
| discovery\_mode | enumerator | Valid values:<br>0: Active discovery.<br>1: Passive, no scan response data will be received.<br><br>Default value: 0 |
| discovery\_length | integer | Timeout measured in milliseconds. Time range: 10 ms - 40 s<br><br>Valid values: 10..40000<br><br>Default value: 5000 |
| device\_name | string | Name of the discovered device. |
| data\_type | enumerator | Valid values:<br>0: Scan response data.<br>1: Advertise data. |
| data | byte\_array | Complete advertise/scan response data received from the remote device. |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| rssi | integer | Received signal strength in dBm. |

<a name="atubtbgd" id="atubtbgd"></a>
### **3.1.9 AT+UBTBGD - Bluetooth Background Discovery**

Start a background discovery.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTBGD=<background_discovery_mode>` | Start/Stop background discovery |
| `AT+UBTBGD?` | Read background discovery mode |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTBGD:<background_discovery_mode>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| background\_discovery\_mode | enumerator | Valid values:<br>0: Set background discovery off<br>1: Set background discovery on |

<a name="atubtrss" id="atubtrss"></a>
### **3.1.10 AT+UBTRSS - Bluetooth RSSI**

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
### **3.1.11 AT+UBTCL - Bluetooth Connection List**

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
### **3.1.12 AT+UBTCST - Bluetooth Connection Status**

Read negotiated properties of a Bluetooth low energy ACL connection.
Some of the properties are a result of negotiation when a connections is set up, and this command gives the possibility
to see what properties the connection actually uses.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTCST=<conn_handle>` | Read all properties of an existing Bluetooth low energy ACL connection. |
| `AT+UBTCST=<conn_handle>,<property_id>` | Read a specific property of an existing Bluetooth low energy ACL connection. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTCST:<property_id>,<status_val>` | One response for each property_id. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| status\_val | integer | Value of the preceding property. |
| property\_id | enumerator | Valid values:<br>0: Connection interval used on this connection.<br> Range: 6 to 3200<br> Time = status_val * 1.25 ms<br> Time range: 7.5 ms to 4000 ms<br><br>1: Peripheral latency for the connection in number of connection events. Range: 0 to 499<br>2: Supervision timeout (in ms) for this connections. Range: 100 ms to 32000 ms<br>3: MTU size for this connections.<br>4: Data Channel TX PDU Payload Length.<br>5: Data Channel RX PDU Payload Length.<br>6: Data Length Extension state. 0: Data Length Extension Off \ 1: Data Length Extension On<br>7: Local role in this connection. 1: Low Energy Central \ 2: Low Energy Peripheral<br>8: TX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: reserved for future use<br><br>9: RX Phy used in this connection<br>Bit 0: 1 Mbps<br>Bit 1: 2 Mbps<br>Bit 2: reserved for future use<br> |
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |

<a name="atubtad" id="atubtad"></a>
### **3.1.13 AT+UBTAD - Bluetooth Advertising Data**

Command for setting custom advertising data in Bluetooth low energy. Maximum of 28 bytes.
Any custom advertising data will be appended to the default mandatory flags field. 
Note that the AT command [AT+UBTD](#atubtd) supports scan modes that can be used to see the complete advertising data. 
This is useful when testing the advertising configurations set with the AT+UBTAD. By default, the service UUID for the u-blox Serial Port Service is part of the advertising data.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAD=<adv_data>` | Write custom advertising data.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTAD?` | Read custom advertising data. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTAD:<adv_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| adv\_data | byte\_array | Valid length: 2..28 |

<a name="atubtsd" id="atubtsd"></a>
### **3.1.14 AT+UBTSD - Bluetooth Scan Data**

Command for setting custom scan response data in Bluetooth low energy. Any custom scan response data will override the default scan response data. By default, the local name is part of the scan response data.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTSD=<scan_rsp_data>` | Write scan response data.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTSD?` | Read scan response data. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTSD:<scan_rsp_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| scan\_rsp\_data | byte\_array | Valid length: 1..31 |

<a name="atubta" id="atubta"></a>
### **3.1.15 AT+UBTA - Bluetooth Advertisements**

Command for enabling and disabling advertisements


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTA=<adv_mode>` | Set advertisements on or off.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTA?` | Read advertisement mode. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTA:<adv_mode>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| adv\_mode | enumerator | Valid values:<br>0: Set Bluetooth Advertisements off<br>1: Set Bluetooth Advertisements on |

<a name="atubtda" id="atubtda"></a>
### **3.1.16 AT+UBTDA - Bluetooth Directed Advertisement**

Start a directed advertisement to a given Bluetooth Address


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTDA=<bd_addr>[,<timeout>]` | Starts directed advertisements to Bluetooth Address. If bd_addr is FFFFFFFFFFFF, direct advertisements will be disabled.<br>By default the timeout is 1280 ms, and uses High Duty Cycle Advertising. A timeout greater than this will result in<br>Low Duty Cycle Advertising as High Duty Cycle Advertising has a limited use of only 1280 ms. Setting timeout to 0 will let the<br>device advertise indefinitely in Low Duty Cycle mode.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| timeout | integer | Timeout for Directed Advertisements.<br><br>Default value: 1280 |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtcs" id="atubtcs"></a>
### **3.1.17 AT+UBTCS - Bluetooth Connection Settings**

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
| preferred\_tx\_phy | integer | Preferred Transmitter PHY<br>0: Let other side decide<br>OR a bit field with three bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: reserved for future use<br><br><br>Valid values: 0..7<br><br>Default value: 0 |
| preferred\_rx\_phy | integer | Preferred Receiver PHY<br>0: Let other side decide<br>OR a bit field with three bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: reserved for future use<br><br><br>Valid values: 0..7<br><br>Default value: 0 |
| param | enumerator | Connection parameter.<br><br>Valid values:<br>0: Connection interval minimum.<br>1: Connection interval maximum.<br>2: Connection peripheral latency.<br>3: Connection linkloss timeout.<br>4: Preferred Transmitter PHY<br>5: Preferred Receiver PHY |
| value | integer | Value of connection parameter.<br><br>Valid values: 0..65535 |

<a name="atubtas" id="atubtas"></a>
### **3.1.18 AT+UBTAS - Bluetooth Advertisement Settings.**

Get and Set Advertisement Settings.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTAS0=<advertisement_interval_minimum>` | Write advertisement interval minimum. |
| `AT+UBTAS0?` | Read advertisement Interval miniumum. |
| `AT+UBTAS1=<advertisement_interval_maximum>` | Write advertisement interval maximum. |
| `AT+UBTAS1?` | Read advertisement Interval maximum. |
| `AT+UBTAS?` | Read all Advertising parameter setting values. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTAS0:<advertisement_interval_minimum>` | Successful read of connection interval minimum. |
| `+UBTAS1:<advertisement_interval_maximum>` | Successful read of advertisement interval maximum. |
| `+UBTAS:<adv_param>,<value>` | Successful read response for AT+UBTAS?. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| advertisement\_interval\_minimum | integer | Advertising interval minimum (must be <= Advertising interval maximum. <br> Default: 1600.<br> Calculation: advertisement_interval_minimum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 1600 |
| advertisement\_interval\_maximum | integer | Advertising interval maximum (must be >= Advertising interval minimum. <br> Default: 2000.<br> Calculation: advertisement_interval_maximum * 0.625 ms)<br><br>Valid values: 32..16384<br><br>Default value: 2000 |
| value | integer | Value of advertisement parameter.<br><br>Valid values: 0..65535 |
| adv\_param | enumerator | Advertisement parameter.<br><br>Valid values:<br>0: Advertisement interval minimum.<br>1: Advertisement interval maximum. |

<a name="atubtioc" id="atubtioc"></a>
### **3.1.19 AT+UBTIOC - Bluetooth I/O Capabilities**

Set Bluetooth I/O Capabilities, this impacts the possible bonding procedure between devices.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTIOC=<io_capabilities>` | Set I/O Capabilities<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTIOC?` | Read I/O Capabilities |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTIOC:<io_capabilities>` | Successful read response for AT+UBTIOC?. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| io\_capabilities | enumerator | Valid values:<br>0: Set I/O Capabilities to No Input No Output.<br>1: Set I/O Capabilities to Display Only.<br>2: Set I/O Capabilities to Display Yes/No<br>3: Set I/O Capabilities to Keyboard Only.<br>4: Set I/O Capabilities to Keyboard Display.<br><br>Default value: 0 |

<a name="atubtbsm" id="atubtbsm"></a>
### **3.1.20 AT+UBTBSM - Bluetooth Bond Security Mode**

Set the security mode of the device. This command works together with [AT+UBTIOC](#atubtioc) to determine the bonding procedure used.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTBSM=<bt_security_mode>` | Writes the security mode<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTBSM?` | Reads the security mode |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTBSM:<bt_security_mode>` | Successful read response for AT+UBTBSM? |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bt\_security\_mode | enumerator | Valid values:<br>0: Security Disabled.<br>1: Allow unauthenticated bonding.<br>2: Only allow authenticated bonding.<br>3: Only allow authenticated bonding with encrypted Bluetooth link. Fallback to simple pairing if the remote side does not support secure connections.<br>4: Only allow authenticated bonding with encrypted Bluetooth link. Strictly uses secure connections.<br><br>Default value: 0 |

<a name="atubtpm" id="atubtpm"></a>
### **3.1.21 AT+UBTPM - Bluetooth Pairing Mode**

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
### **3.1.22 AT+UBTUC - Bluetooth User Confirmation**

The user confirmation is used together with IO capability DisplayYesNo to repond to a user confirmation request ([+UEBTUC](#uebtuc)). The command shall be used only after [+UEBTUC](#uebtuc) has been received.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTUC=<bd_addr>,<yes_no>` | Respond to +UEUBTUC and confirm/deny bonding. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| yes\_no | enumerator | Valid values:<br>0: Deny bonding.<br>1: Confirm bonding. |

<a name="atubtupe" id="atubtupe"></a>
### **3.1.23 AT+UBTUPE - User passkey entry**

The user passkey entry is used together with IO capability KeyboardOnly to respond on a user passkey entry request ([+UEBTUPE](#uebtupe)). This command shall be used only after [+UEBTUPE](#uebtupe) has been received.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTUPE=<bd_addr>,<yes_no>[,<passkey>]` | Respond to +UEBTUPE event and confirm/deny bonding. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| passkey | integer | Passkey used to confirm bonding, if yes_no is set to no, this can be omitted.<br><br>Valid values: 0..999999 |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| yes\_no | enumerator | Valid values:<br>0: Deny bonding.<br>1: Confirm bonding. |

<a name="atubtb" id="atubtb"></a>
### **3.1.24 AT+UBTB - Bluetooth Bond**

Performs a GAP bond procedure with another Bluetooth device. For some I/O Capabilities, user interaction is required during the bonding procedure. The procedure to use is determined by the I/O Capabilities and security mode.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTB=<bd_addr>` | Initiate bonding. To perform the bonding, the remote device must be in a pairable and connectable mode. Bond Event [+UEBTB](#uebtb) is genereated once the bond is complete. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="atubtub" id="atubtub"></a>
### **3.1.25 AT+UBTUB - Bluetooth Unbond**

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
### **3.1.26 AT+UBTBDL - Bluetooth Bonded Devices List**

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
### **3.1.27 AT+UBTDIS - Bluetooth Device Information Service**

Write and read the module's Device Information Service (DIS) characteristics.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTDIS=<characteristic_id>,<characteristic_value>` | Set a characteristic value.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UBTDIS=<characteristic_id>` | Read a characteristic value. |
| `AT+UBTDIS?` | Read all individual characteristic of the Device Information Service characteristics. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTDIS:<characteristic_id>,<characteristic_value>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| characteristic\_id | enumerator | Valid values:<br>0: Manufacturer name string. Maximum length of the custom string is 31 characters.<br>1: Model name string. Maximum length of the custom string is 20 characters.<br>2: Firmware revision string. Maximum length of the custom string is 20 characters.<br>3: Software revision string. Maximum length of the custom string is 20 characters. |
| characteristic\_value | string | Value of Device Information Service characteristic. |

<a name="atubtphyr" id="atubtphyr"></a>
### **3.1.28 AT+UBTPHYR - Bluetooth PHY Request**

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
| tx\_phy | integer | Requested PHY for Transmitter:<br>0: Let other side decide<br>OR a bit field with three bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY (S=8). Not supported by NORA-W36<br><br><br>Valid values: 0..7 |
| rx\_phy | integer | Requested PHY for Receiver<br>0: Let other side decide<br>OR a bit field with three bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY (S=8). Not supported by NORA-W36<br><br><br>Valid values: 0..7 |

<a name="u_32-unsolicited-response-codes" id="u_32-unsolicited-response-codes"></a>
## **3.2 Unsolicited Response Codes**

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
### **3.2.1 +UEBTC - Event Bluetooth Connected**

Event indicating successful Bluetooth connection.


**Syntax**<br>
```+UEBTC:<conn_handle>,<bd_addr>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="uebtdc" id="uebtdc"></a>
### **3.2.2 +UEBTDC - Event Bluetooth Disconnected**

Event indicating a disconnected Bluetooth connection.


**Syntax**<br>
```+UEBTDC:<conn_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |

<a name="uebtb" id="uebtb"></a>
### **3.2.3 +UEBTB - Event Bluetooth Bond status**

Event indicates that a bonding procedure is completed.


**Syntax**<br>
```+UEBTB:<bd_addr>,<bond_status>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| bond\_status | enumerator | Bonding status<br><br>Valid values:<br>0: Bonding procedure succeeded.<br>1: Bonding procedure failed due to page timeout.<br>2: Bonding failed because of authentication or pairing failed. This could be due to incorrect PIN/passkey.<br>3: Bonding failed because the protection against Man-In-The-Middle attack could not be guaranteed; the generated link key was too weak. |

<a name="uebtuc" id="uebtuc"></a>
### **3.2.4 +UEBTUC - Event Bluetooth User Confirmation**

This event is used while bonding with IO capability DisplayYesNo. This event indicates that the user confirmation of a numeric value is required.


**Syntax**<br>
```+UEBTUC:<bd_addr>,<numeric_value>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| numeric\_value | integer | Numeric value.<br><br>Valid values: 0..999999 |

<a name="uebtupd" id="uebtupd"></a>
### **3.2.5 +UEBTUPD - Event Bluetooth Passkey entry**

This event is used to indicate to the user that a passkey has to be entered on the remote device during a bonding procedure with the IO capability DisplayOnly.


**Syntax**<br>
```+UEBTUPD:<bd_addr>,<numeric_value>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |
| numeric\_value | integer | Numeric value.<br><br>Valid values: 0..999999 |

<a name="uebtupe" id="uebtupe"></a>
### **3.2.6 +UEBTUPE - Event Bluetooth Passkey request**

This event is used during bonding with IO capability KeyboardOnly to indicate that a passkey is required from the user. User should respond to this event with the [AT+UBTUPE](#atubtupe) command.


**Syntax**<br>
```+UEBTUPE:<bd_addr>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| bd\_addr | bd\_addr | Bluetooth device address of the remote device. |

<a name="uebtphyu" id="uebtphyu"></a>
### **3.2.7 +UEBTPHYU - Event Bluetooth PHY update**

This event informs the result of a PHY update procedure. It may be generated as a result of the command [AT+UBTPHYR](#atubtphyr) or as a successful event, if the operation has been initiated by the remote peer.


**Syntax**<br>
```+UEBTPHYU:<conn_handle>,<phy_status>,<tx_phy>,<rx_phy>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of the Bluetooth low energy connection. |
| phy\_status | integer | Bluetooth status codes:<br>0: Success<br>0x01-0xFF: Error, see Bluetooth Core Specifications, Vol 2, Part D.<br><br><br>Valid values: 0..255 |
| tx\_phy | integer | Requested PHY for Transmitter:<br>0: Let other side decide<br>OR a bit field with three bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY (S=8). Not supported by NORA-W36<br><br><br>Valid values: 0..7 |
| rx\_phy | integer | Requested PHY for Receiver<br>0: Let other side decide<br>OR a bit field with three bits:<br>Bit 0: 1 Mbps preferred<br>Bit 1: 2 Mbps preferred<br>Bit 2: Coded PHY (S=8). Not supported by NORA-W36<br><br><br>Valid values: 0..7 |

<a name="gatt-client" id="gatt-client"></a>
# **4 GATT client**

GATT Client

<a name="u_41-at-commands" id="u_41-at-commands"></a>
## **4.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UBTGPSD](#atubtgpsd) | GATT Primary Services Discover |
| [AT+UBTGPSDU](#atubtgpsdu) | GATT Primary Services Discover by UUID |
| [AT+UBTGSCD](#atubtgscd) | GATT Service Characteristics Discover |
| [AT+UBTGCDD](#atubtgcdd) | GATT Characteristic Descriptors Discover |
| [AT+UBTGR](#atubtgr) | GATT Read |
| [AT+UBTGRU](#atubtgru) | GATT Read characteristic by UUID |
| [AT+UBTGW](#atubtgw) | GATT Write |
| [AT+UBTGCCW](#atubtgccw) | GATT Client Configuration Write |
| [AT+UBTGWNR](#atubtgwnr) | GATT Write with No Response |
| [AT+UBTGWL](#atubtgwl) | GATT Write long |

<a name="atubtgpsd" id="atubtgpsd"></a>
### **4.1.1 AT+UBTGPSD - GATT Primary Services Discover**

List all GATT services on the GATT server.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGPSD=<conn_handle>` | Discover all primary services on the remote device. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGPSD:<conn_handle>,<start_handle>,<end_handle>,<uuid>` | This response is sent for each service found. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| start\_handle | integer | Service start handle. |
| end\_handle | integer | Service end handle. |
| uuid | byte\_array | UUID of attribute. Either 16-bit or 128-bit. |

<a name="atubtgpsdu" id="atubtgpsdu"></a>
### **4.1.2 AT+UBTGPSDU - GATT Primary Services Discover by UUID**

Discovers all primary services by UUID on the remote device.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGPSDU=<conn_handle>,<uuid>` | Start discovery. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGPSDU:<conn_handle>,<start_handle>,<end_handle>` | This response is sent for each service found. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| uuid | byte\_array | UUID of attribute. Either 16-bit or 128-bit. |
| start\_handle | integer | Service start handle. |
| end\_handle | integer | Service end handle. |

<a name="atubtgscd" id="atubtgscd"></a>
### **4.1.3 AT+UBTGSCD - GATT Service Characteristics Discover**

This command will list all characteristics belonging to a service on the GATT server.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGSCD=<conn_handle>,<start>,<end>` | Discover all characteristics of a service. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGSCD:<conn_handle>,<attr_handle>,<properties>,<value_handle>,<uuid>` | This response is sent for each characteristic found. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| start | integer | Service start handle. |
| end | integer | Service end handle. |
| attr\_handle | integer | Attribute handle of the characteristic |
| properties | byte\_array | Bit mask describing the properties of the characteristic |
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| uuid | byte\_array | UUID of attribute. Either 16-bit or 128-bit. |

<a name="atubtgcdd" id="atubtgcdd"></a>
### **4.1.4 AT+UBTGCDD - GATT Characteristic Descriptors Discover**

Discover Characteristics Descriptors. This command will list all descriptors of a characteristic on the GATT server.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGCDD=<conn_handle>,<value_handle>,<characteristic_end_handle>` | Discover all descriptors of a characteristic. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGCDD:<conn_handle>,<char_handle>,<desc_handle>,<uuid>` | This response is sent for each descriptor found. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| char\_handle | integer | Characteristic handle. |
| characteristic\_end\_handle | integer | End handle of characteristic to which descriptor discovery is being performed. |
| desc\_handle | integer | Descriptor handle. |
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| uuid | byte\_array | UUID of attribute. Either 16-bit or 128-bit. |

<a name="atubtgr" id="atubtgr"></a>
### **4.1.5 AT+UBTGR - GATT Read**

Read a characteristic value.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGR=<conn_handle>,<value_handle>` | Reads the characteristic; all bytes included. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGR:<conn_handle>,<value_handle>,<hex_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="atubtgru" id="atubtgru"></a>
### **4.1.6 AT+UBTGRU - GATT Read characteristic by UUID**

Read GATT characteristic values by UUID.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGRU=<conn_handle>,<start>,<end>,<uuid>` | Read all the characteristics by UUID. It will read all the bytes in each characteristic. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UBTGRU:<conn_handle>,<value_handle>,<hex_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| start | integer | Start handle. |
| end | integer | End handle. |
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| uuid | byte\_array | UUID of attribute. Either 16-bit or 128-bit. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="atubtgw" id="atubtgw"></a>
### **4.1.7 AT+UBTGW - GATT Write**

Write a characteristic value.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGW=<conn_handle>,<value_handle>,<hex_data>` | Write the characteristic value. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="atubtgccw" id="atubtgccw"></a>
### **4.1.8 AT+UBTGCCW - GATT Client Configuration Write**

Write characteristic configuration to enable notifications or indications.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGCCW=<conn_handle>,<desc_handle>,<config>` | Writes the client characteristic configuration. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| desc\_handle | integer | Descriptor handle. |
| config | enumerator | Valid values:<br>0: None<br>1: Enable notifications<br>2: Enable indications<br>3: Enable notifications and indications |
| conn\_handle | integer | Bluetooth Low Energy connection handle. |

<a name="atubtgwnr" id="atubtgwnr"></a>
### **4.1.9 AT+UBTGWNR - GATT Write with No Response**

Write the characteristic with no response message from the remote side.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGWNR=<conn_handle>,<value_handle>,<hex_data>` | Write characteristic. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="atubtgwl" id="atubtgwl"></a>
### **4.1.10 AT+UBTGWL - GATT Write long**

Write a long characteristic.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGWL=<conn_handle>,<value_handle>,<hex_data>,<reliable>,<flag>,<offset>` | Write long characteristic. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| reliable | enumerator | Valid values:<br>0: Not reliable<br>1: Reliable |
| flag | enumerator | Valid values:<br>0: Final data<br>1: More data<br>2: Cancel |
| offset | integer |  |
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="u_42-unsolicited-response-codes" id="u_42-unsolicited-response-codes"></a>
## **4.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEBTGCN](#uebtgcn) | Event GATT Client Notification |
| [+UEBTGCI](#uebtgci) | Event GATT Client Indication |

<a name="uebtgcn" id="uebtgcn"></a>
### **4.2.1 +UEBTGCN - Event GATT Client Notification**

GATT Client Notification. This event is received when the remote side sends a notification.


**Syntax**<br>
```+UEBTGCN:<conn_handle>,<value_handle>,<hex_data>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="uebtgci" id="uebtgci"></a>
### **4.2.2 +UEBTGCI - Event GATT Client Indication**

GATT Client Indication. This event is received when the remote side sends an indication.


**Syntax**<br>
```+UEBTGCI:<conn_handle>,<value_handle>,<hex_data>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Bluetooth Low Energy connection handle. |
| value\_handle | integer | Attribute handle of the characteristic value. |
| hex\_data | byte\_array | Characteristic data in hexadecimal form. For example, 070809AABBCC |

<a name="gatt-server" id="gatt-server"></a>
# **5 GATT Server**

GATT Server

<a name="u_51-at-commands" id="u_51-at-commands"></a>
## **5.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UBTGS](#atubtgs) | GATT Service define |
| [AT+UBTGC](#atubtgc) | GATT Characteristic define |
| [AT+UBTGHCC](#atubtghcc) | GATT Host Controlled Characteristic |
| [AT+UBTGD](#atubtgd) | GATT Descriptor define |
| [AT+UBTGSA](#atubtgsa) | GATT Service Activate. |
| [AT+UBTGRRR](#atubtgrrr) | GATT Read Request Respond |
| [AT+UBTGNS](#atubtgns) | GATT Notification Send |
| [AT+UBTGIS](#atubtgis) | GATT Indication Send |
| [AT+UBTGAV](#atubtgav) | GATT Attribute Value |
| [AT+UBTGRRRE](#atubtgrrre) | GATT Read Request Respond with error code |
| [AT+UBTGWRE](#atubtgwre) | GATT Write Respond with Error code |
| [AT+UBTGWRR](#atubtgwrr) | GATT Write Request Respond |
| [AT+UBTGSCI](#atubtgsci) | GATT Service Changed Indication |

<a name="atubtgs" id="atubtgs"></a>
### **5.1.1 AT+UBTGS - GATT Service define**

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
### **5.1.2 AT+UBTGC - GATT Characteristic define**

Command to add a GATT characteristic to the most recent GATT service record created with [AT+UBTGS](#atubtgs).


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGC=<uuid>,<properties>,<security_read>,<security_write>,<value>[,<max_length>]` | Create a new characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported. |

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
| security\_read | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |
| security\_write | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |

<a name="atubtghcc" id="atubtghcc"></a>
### **5.1.3 AT+UBTGHCC - GATT Host Controlled Characteristic**

Create a new host controlled characteristic in the GATT table for a GATT server. The CCCD for the characteristic, if applicable, is created here. Extended properties such as CPFD, CUDD, and SCCD are not supported.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGHCC=<uuid>,<properties>,<security_read>,<security_write>` | Define a characteristic. |

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
| security\_read | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |
| security\_write | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |

<a name="atubtgd" id="atubtgd"></a>
### **5.1.4 AT+UBTGD - GATT Descriptor define**

Define a vendor defined descriptor. Standard Bluetooth low energy descriptors such as CCCD are created while creating the characteristic in [AT+UBTGC](#atubtgc) command.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGD=<uuid>,<security_read>,<security_write>,<value>[,<max_length>]` | Define descriptor. |

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
| security\_read | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |
| security\_write | enumerator | Valid values:<br>1: No encryption required.<br>2: Unauthenticated encryption required.<br>3: Authenticated encryption required. |

<a name="atubtgsa" id="atubtgsa"></a>
### **5.1.5 AT+UBTGSA - GATT Service Activate.**

Activate the service defined with the [AT+UBTGS](#atubtgs) command. After this command is issued, it is not possible to add more characteristics or descriptors to the service.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGSA` | Activate current defined service. |

<a name="atubtgrrr" id="atubtgrrr"></a>
### **5.1.6 AT+UBTGRRR - GATT Read Request Respond**

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
### **5.1.7 AT+UBTGNS - GATT Notification Send**

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
### **5.1.8 AT+UBTGIS - GATT Indication Send**

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
### **5.1.9 AT+UBTGAV - GATT Attribute Value**

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
### **5.1.10 AT+UBTGRRRE - GATT Read Request Respond with error code**

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
### **5.1.11 AT+UBTGWRE - GATT Write Respond with Error code**

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
### **5.1.12 AT+UBTGWRR - GATT Write Request Respond**

Accept write request from GATT client.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGWRR=<conn_handle>` | Respond to write request. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of connected device. |

<a name="atubtgsci" id="atubtgsci"></a>
### **5.1.13 AT+UBTGSCI - GATT Service Changed Indication**

Sends an indication to the remote peer client that the attribute table of the local GATT server has changed.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UBTGSCI=<conn_handle>,<start_handle>,<end_handle>` | Send Service Changed Indication. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | GAP handle of connected device. |
| start\_handle | integer | Start of the affected attribute handle range. |
| end\_handle | integer | End of the affected attribute handle range. |

<a name="u_52-unsolicited-response-codes" id="u_52-unsolicited-response-codes"></a>
## **5.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEBTGCW](#uebtgcw) | Event GATT Server Write |
| [+UEBTGRR](#uebtgrr) | Event GATT Server Read Response |
| [+UEBTGIC](#uebtgic) | Event GATT Server Indication Confirmation |

<a name="uebtgcw" id="uebtgcw"></a>
### **5.2.1 +UEBTGCW - Event GATT Server Write**

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
### **5.2.2 +UEBTGRR - Event GATT Server Read Response**

Unsolicited response code for GATT Server. This event occurs when a remote client reads an attribute over the air. The event should be responded with [AT+UBTGRRR](#atubtgrrr).


**Syntax**<br>
```+UEBTGRR:<conn_handle>,<value_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Handle of the connected device. |
| value\_handle | integer | Handle of the characteristic value. |

<a name="uebtgic" id="uebtgic"></a>
### **5.2.3 +UEBTGIC - Event GATT Server Indication Confirmation**

Unsolicited response code for GATT Server. This event occurs when a remote GATT client acknowledges the receipt of an indication message sent using [AT+UBTGIS](#atubtgis).


**Syntax**<br>
```+UEBTGIC:<conn_handle>,<char_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connected device handle. |
| char\_handle | integer | Characteristic value handle. |

<a name="sps" id="sps"></a>
# **6 SPS**

SPS - Serial Port Service

<a name="u_61-at-commands" id="u_61-at-commands"></a>
## **6.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+USPSC](#atuspsc) | SPS Connect |
| [AT+USPS](#atusps) | SPS - Enable/Disable Service |
| [AT+USPSWS](#atuspsws) | SPS Write String |
| [AT+USPSWB](#atuspswb) | SPS Write Binary |
| [AT+USPSRM](#atuspsrm) | SPS Receive Mode |
| [AT+USPSRS](#atuspsrs) | SPS Read String |
| [AT+USPSRB](#atuspsrb) | SPS Read Binary |

<a name="atuspsc" id="atuspsc"></a>
### **6.1.1 AT+USPSC - SPS Connect**

SPS connect on connected Bluetooth device


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPSC=<conn_handle>[,<flow_control>]` | SPS connect on connected Bluetooth device |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |
| flow\_control | integer | Flow control: 0 - no flow control, 1 - flow control |

<a name="atusps" id="atusps"></a>
### **6.1.2 AT+USPS - SPS - Enable/Disable Service**

Enable or disable the SPS service


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USPS=<sps_service_option>` | Enables or disable the SPS Service.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USPS?` | Read if the SPS service is enabled or disabled. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USPS:<sps_service_option>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| sps\_service\_option | enumerator | Valid values:<br>0: This option disables the SPS service after saving the configuration and restarting the device. (Default)<br>1: This option enables the SPS service directly.<br>If this option is set, and the configuration is saved,<br>SPS will be enabled after reboot.<br> |

<a name="atuspsws" id="atuspsws"></a>
### **6.1.3 AT+USPSWS - SPS Write String**

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
### **6.1.4 AT+USPSWB - SPS Write Binary**


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
### **6.1.5 AT+USPSRM - SPS Receive Mode**


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
### **6.1.6 AT+USPSRS - SPS Read String**


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
### **6.1.7 AT+USPSRB - SPS Read Binary**


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

<a name="u_62-unsolicited-response-codes" id="u_62-unsolicited-response-codes"></a>
## **6.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UESPSC](#uespsc) | Event SPS Connection |
| [+UESPSDC](#uespsdc) | Event SPS Disconnection |
| [+UESPSDS](#uespsds) | Event SPS Data String |
| [+UESPSDB](#uespsdb)} | Event SPS Data Binary |
| [+UESPSDA](#uespsda) | Event SPS Data Available |

<a name="uespsc" id="uespsc"></a>
### **6.2.1 +UESPSC - Event SPS Connection**

Event response for SPS Connect. Upon a successful SPS connection, conn_handle will contain the connection handle of the remote peer.


**Syntax**<br>
```+UESPSC:<conn_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |

<a name="uespsdc" id="uespsdc"></a>
### **6.2.2 +UESPSDC - Event SPS Disconnection**

Event response for SPS Connect. Upon a SPS disconnection, conn_handle will contain the connection handle of the remote peer.


**Syntax**<br>
```+UESPSDC:<conn_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |

<a name="uespsds" id="uespsds"></a>
### **6.2.3 +UESPSDS - Event SPS Data String**

Unsolicited event containing SPS data as a string received from remote peer.


**Syntax**<br>
```+UESPSDS:<conn_handle>,<string_data>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| conn\_handle | integer | Connection handle of remote peer |
| string\_data | string | SPS data in string format |

<a name="uespsdb" id="uespsdb"></a>
### **6.2.4 +UESPSDB - Event SPS Data Binary**

Unsolicited event containing SPS data in binary format.


**Syntax**<br>
```+UESPSDB:<conn_handle>{binary_data}```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The received data. |
| conn\_handle | integer | Connection handle of remote peer |

<a name="uespsda" id="uespsda"></a>
### **6.2.5 +UESPSDA - Event SPS Data Available**

Unsolicited event containing the number of received bytes to read.


**Syntax**<br>
```+UESPSDA:<conn_handle>,<number_bytes>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| number\_bytes | integer | Number of bytes available to read. |
| conn\_handle | integer | Connection handle of remote peer |

<a name="wi-fi" id="wi-fi"></a>
# **7 Wi-Fi**

Wi-Fi Commands

<a name="u_71-at-commands" id="u_71-at-commands"></a>
## **7.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UWHN](#atuwhn) | Wi-Fi Host Name |
| [AT+UWSSE](#atuwsse) | Wi-Fi Station Enterprise security |
| [AT+UWSS](#atuwss) | Wi-Fi Security Config |
| [AT+UWSSP](#atuwssp) | Wi-Fi Station PEAP security |
| [AT+UWSSW](#atuwssw) | Wi-Fi Station Security WPA |
| [AT+UWSSO](#atuwsso) | Wi-Fi Station Security Open |
| [AT+UWSCP](#atuwscp) | Wi-Fi Station Connection Parameters |
| [AT+UWSIPS](#atuwsips) | Wi-Fi Station IP Static configuration |
| [AT+UWSIPD](#atuwsipd) | Wi-Fi Station IP with DHCP |
| [AT+UWSIP](#atuwsip) | Wi-Fi Station IP configuration |
| [AT+UWSC](#atuwsc) | Wi-Fi Station Connect |
| [AT+UWSDC](#atuwsdc) | Wi-Fi Station Disconnect |
| [AT+UWSNST](#atuwsnst) | Wi-Fi Station Network Status |
| [AT+UWRD](#atuwrd) | Wi-Fi Regulatory Domain |
| [AT+UWSSC](#atuwssc) | Wi-Fi Station Scan |
| [AT+UWSST](#atuwsst) | Wi-Fi Station Status |
| [AT+UWAPA](#atuwapa) | Wi-Fi Access Point Activate |
| [AT+UWAPD](#atuwapd) | Wi-Fi Access Point Deactivate |
| [AT+UWAPCP](#atuwapcp) | Wi-Fi AP Connection Parameters |
| [AT+UWAPSW](#atuwapsw) | Wi-Fi AP Security WPA |
| [AT+UWAPSO](#atuwapso) | Wi-Fi AP Security Open |
| [AT+UWAPS](#atuwaps) | Wi-Fi AP Security |
| [AT+UWAPCS](#atuwapcs) | Wi-Fi Access Point Connected Stations |
| [AT+UWAPNST](#atuwapnst) | Wi-Fi Access Point Network Status |

<a name="atuwhn" id="atuwhn"></a>
### **7.1.1 AT+UWHN - Wi-Fi Host Name**

Set hostname for Wi-Fi interfaces. Note that AP and Station will both use the stored hostname


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWHN=<host_name>` | Set the Host Name<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UWHN?` | Reads the current hostname |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWHN:<host_name>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| host\_name | string | Valid length: 0..40<br><br>Default value: NORA-W36-xxxxxxxxxxxx where xxxxxxxxxxxx is the Wi-Fi station mac address<br>If the hostname is set to "" it will be restored to the factory value after reset<br> |

<a name="atuwsse" id="atuwsse"></a>
### **7.1.2 AT+UWSSE - Wi-Fi Station Enterprise security**

Configure enterprise security. Certificates must be uploaded to the module before being used in this command, see [AT+USECUB](#atusecub)


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSSE=<wlan_handle>,<ca_name>,<client_cert_name>,<client_key_name>` | Set the EAP-TLS connection parameters to use.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| ca\_name | string | Name of the certificate authority (CA) certificate to use<br><br>Valid length: 1..32 |
| client\_cert\_name | string | Name of the client certificate to use<br><br>Valid length: 1..32 |
| client\_key\_name | string | Name of the private key for client certificate<br><br>Valid length: 1..32 |

<a name="atuwss" id="atuwss"></a>
### **7.1.3 AT+UWSS - Wi-Fi Security Config**

Read the current security parameter configuration, for Wi-Fi station


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSS=<wlan_handle>` | Get the current Wi-Fi station security config |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSS:<wlan_handle>,<security_mode>,<wpa_threshold>` | Response if security mode is WPA |
| `+UWSS:<wlan_handle>,<security_mode>` | Response if security mode is Open |
| `+UWSS:<wlan_handle>,<security_mode>,<ca_name>,<client_cert_name>,<client_key_name>` | Response if security mode is EAP-TLS |
| `+UWSS:<wlan_handle>,<security_mode>,<username>,<ca_name>` | Response if security mode is PEAP |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| security\_mode | enumerator | The current security mode.<br><br>Valid values:<br>0: Open security<br>1: WPA security<br>2: EAP-TLS security<br>3: PEAP security |
| wpa\_threshold | enumerator | Lowest WPA version to connect to<br><br>Valid values:<br>0: Only connect to access points that support WPA2 or up<br>1: Only connect to access points that support WPA3<br><br>Default value: 0 |
| ca\_name | string | Name of the certificate authority (CA) certificate to use<br><br>Valid length: 1..32 |
| client\_cert\_name | string | Name of the client certificate to use<br><br>Valid length: 1..32 |
| client\_key\_name | string | Name of the private key for client certificate<br><br>Valid length: 1..32 |
| username | string | User name for PEAP authentication.<br><br>Valid length: 1..31 |

<a name="atuwssp" id="atuwssp"></a>
### **7.1.4 AT+UWSSP - Wi-Fi Station PEAP security**

Configure PEAP security. CA certificate must be uploaded first if used here, see [AT+USECUB](#atusecub)


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSSP=<wlan_handle>,<peap_user>,<peap_password>[,<ca_name>]` | Set the PEAP connection parameters to use.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| peap\_user | string | User name for PEAP authentication. Could be either only username or username@domain. Use @ as separator<br><br><br>Valid length: 1..31 |
| peap\_password | string | Password for PEAP authentication.<br><br>Valid length: 1..31 |
| ca\_name | string | Name of the certificate authority (CA) certificate to use<br><br>Valid length: 1..32 |

<a name="atuwssw" id="atuwssw"></a>
### **7.1.5 AT+UWSSW - Wi-Fi Station Security WPA**

Configure WPA security


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSSW=<wlan_handle>,<passphrase>,<wpa_threshold>` | Set WPA connection parameters to use<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| passphrase | string | Passphrase to use for WPA connection<br><br>Valid length: 8..63 |
| wpa\_threshold | enumerator | Lowest WPA version to connect to<br><br>Valid values:<br>0: Only connect to access points that support WPA2 or up<br>1: Only connect to access points that support WPA3<br><br>Default value: 0 |

<a name="atuwsso" id="atuwsso"></a>
### **7.1.6 AT+UWSSO - Wi-Fi Station Security Open**

Configure open security


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSSO=<wlan_handle>` | Sets security to open security<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |

<a name="atuwscp" id="atuwscp"></a>
### **7.1.7 AT+UWSCP - Wi-Fi Station Connection Parameters**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSCP=<wlan_handle>,<ssid>` | Sets the connection parameters for the connection.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UWSCP=<wlan_handle>` | Reads the connection parameters for the connection. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSCP:<wlan_handle>,<ssid>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| ssid | string | SSID<br><br>Valid length: 0..32 |

<a name="atuwsips" id="atuwsips"></a>
### **7.1.8 AT+UWSIPS - Wi-Fi Station IP Static configuration**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSIPS=<wlan_handle>,<ip_addr>,<subnet_mask>,<gateway>[,<prim_dns>[,<sec_dns>]]` | Sets ip configuration to use static ip<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| ip\_addr | ip\_addr | Static IPv4 address<br><br>Default value: 0.0.0.0 |
| subnet\_mask | ip\_addr | Subnet mask<br><br>Default value: 0.0.0.0 |
| gateway | ip\_addr | IPv4 gateway address<br><br>Default value: 0.0.0.0 |
| prim\_dns | ip\_addr | IPv4 primary dns address<br><br>Default value: 0.0.0.0 |
| sec\_dns | ip\_addr | IPv4 secondary dns address<br><br>Default value: 0.0.0.0 |

<a name="atuwsipd" id="atuwsipd"></a>
### **7.1.9 AT+UWSIPD - Wi-Fi Station IP with DHCP**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSIPD=<wlan_handle>` | Sets ip configuration to receive ip address via dhcp<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |

<a name="atuwsip" id="atuwsip"></a>
### **7.1.10 AT+UWSIP - Wi-Fi Station IP configuration**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSIP=<wlan_handle>` | Read the current configuration for IP address assignment |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSIP:<wlan_handle>,<ip_mode>` | Response if IP mode is DHCP |
| `+UWSIP:<wlan_handle>,<ip_mode>,<ip_addr>,<subnet_mask>,<gateway>,<prim_dns>,<sec_dns>` | Response if IP mode is set to be static |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| ip\_mode | enumerator | IP assignment<br><br>Valid values:<br>0: DHCP<br>1: Static IP |
| ip\_addr | ip\_addr | Static IPv4 address<br><br>Default value: 0.0.0.0 |
| subnet\_mask | ip\_addr | Subnet mask<br><br>Default value: 0.0.0.0 |
| gateway | ip\_addr | IPv4 gateway address<br><br>Default value: 0.0.0.0 |
| prim\_dns | ip\_addr | IPv4 primary dns address<br><br>Default value: 0.0.0.0 |
| sec\_dns | ip\_addr | IPv4 secondary dns address<br><br>Default value: 0.0.0.0 |

<a name="atuwsc" id="atuwsc"></a>
### **7.1.11 AT+UWSC - Wi-Fi Station Connect**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSC=<wlan_handle>` | Initiate connection to Wi-Fi network<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |

<a name="atuwsdc" id="atuwsdc"></a>
### **7.1.12 AT+UWSDC - Wi-Fi Station Disconnect**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSDC` | Disconnect from Wi-Fi network<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="atuwsnst" id="atuwsnst"></a>
### **7.1.13 AT+UWSNST - Wi-Fi Station Network Status**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSNST=<status_id>` | Show current status of Wi-Fi station network interface |
| `AT+UWSNST?` | Show current status of Wi-Fi station network interface |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSNST:<status_id>,<status_val>` | Send for every applicable status |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| status\_id | enumerator | Valid values:<br>0: The current IPv4 address.<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>1: The current subnet mask<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>2: The current gateway<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>3: The current primary DNS server<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>4: The current secondary DNS server<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>5: The current IPv6 link local address<br>Note: If network is down this will be [0000:0000:0000:0000:0000:0000:0000:0000] regardless of IP setting<br> |
| status\_val | ip\_addr | IP address |

<a name="atuwrd" id="atuwrd"></a>
### **7.1.14 AT+UWRD - Wi-Fi Regulatory Domain**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWRD=<reg_domain>` | Set the regulatory domain for all Wi-Fi interfaces. This will configure the channel list and power levels for Wi-Fi. Make sure to set the correct code for the region the device will be operating in. Both 2.4 and 5 GHz band is always operative. Set the domain before starting AP or Station<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UWRD?` | Read regulatory domain |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWRD:<reg_domain>` | Current regulatory domain |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| reg\_domain | enumerator | Regulatory domain<br><br>Valid values:<br>0: World<br>Supported Channels;<br>1-11<br>36,40,44,48<br>52,56,60,64<br><br>1: ETSI<br>Supported Channels;<br>1-13<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,120,124,128,132,136,140<br>149,153,157,161,165<br><br>2: FCC<br>Supported Channels;<br>1-11<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,120,124,128,132,136,140<br>149,153,157,161,165<br><br>3: IC/ISED<br>Supported Channels;<br>1-11<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,132,136,140,144<br>149,153,157,161,165<br><br>4: NZ/BR<br>Supported Channels;<br>1-13<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,120,124,128,132,136,140,144<br>149,153,157,161,165<br><br>5: MKK/Japan<br>Supported Channels;<br>1-14<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,120,124,128,132,136,140,144<br><br>6: NCC/Taiwan<br>Supported Channels;<br>1-11<br>52,56,60,64<br>100,104,108,112,116,132,136,140<br>NOTE: Certification pending. DO NOT USE without certifying the end product<br><br>7: ACMA/AU<br>Supported Channels;<br>1-13<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,132,136,140,144<br>149,153,157,161,165<br><br>8: KCC/South Korea<br>Supported Channels;<br>1-13<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,120,124,128,132,136,140,144<br>149,153,157,161,165<br><br>9: SA/South Africa<br>Supported Channels;<br>1-13<br>36,40,44,48<br>52,56,60,64<br>100,104,108,112,116,120,124,128,132,136,140<br> |

<a name="atuwssc" id="atuwssc"></a>
### **7.1.15 AT+UWSSC - Wi-Fi Station Scan**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSSC` | Initiate synchronous Wi-Fi scan (will lock AT interface until scan has finished) |
| `AT+UWSSC=<scan_mode>[,<ssid>]` | Initiate synchronous Wi-Fi scan (will lock AT interface until scan has finished) |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSSC:<bssid>,<ssid>,<channel>,<rssi>,<authentication_suites>,<unicast_ciphers>,<group_ciphers>` | Successful scan response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| scan\_mode | enumerator | Choose how to scan<br><br>Valid values:<br>0: Active<br>1: Passive<br><br>Default value: Active |
| bssid | mac\_addr | BSSID |
| ssid | string | SSID<br><br>Valid length: 0..32 |
| channel | integer | Channel |
| rssi | integer | RSSI |
| authentication\_suites | integer | Authentication suites. Bit 0 = shared secret, 1 = PSK, 2 = EAP, 3 = WPA, 4 = WPA2, 5 = WPA3 |
| unicast\_ciphers | integer | unicast ciphers. Bit 0 = WEP64, 1 = WEP128, 2 = TKIP, 3 = AES/CCMP |
| group\_ciphers | integer | group ciphers. Bit 0 = WEP64, 1 = WEP128, 2 = TKIP, 3 = AES/CCMP |

<a name="atuwsst" id="atuwsst"></a>
### **7.1.16 AT+UWSST - Wi-Fi Station Status**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWSST=<wifi_status_id>` | Read status |
| `AT+UWSST` | Read status |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWSST:<wifi_status_id>,<ssid>` | Read response for SSID |
| `+UWSST:<wifi_status_id>,<bssid>` | Read response for BSSID |
| `+UWSST:<wifi_status_id>,<int_val>` | Read response for Channel, Connection status and RSSI |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ssid | string | SSID<br><br>Valid length: 0..32 |
| wifi\_status\_id | enumerator | Valid values:<br>0: SSID of the connected AP<br>1: BSSID of the connected AP<br>2: Active channel<br>3: Connection status, 1 = not connected, 2 = Connected<br>4: RSSI value of the current connection; will return -32768, if not connected. |
| int\_val | integer | RSSI, Connection status  or Channel |
| bssid | mac\_addr | BSSID of the connected access point |

<a name="atuwapa" id="atuwapa"></a>
### **7.1.17 AT+UWAPA - Wi-Fi Access Point Activate**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPA` | Start an access point with the current access point configuration.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="atuwapd" id="atuwapd"></a>
### **7.1.18 AT+UWAPD - Wi-Fi Access Point Deactivate**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPD` | Brings down Wi-Fi access point and disconnect all connected stations<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="atuwapcp" id="atuwapcp"></a>
### **7.1.19 AT+UWAPCP - Wi-Fi AP Connection Parameters**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPCP=<ssid>[,<channel>]` | Sets connection parameters for the AP configuration<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UWAPCP?` | Read the current connection parameters |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWAPCP:<ssid>,<channel>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ssid | string | SSID<br><br>Valid length: 0..32 |
| channel | enumerator | channel<br><br>Valid values:<br>1: 1<br>2: 2<br>3: 3<br>4: 4<br>5: 5<br>6: 6<br>7: 7<br>8: 8<br>9: 9<br>10: 10<br>11: 11<br>36: 36<br>40: 40<br>44: 44<br>48: 48<br><br>Default value: 6 |

<a name="atuwapsw" id="atuwapsw"></a>
### **7.1.20 AT+UWAPSW - Wi-Fi AP Security WPA**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPSW=<passphrase>[,<wpa_version>]` | Sets WPA parameters for the AP config<br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| passphrase | string | Passphrase to use<br><br>Valid length: 8..63 |
| wpa\_version | enumerator | Valid values:<br>0: WPA 2<br><br>Default value: WPA 2 |

<a name="atuwapso" id="atuwapso"></a>
### **7.1.21 AT+UWAPSO - Wi-Fi AP Security Open**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPSO` | Sets security level to open for the AP config<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="atuwaps" id="atuwaps"></a>
### **7.1.22 AT+UWAPS - Wi-Fi AP Security**


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
| security\_mode | enumerator | The current security mode.<br><br>Valid values:<br>0: Open security<br>1: WPA security<br>2: EAP-TLS security<br>3: PEAP security |
| wpa\_version | enumerator | Valid values:<br>0: WPA 2<br><br>Default value: WPA 2 |

<a name="atuwapcs" id="atuwapcs"></a>
### **7.1.23 AT+UWAPCS - Wi-Fi Access Point Connected Stations**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPCS?` | Get a list of connected stations. One response will be sent for each connected station |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWAPCS:<mac>` | A station that is connected to the access point |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mac | mac\_addr | MAC address of the connected Wi-Fi Station |

<a name="atuwapnst" id="atuwapnst"></a>
### **7.1.24 AT+UWAPNST - Wi-Fi Access Point Network Status**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UWAPNST=<status_id>` | Show current status of Wi-Fi station network interface |
| `AT+UWAPNST?` | Show current status of Wi-Fi station network interface |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UWAPNST:<status_id>,<status_val>` | Send for every applicable status |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| status\_id | enumerator | Valid values:<br>0: The current IPv4 address.<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>1: The current subnet mask<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>2: The current gateway<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>3: The current primary DNS server<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>4: The current secondary DNS server<br>Note: If network is down this will be 0.0.0.0 regardless of IP setting<br><br>5: The current IPv6 link local address<br>Note: If network is down this will be [0000:0000:0000:0000:0000:0000:0000:0000] regardless of IP setting<br> |
| status\_val | ip\_addr | IP address |

<a name="u_72-unsolicited-response-codes" id="u_72-unsolicited-response-codes"></a>
## **7.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEWLU](#uewlu) | Event Wi-Fi Link Up |
| [+UEWLD](#uewld) | Event Wi-Fi Link Down |
| [+UEWSNU](#uewsnu) | Event Wi-Fi Station Network Up |
| [+UEWSND](#uewsnd) | Event Wi-Fi Station Network Down |
| [+UEWSRSI](#uewsrsi) | Event Wi-Fi Station Roaming Switch Initiated |
| [+UEWSRSF](#uewsrsf) | Event Wi-Fi Station Roaming Switch Failed |
| [+UEWSRSC](#uewsrsc) | Event Wi-Fi Station Roaming Switch Completed |
| [+UEWAPNU](#uewapnu) | Event Wi-Fi Access Point Network Up |
| [+UEWAPND](#uewapnd) | Event Wi-Fi Access Point Network Down |
| [+UEWAPU](#uewapu) | Event Wi-Fi Access Point Up |
| [+UEWAPD](#uewapd) | Event Wi-Fi Access Point Down |
| [+UEWAPSA](#uewapsa) | Event Wi-Fi Access Point Station Associated |
| [+UEWAPSDA](#uewapsda) | Event Wi-Fi Access Point Station Disassociated |

<a name="uewlu" id="uewlu"></a>
### **7.2.1 +UEWLU - Event Wi-Fi Link Up**

This event is sent when Wi-Fi Link goes up


**Syntax**<br>
```+UEWLU:<wlan_handle>,<bssid>,<channel>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| channel | integer | Connected channel |
| bssid | mac\_addr | BSSID of the connected access point |

<a name="uewld" id="uewld"></a>
### **7.2.2 +UEWLD - Event Wi-Fi Link Down**

This event is sent when Wi-Fi Link goes down


**Syntax**<br>
```+UEWLD:<wlan_handle>,<reason>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| reason | integer | Standard 802.11 reason codes |

<a name="uewsnu" id="uewsnu"></a>
### **7.2.3 +UEWSNU - Event Wi-Fi Station Network Up**

This event is sent when Wi-Fi Station network is up


**Syntax**<br>
```+UEWSNU```

<a name="uewsnd" id="uewsnd"></a>
### **7.2.4 +UEWSND - Event Wi-Fi Station Network Down**

This event is sent when Wi-Fi Station network is down


**Syntax**<br>
```+UEWSND```

<a name="uewsrsi" id="uewsrsi"></a>
### **7.2.5 +UEWSRSI - Event Wi-Fi Station Roaming Switch Initiated**

This event is sent during Wi-Fi Station Roaming when AP switch is initiated


**Syntax**<br>
```+UEWSRSI```

<a name="uewsrsf" id="uewsrsf"></a>
### **7.2.6 +UEWSRSF - Event Wi-Fi Station Roaming Switch Failed**

This event is sent during Wi-Fi Station Roaming when the switch to the new AP failed. After this event the module will try to reconnect to the configured SSID


**Syntax**<br>
```+UEWSRSF```

<a name="uewsrsc" id="uewsrsc"></a>
### **7.2.7 +UEWSRSC - Event Wi-Fi Station Roaming Switch Completed**

This event is sent during Wi-Fi Station Roaming when AP switch is completed


**Syntax**<br>
```+UEWSRSC:<wlan_handle>,<bssid>,<channel>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| wlan\_handle | integer | Handle to use for Wi-Fi config and connection<br><br>Valid values: 0 only |
| channel | integer | Connected channel |
| bssid | mac\_addr | BSSID of the connected access point |

<a name="uewapnu" id="uewapnu"></a>
### **7.2.8 +UEWAPNU - Event Wi-Fi Access Point Network Up**

This event is sent when Wi-Fi Access Point network is up


**Syntax**<br>
```+UEWAPNU```

<a name="uewapnd" id="uewapnd"></a>
### **7.2.9 +UEWAPND - Event Wi-Fi Access Point Network Down**

This event is sent when Wi-Fi Access Point network is down


**Syntax**<br>
```+UEWAPND```

<a name="uewapu" id="uewapu"></a>
### **7.2.10 +UEWAPU - Event Wi-Fi Access Point Up**

This event is sent when Wi-Fi Access Point is started


**Syntax**<br>
```+UEWAPU```

<a name="uewapd" id="uewapd"></a>
### **7.2.11 +UEWAPD - Event Wi-Fi Access Point Down**

This event is sent when Wi-Fi Access Point is stopped


**Syntax**<br>
```+UEWAPD```

<a name="uewapsa" id="uewapsa"></a>
### **7.2.12 +UEWAPSA - Event Wi-Fi Access Point Station Associated**

This event is sent when a Wi-Fi station has associated with the Wi-Fi Access point


**Syntax**<br>
```+UEWAPSA:<mac>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mac | mac\_addr | Mac address of the connected Wi-Fi station |

<a name="uewapsda" id="uewapsda"></a>
### **7.2.13 +UEWAPSDA - Event Wi-Fi Access Point Station Disassociated**

This event is sent when a Wi-Fi station has disassociated with the Wi-Fi Access point


**Syntax**<br>
```+UEWAPSDA:<mac>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mac | mac\_addr | MAC address of the connected Wi-Fi station |

<a name="socket" id="socket"></a>
# **8 Socket**

The socket AT commands are used for creating and interfacing TCP/UDP sockets.


<a name="u_81-at-commands" id="u_81-at-commands"></a>
## **8.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+USOCR](#atusocr) | Create Socket |
| [AT+USOPCR](#atusopcr) | Create Persistent Socket |
| [AT+USOTLS](#atusotls) | Socket TLS |
| [AT+USOC](#atusoc) | Socket Connect |
| [AT+USOP](#atusop) | Socket Persistent |
| [AT+USOPR](#atusopr) | Socket Persistent Remove |
| [AT+USOPL](#atusopl) | Socket Persistent List |
| [AT+USORM](#atusorm) | Socket Receive Mode |
| [AT+USOWS](#atusows) | Socket Write String |
| [AT+USOWB](#atusowb) | Socket Write Binary |
| [AT+USOCL](#atusocl) | Close socket |
| [AT+USORS](#atusors) | Read Socket String |
| [AT+USORB](#atusorb) | Socket Read Binary |
| [AT+USOE](#atusoe) | Socket Error |
| [AT+USOL](#atusol) | Socket Listen |
| [AT+USORF](#atusorf) | Socket Read From |
| [AT+USOPA](#atusopa) | Socket Peer Address |
| [AT+USOST](#atusost) | Socket Status |
| [AT+USOO](#atusoo) | Socket Options |
| [AT+USOH](#atusoh) | Socket Host by Name |

<a name="atusocr" id="atusocr"></a>
### **8.1.1 AT+USOCR - Create Socket**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOCR=<protocol>[,<preferred_protocol_type>]` | Creates a socket and associates it with the specified protocol (TCP or UDP).<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOCR:<socket_handle>` | Successful creation of socket. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| protocol | enumerator | IP protocol.<br><br>Valid values:<br>6: TCP<br>17: UDP |
| preferred\_protocol\_type | enumerator | Selects the IP address type to use.<br><br>Valid values:<br>0: IPv4 address.<br>1: IPv6 address.<br><br>Default value: 0 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="atusopcr" id="atusopcr"></a>
### **8.1.2 AT+USOPCR - Create Persistent Socket**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOPCR=<protocol>[,<preferred_protocol_type>]` | Creates a persistent socket and associates it with the specified protocol (TCP or UDP).<br>A persistent socket will automatically re-connect when connection is lost.<br>It can also be stored so that the connection initiated on boot.<br><br>Note: Only TCP client supported for persistent sockets.<br><br><br>Notes:<br>Can be stored using [AT&W](#atw). |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOPCR:<socket_handle>` | Successful creation of persistent socket. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| protocol | enumerator | IP protocol.<br><br>Valid values:<br>6: TCP<br>17: UDP |
| preferred\_protocol\_type | enumerator | Selects the IP address type to use.<br><br>Valid values:<br>0: IPv4 address.<br>1: IPv6 address.<br><br>Default value: 0 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="atusotls" id="atusotls"></a>
### **8.1.3 AT+USOTLS - Socket TLS**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOTLS=<socket_handle>,<tls_version>[,<ca_name>[,<client_cert_name>,<client_key_name>]]` | Add a TLS context to a socket. This is only valid for TCP client sockets. |
| `AT+USOTLS=<socket_handle>` | Get the TLS context information for a socket. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOTLS:<socket_handle>,<tls_version>,<ca_name>,<client_cert_name>,<client_key_name>` | Successful response with the TLS context information for the specified socket. The response includes the TLS version, CA name, client certificate name, and client key name. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| tls\_version | enumerator | Minimum TLS version to use<br><br>Valid values:<br>0: Disable TLS<br>1: TLS 1.2 or up |
| ca\_name | string | Name of the certificate authority (CA) certificate to use<br><br>Valid length: 1..32 |
| client\_cert\_name | string | Name of the client certificate to use<br><br>Valid length: 1..32 |
| client\_key\_name | string | Name of the private key for client certificate<br><br>Valid length: 1..32 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="atusoc" id="atusoc"></a>
### **8.1.4 AT+USOC - Socket Connect**

For a TCP socket, this command will perform the TCP negotiation (3-way handshake) to open a connection and for a UDP socket this command will just declare the remote host address and port for later use with other socket operations.



**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOC=<socket_handle>,<host_address>,<remote_port>` | Establish a peer-to-peer connection to the specified remote host on the given remote port. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| host\_address | string | Remote host IP address or domain name of the remote host.<br><br>Valid length: 0..128 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |


**Notes**<br>
This command is non-blocking by default (can be configured with ${ref:AT+USOO}).

**Notes for TCP sockets:**  
When socket is non-blocking (default), a connection is not fully set up until ${ref:+UESOC} URC is received.

**Notes for UDP sockets:**  
Errors will not be reported prior to an attempt to write or read data on the socket.
Since UDP is connectionless no ${ref:+UESOC} event will be sent, instead as soon as this command return OK the socket is ready for reading/writing data.


<a name="atusop" id="atusop"></a>
### **8.1.5 AT+USOP - Socket Persistent**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOP=<socket_handle>,<host_address>,<remote_port>` | Configure a TCP link with automatic re-connection. As opposed to [AT+USOC](#atusoc), this command will not initiate<br>a connection directly but is used for configuring a link that is automatically setup on boot.<br><br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| host\_address | string | Remote host IP address or domain name.<br><br>Valid length: 0..128 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |


**Example**<br>
Example of setting up a persistent TCP client connection that is loaded on boot:
AT+USOCR=6,0
AT+USOP=0,192.168.0.10,30123
AT&W
AT+CPWROFF
Please note that WiFi must also be setup.



**Notes**<br>
Only one configuration is supported at the moment.

Only TCP client is supported at the moment.


<a name="atusopr" id="atusopr"></a>
### **8.1.6 AT+USOPR - Socket Persistent Remove**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOPR=<config_id>` | Removes an persistent socket configuration created by [AT+USOPCR](#atusopcr).<br><br><br>Notes:<br>Can be stored using [AT&W](#atw). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| config\_id | integer | Configuration ID |


**Notes**<br>
The corresponding socket will be automatically closed.

<a name="atusopl" id="atusopl"></a>
### **8.1.7 AT+USOPL - Socket Persistent List**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOPL?` | List all persistent socket configurations.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOPL:<socket_handle>,<host_address>,<remote_port>` | The response for each persistent configuration. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| config\_id | integer | Configuration ID. |
| host\_address | string | Remote host IP address or domain name of the remote host.<br><br>Valid length: 0..128 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |

<a name="atusorm" id="atusorm"></a>
### **8.1.8 AT+USORM - Socket Receive Mode**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USORM=<read_mode>` | Set the mode in which you would like to receive data in AT mode.<br><br><br>Notes:<br>Any created sockets or created persistent sockets will use the same receive mode as was configured when they were created<br>Can be stored using [AT&W](#atw). |
| `AT+USORM?` | Read the current receive mode |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USORM:<read_mode>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| read\_mode | enumerator | Modes to read data in AT<br><br>Valid values:<br>0: Buffered mode<br>1: Direct String mode<br>2: Direct Binary Mode |

<a name="atusows" id="atusows"></a>
### **8.1.9 AT+USOWS - Socket Write String**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOWS=<socket_handle>,<string_data>` | Writes string data to the specified socket.<br>The command can be used for both TCP and UDP sockets after calling [AT+USOC](#atusoc). <br>If socket is not ready to be written, generic negative error will be returned. <br>Check BSD errno (see BSD standard) by calling [AT+USOE](#atusoe).<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOWS:<socket_handle>,<written_length>` | Successful write response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| written\_length | integer | Data length that was written. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| string\_data | string | Data encoded as ascii chars.<br><br>Valid length: 0..1000 |


**Notes**<br>
This command is non-blocking.

The command may respond writing less data than what was passed to the command.
This means that the socket transmit buffer is currently full and data not successfully written must be retransmitted later.


<a name="atusowb" id="atusowb"></a>
### **8.1.10 AT+USOWB - Socket Write Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOWB=<socket_handle>{binary_data}` | Writes binary data to the specified socket in binary mode. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOWB:<socket_handle>,<written_length>` | Successful write response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| written\_length | integer | Data length that was actually written to socket. |
| binary\_data | binary | The data to write. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |


**Notes**<br>
This command is non-blocking.

The command may respond writing less data than what was passed to the command.
This means that the socket transmit buffer is currently full and data not successfully written must be retransmitted later.


<a name="atusocl" id="atusocl"></a>
### **8.1.11 AT+USOCL - Close socket**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOCL=<socket_handle>` | Closes the specified socket.<br><br>The command blocks the AT command interface until the completion of the socket close operation.<br>When this function returns OK the socket is cleaned up and fully closed.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_handle | integer | Socket identifier to be used for any future operation on that socket.<br><br>Valid values: 0..256 |

<a name="atusors" id="atusors"></a>
### **8.1.12 AT+USORS - Read Socket String**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USORS=<socket_handle>,<length>` | Reads the specified amount of data from the specified socket.<br>Note that the data should include no null terminator characters.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USORS:<socket_handle>,<length>,<string_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| length | integer | Number of bytes to read.<br><br>Valid values: 1..1000 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| string\_data | string | Data encoded as ascii chars.<br><br>Valid length: 0..1000 |


**Notes**<br>
This command is non-blocking.

<a name="atusorb" id="atusorb"></a>
### **8.1.13 AT+USORB - Socket Read Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USORB=<socket_handle>,<length>` | Reads the specified amount of data from the specified socket in binary mode.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USORB:<socket_handle>{binary_data}` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| length | integer | Number of bytes to read.<br><br>Valid values: 1..1000 |
| binary\_data | binary | The available data. Please note that the number of bytes may be less than requested. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="atusoe" id="atusoe"></a>
### **8.1.14 AT+USOE - Socket Error**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOE` | Retrieves the last error that occurred in any socket operation, stored in the socket errno. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOE:<error_code>` | Successful response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| error\_code | integer | BSD error code. See BSD standard for error code definitions. |

<a name="atusol" id="atusol"></a>
### **8.1.15 AT+USOL - Socket Listen**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOL=<socket_handle>,<port>` | Sets the specified socket in listening mode on the specified port of service, waiting for incoming connections (TCP) or data (UDP). |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| port | integer | Port of service, range 1-65535. Port numbers below 1024 are not recommended since they are usually reserved<br><br>Valid values: 1..65535 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |


**Notes**<br>
For TCP sockets this command corresponds to BSD bind + listen and for UDP sockets BSD bind.

<a name="atusorf" id="atusorf"></a>
### **8.1.16 AT+USORF - Socket Read From**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USORF=<socket_handle>,<length>` | Reads the specified amount of data from the specified UDP socket. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USORF:<socket_handle>,<remote_ip>,<remote_port>,<length>,<string_data>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| length | integer | Number of bytes to read.<br><br>Valid values: 1..900 |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_ip | ip\_addr | The ip address of the remote peer. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |
| string\_data | string | Data encoded as ascii chars.<br><br>Valid length: 0..1000 |

<a name="atusopa" id="atusopa"></a>
### **8.1.17 AT+USOPA - Socket Peer Address**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOPA=<socket_handle>` | Get the address of remote peer. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOPA:<socket_handle>,<remote_ip>,<remote_port>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_ip | ip\_addr | The ip address of the remote peer. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |

<a name="atusost" id="atusost"></a>
### **8.1.18 AT+USOST - Socket Status**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOST?` | List status for all created sockets. |
| `AT+USOST=<socket_handle>` | Get the status of a specific socket. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOST:<socket_handle>,<protocol>,<socket_status>` | Response for each created socket. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_status | enumerator | Valid values:<br>0: Not Connected<br>1: Listening<br>2: Connected |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| protocol | enumerator | IP protocol.<br><br>Valid values:<br>6: TCP<br>17: UDP |

<a name="atusoo" id="atusoo"></a>
### **8.1.19 AT+USOO - Socket Options**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOO=<socket_handle>,<option>,<value>` | Set a socket option. See available options below. |
| `AT+USOO=<socket_handle>,<option>` | Read a socket option for a socket |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOO:<socket_handle>,<option>,<value>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| option | enumerator | Available options to set<br><br>Valid values:<br>0: Turn on/off No delay feature for TCP sockets.<br>Integer flag: 0 = off (i.e. Nagle algorithm enabled), 1 = on  (i.e. Nagle algorithm disabled)<br>Default: to 0<br><br>1: Set socket to be blocking or non blocking.<br>Integer flag: 0 = off, 1 = on.<br>Sockets are non-blocking by default (Note that read/write will always be non-blocking).<br>Can only be set while the socket is in a non connected state.<br>Note: Only valid for non-persistent TCP sockets, will have no effect on UDP sockets<br><br>2: Keep connections alive by sending keepalive probes.<br>Integer flag: 0 = off, 1 = on.<br>To calculate the keepalive time us this formula KeepIdle + (KeepIntvl * KeepCnt).<br>Defaults to 1.<br>Note: Only valid for TCP sockets.<br><br>3: Set Keep Idle value for the socket.<br>This specifies the amount of time (in sec) that the connection must be idle before sending keepalive probes (if keepalive is enabled).<br>Defaults to 3.<br>Note: Only valid for TCP sockets.<br><br>4: Set keep alive interval value for the socket. This is the time in seconds between two successive keepalive retransmissions. <br>Defaults to 3.<br>Note: Only valid for TCP sockets.<br><br>5: Set keep alive counter value for the socket.<br>The number of unanswered probes required to force closure of the socket.<br>Defaults to 3.<br>Note: Only valid for TCP sockets.<br> |
| value | integer | See option parameter |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="atusoh" id="atusoh"></a>
### **8.1.20 AT+USOH - Socket Host by Name**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USOH=<host_name>` | Does a DNS lookup of a host name and returns the IP address. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USOH:<host_ip>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| host\_name | string | Name to lookup.<br><br>Valid length: 0..128 |
| host\_ip | ip\_addr | The ip address of the host. |

<a name="u_82-unsolicited-response-codes" id="u_82-unsolicited-response-codes"></a>
## **8.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UESOC](#uesoc) | Event Socket Connection |
| [+UESODA](#uesoda) | Event Socket Data Available |
| [+UESODS](#uesods) | Event Socket Data String |
| [+UESODSF](#uesodsf) | Event Socket Data String From |
| [+UESODB](#uesodb)} | Event Socket Data Binary |
| [+UESODBF](#uesodbf)} | Event Socket Data Binary From |
| [+UESOCL](#uesocl) | Event Socket Closed |
| [+UESOIC](#uesoic) | Event Socket Incoming Connection |

<a name="uesoc" id="uesoc"></a>
### **8.2.1 +UESOC - Event Socket Connection**

Event is sent out after a successful connection to a remote peer.


**Syntax**<br>
```+UESOC:<socket_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |


**Notes**<br>
TCP only.

<a name="uesoda" id="uesoda"></a>
### **8.2.2 +UESODA - Event Socket Data Available**

Data is available to be read. This will be sent out when using the buffered data mode.


**Syntax**<br>
```+UESODA:<socket_handle>,<number_bytes>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| number\_bytes | integer | Number of bytes available to read. If socket is a UDP socket this number refers to the size of the next datagram. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="uesods" id="uesods"></a>
### **8.2.3 +UESODS - Event Socket Data String**

Incoming on TCP socket data represented as a string.


**Syntax**<br>
```+UESODS:<socket_handle>,<string_data>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| string\_data | string | Data encoded as ascii chars.<br><br>Valid length: 0..1000 |

<a name="uesodsf" id="uesodsf"></a>
### **8.2.4 +UESODSF - Event Socket Data String From**

Incoming on UDP socket data represented as a string.


**Syntax**<br>
```+UESODSF:<socket_handle>,<remote_ip>,<remote_port>,<string_data>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_ip | ip\_addr | The ip address of the remote peer. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |
| string\_data | string | Data encoded as ascii chars.<br><br>Valid length: 0..1000 |

<a name="uesodb" id="uesodb"></a>
### **8.2.5 +UESODB - Event Socket Data Binary**

Incoming on TCP socket data represented as binary data.


**Syntax**<br>
```+UESODB:<socket_handle>{binary_data}```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The received data. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |

<a name="uesodbf" id="uesodbf"></a>
### **8.2.6 +UESODBF - Event Socket Data Binary From**

Incoming on UDP socket data represented as binary data.


**Syntax**<br>
```+UESODBF:<socket_handle>,<remote_ip>,<remote_port>{binary_data}```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The received data. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_ip | ip\_addr | The ip address of the remote peer. |
| remote\_port | integer | The port of the remote peer.<br><br>Valid values: 1..65535 |

<a name="uesocl" id="uesocl"></a>
### **8.2.7 +UESOCL - Event Socket Closed**

Event is sent out either when a socket was closed (by the remote or timed out) or when a connection to a remote peer has failed.
When this event is sent out the socket has been fully closed and the handle can be re-used.



**Syntax**<br>
```+UESOCL:<socket_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |


**Notes**<br>
If there are unread data available, this event will not be sent out until all data has been read.

<a name="uesoic" id="uesoic"></a>
### **8.2.8 +UESOIC - Event Socket Incoming Connection**

This event is sent when there is an incoming connection for a server socket.


**Syntax**<br>
```+UESOIC:<socket_handle>,<remote_ip>,<listening_socket_handle>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| listening\_socket\_handle | integer | The handle of the new connected socket. Use this for any further operations on the connection. |
| socket\_handle | integer | Socket identifier be used for any operation on that socket. |
| remote\_ip | ip\_addr | The ip address of the remote peer. |

<a name="mqtt" id="mqtt"></a>
# **9 MQTT**

MQTT Commands

<a name="u_91-at-commands" id="u_91-at-commands"></a>
## **9.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UMQCP](#atumqcp) | MQTT Connection Parameters |
| [AT+UMQC](#atumqc) | MQTT Connect to Broker |
| [AT+UMQKA](#atumqka) | MQTT Keep Alive |
| [AT+UMQLWT](#atumqlwt) | MQTT Last Will and Testament |
| [AT+UMQTLS](#atumqtls) | MQTT TLS Configuration |
| [AT+UMQDC](#atumqdc) | MQTT Disconnect |
| [AT+UMQPS](#atumqps) | MQTT Publish String |
| [AT+UMQPB](#atumqpb) | MQTT Publish Binary |
| [AT+UMQS](#atumqs) | MQTT Subscribe |
| [AT+UMQRS](#atumqrs) | MQTT Read String |
| [AT+UMQRB](#atumqrb) | MQTT Read Binary |

<a name="atumqcp" id="atumqcp"></a>
### **9.1.1 AT+UMQCP - MQTT Connection Parameters**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQCP=<mqtt_id>,<hostname>,<port>[,<client_id>[,<username>[,<password>]]]` | Set the MQTT connection parameters.<br><br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UMQCP=<mqtt_id>` | Get the MQTT connection parameters.<br> |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UMQCP:<mqtt_id>,<hostname>,<port>,<client_id>,<username>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| hostname | string | Hostname or IP address of the broker<br><br>Valid length: 0..128 |
| port | integer | The port of the broker<br><br>Valid values: 1..65535 |
| client\_id | string | Client ID. Can be left empty to let the broker decide<br><br>Valid length: 0..128 |
| username | string | Valid length: 0..128 |
| password | string | Valid length: 0..128 |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |


**Notes**<br>
Empty strings for username and password mean they will not be used during the connection.

<a name="atumqc" id="atumqc"></a>
### **9.1.2 AT+UMQC - MQTT Connect to Broker**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQC=<mqtt_id>` | Connect to a broker using the MQTT config ID. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |

<a name="atumqka" id="atumqka"></a>
### **9.1.3 AT+UMQKA - MQTT Keep Alive**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQKA=<mqtt_id>,<keep_alive>` | Set keepalive timeout for MQTT the MQTT config<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UMQKA=<mqtt_id>` | Get keepalive timeout for MQTT config |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UMQKA:<mqtt_id>,<keep_alive>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| keep\_alive | integer | MQTT keepalive in seconds. If set to 0, no keepalive is used<br><br>Valid values: 0..65535<br><br>Default value: 60 |

<a name="atumqlwt" id="atumqlwt"></a>
### **9.1.4 AT+UMQLWT - MQTT Last Will and Testament**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQLWT=<mqtt_id>,<topic>,<will_msg>[,<qos>[,<retain>]]` | Add last will and testament configuration for the client<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UMQLWT=<mqtt_id>` | Get last will and testament configuration for the client |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UMQLWT:<mqtt_id>,<topic>,<will_msg>,<qos>,<retain>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| will\_msg | string | Valid length: 0..256 |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| topic | string | Topic name or filter (wildcard allowed)<br><br>Valid length: 0..256 |
| qos | enumerator | Quality of Service (QoS) for the message or topic<br><br>Valid values:<br>0: At most once<br>1: At least once<br>2: Exactly once<br><br>Default value: 0 |
| retain | enumerator | Retain flag for message<br><br>Valid values:<br>0: Do not retain message on broker<br>1: Retain message on broker<br><br>Default value: 0 |

<a name="atumqtls" id="atumqtls"></a>
### **9.1.5 AT+UMQTLS - MQTT TLS Configuration**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQTLS=<mqtt_id>,<tls_version>[,<ca_name>[,<client_cert_name>,<client_key_name>]]` | Setup MQTT TLS config. Certs do not have to be uploaded until connection.<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+UMQTLS=<mqtt_id>` | Get TLS config |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UMQTLS:<mqtt_id>,<tls_version>,<ca_name>,<client_cert_name>,<client_key_name>` | Successful read response |
| `+UMQTLS:<mqtt_id>,<tls_version>` | Successful read response with TLS off |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| tls\_version | enumerator | Minimum TLS version to use<br><br>Valid values:<br>0: Disable TLS<br>1: TLS 1.2 or up |
| ca\_name | string | Name of the certificate authority (CA) certificate to use<br><br>Valid length: 1..32 |
| client\_cert\_name | string | Name of the client certificate to use<br><br>Valid length: 1..32 |
| client\_key\_name | string | Name of the private key for client certificate<br><br>Valid length: 1..32 |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |

<a name="atumqdc" id="atumqdc"></a>
### **9.1.6 AT+UMQDC - MQTT Disconnect**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQDC=<mqtt_id>` | Disconnect the MQTT client from the broker.<br>Note that the disconnection is not complete until the [+UEMQDC](#uemqdc) URC arrives.<br> |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |

<a name="atumqps" id="atumqps"></a>
### **9.1.7 AT+UMQPS - MQTT Publish String**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQPS=<mqtt_id>,<qos>,<retain>,<topic>,<message>` | Publish an MQTT message in string format to the specified topic. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| qos | enumerator | Quality of Service (QoS) for the message or topic<br><br>Valid values:<br>0: At most once<br>1: At least once<br>2: Exactly once<br><br>Default value: 0 |
| retain | enumerator | Retain flag for message<br><br>Valid values:<br>0: Do not retain message on broker<br>1: Retain message on broker<br><br>Default value: 0 |
| topic | string | Topic name or filter (wildcard allowed)<br><br>Valid length: 0..256 |
| message | string | MQTT message<br><br>Valid length: 0..730 |

<a name="atumqpb" id="atumqpb"></a>
### **9.1.8 AT+UMQPB - MQTT Publish Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQPB=<mqtt_id>,<qos>,<retain>,<topic>{binary_data}` | Publish an MQTT message in binary format to the specified topic. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The MQTT message data. |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| qos | enumerator | Quality of Service (QoS) for the message or topic<br><br>Valid values:<br>0: At most once<br>1: At least once<br>2: Exactly once<br><br>Default value: 0 |
| retain | enumerator | Retain flag for message<br><br>Valid values:<br>0: Do not retain message on broker<br>1: Retain message on broker<br><br>Default value: 0 |
| topic | string | Topic name or filter (wildcard allowed)<br><br>Valid length: 0..256 |

<a name="atumqs" id="atumqs"></a>
### **9.1.9 AT+UMQS - MQTT Subscribe**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQS=<mqtt_id>,<subscribe_action>,<topic>[,<qos>]` | Subscribe or unsubscribe to/from MQTT topic. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| subscribe\_action | enumerator | Valid values:<br>0: Subscribe to topic<br>1: Unsubscribe from topic |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| topic | string | Topic name or filter (wildcard allowed)<br><br>Valid length: 0..256 |
| qos | enumerator | Quality of Service (QoS) for the message or topic<br><br>Valid values:<br>0: At most once<br>1: At least once<br>2: Exactly once<br><br>Default value: 0 |

<a name="atumqrs" id="atumqrs"></a>
### **9.1.10 AT+UMQRS - MQTT Read String**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQRS=<mqtt_id>` | Read available MQTT message in string format. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UMQRS:<mqtt_id>,<topic>,<message_len>,<message>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| topic | string | Topic name or filter (wildcard allowed)<br><br>Valid length: 0..256 |
| message\_len | integer | Length of the MQTT message |
| message | string | MQTT message<br><br>Valid length: 0..730 |

<a name="atumqrb" id="atumqrb"></a>
### **9.1.11 AT+UMQRB - MQTT Read Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UMQRB=<mqtt_id>` | Read available MQTT message in binary format. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UMQRB:<mqtt_id>,<topic>{binary_data}` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The MQTT message data. |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| topic | string | Topic name or filter (wildcard allowed)<br><br>Valid length: 0..256 |

<a name="u_92-unsolicited-response-codes" id="u_92-unsolicited-response-codes"></a>
## **9.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEMQC](#uemqc) | Event MQTT Connected |
| [+UEMQDC](#uemqdc) | Event MQTT Disconnected |
| [+UEMQDA](#uemqda) | Event MQTT Data Available |

<a name="uemqc" id="uemqc"></a>
### **9.2.1 +UEMQC - Event MQTT Connected**

Connected to MQTT broker


**Syntax**<br>
```+UEMQC:<mqtt_id>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |

<a name="uemqdc" id="uemqdc"></a>
### **9.2.2 +UEMQDC - Event MQTT Disconnected**

Disconnected from MQTT Broker


**Syntax**<br>
```+UEMQDC:<mqtt_id>,<disconnect_reason>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| disconnect\_reason | integer | Disconnection reason |
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |

<a name="uemqda" id="uemqda"></a>
### **9.2.3 +UEMQDA - Event MQTT Data Available**


**Syntax**<br>
```+UEMQDA:<mqtt_id>,<message_len>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| mqtt\_id | integer | MQTT Config ID<br><br>Valid values: 0 only |
| message\_len | integer | Length of the MQTT message |

<a name="security" id="security"></a>
# **10 Security**

Security AT commands

<a name="u_101-at-commands" id="u_101-at-commands"></a>
## **10.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+USECR](#atusecr) | Security Certificate Remove |
| [AT+USECUB](#atusecub) | Security Certificate Upload Binary |
| [AT+USECL](#atusecl) | Security Certificates List |
| [AT+USETE](#atusete) | Security TLS Extensions |
| [AT+USETE0](#atusete0) | Security TLS Extensions Server Name Indication |
| [AT+USETE1](#atusete1) | Security TLS Extensions Handshake Fragmentation |

<a name="atusecr" id="atusecr"></a>
### **10.1.1 AT+USECR - Security Certificate Remove**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USECR=<cert_type>,<name>` | Remove a single X.509 certificate or private key. |
| `AT+USECR` | Remove all X.509 certificates and private keys. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| cert\_type | enumerator | Valid values:<br>0: Root certificate<br>1: Client certificate<br>2: Client private key |
| name | string | Valid length: 1..32 |

<a name="atusecub" id="atusecub"></a>
### **10.1.2 AT+USECUB - Security Certificate Upload Binary**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USECUB=<cert_type>,<name>{binary_data}` | Write an X.509 certificate or private key using binary transfer. |
| `AT+USECUB=<cert_type>,<name>,<password>{binary_data}` | Write an X.509 certificate or private key with password using binary transfer. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| binary\_data | binary | The certificate data. |
| cert\_type | enumerator | Valid values:<br>0: Root certificate<br>1: Client certificate<br>2: Client private key |
| name | string | Valid length: 1..32 |
| password | string | Decryption password; applicable only for PKCS8 encrypted client private keys. The maximum length is 64 characters.<br>NOTE: Supported Encryption method for private keys is AES only<br><br><br>Valid length: 1..64 |


**Notes**<br>
Note that the size of the certificate can be maximum 15360 bytes and that maximum 8 certs (or cert chains) can be stored simultaneously

<a name="atusecl" id="atusecl"></a>
### **10.1.3 AT+USECL - Security Certificates List**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USECL?` | Read all uploaded certificate names |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USECL:<cert_type>,<name>` | Successful read response. Note that there will be one response per certificate |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| cert\_type | enumerator | Valid values:<br>0: Root certificate<br>1: Client certificate<br>2: Client private key |
| name | string | Valid length: 1..32 |

<a name="atusete" id="atusete"></a>
### **10.1.4 AT+USETE - Security TLS Extensions**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USETE?` | Read all TLS extension settings |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USETE:<extension>,<enabled>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| extension | enumerator | Valid values:<br>0: Server Name Extension<br>1: Handshake fragmentation |
| enabled | enumerator | Valid values:<br>0: Disabled<br>1: Enabled |

<a name="atusete0" id="atusete0"></a>
### **10.1.5 AT+USETE0 - Security TLS Extensions Server Name Indication**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USETE0=<enabled>` | Turn Server Name Indication TLS extension on and off on a system level<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USETE0?` | Read Server Name Indication setting |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USETE0:<enabled>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| enabled | enumerator | Valid values:<br>0: Disabled<br>1: Enabled |

<a name="atusete1" id="atusete1"></a>
### **10.1.6 AT+USETE1 - Security TLS Extensions Handshake Fragmentation**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+USETE1=<enabled>` | Turn Handshake Fragmentation TLS extension on and off on a system level<br><br>Notes:<br>Can be stored using [AT&W](#atw). |
| `AT+USETE1?` | Read Handshake Fragmentation setting |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+USETE1:<enabled>` | Successful read response |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| enabled | enumerator | Valid values:<br>0: Disabled<br>1: Enabled |

<a name="power" id="power"></a>
# **11 Power**

<a name="u_111-at-commands" id="u_111-at-commands"></a>
## **11.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UPMDS](#atupmds) | Power Management Deep Sleep |
| [AT+UPMPSTO](#atupmpsto) | Power Management Power Save Timeout |

<a name="atupmds" id="atupmds"></a>
### **11.1.1 AT+UPMDS - Power Management Deep Sleep**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UPMDS` | Enter Deep Sleep Mode. |

<a name="atupmpsto" id="atupmpsto"></a>
### **11.1.2 AT+UPMPSTO - Power Management Power Save Timeout**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UPMPSTO=<timeoutMs>` | Set Power Save active state timeout in milli second . |
| `AT+UPMPSTO?` | Read Power Save active state TO. |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UPMPSTO:<timeoutMs>` | Response with current active state timeout value in milli second. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| timeoutMs | integer | Active state timeout ms<br><br>Valid values: 1..60000<br><br>Default value: 1000 |

<a name="transparent" id="transparent"></a>
# **12 Transparent**

Transparent Mode AT commands. In transparent mode all data that is sent from the host to the UART is
forwarded to the socket or SPS link that is configured for transparent mode, and the all data that arrives
on this link is sent to the UART.
Transparent mode is limited to one link at a time.


<a name="u_121-at-commands" id="u_121-at-commands"></a>
## **12.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UTM](#atutm) | Transparent Mode |
| [AT+UTMP](#atutmp) | Transparent Mode Persistent |
| [AT+UTMPC](#atutmpc) | Transparent Mode Persistent Clear |

<a name="atutm" id="atutm"></a>
### **12.1.1 AT+UTM - Transparent Mode**

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

<a name="atutmp" id="atutmp"></a>
### **12.1.2 AT+UTMP - Transparent Mode Persistent**

This command is used for automatically setting up a transparent mode connection on boot.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UTMP=<link_type>,<config_id>` | Set persistent transparent mode for link<br><br>Notes:<br>Requires [AT&W](#atw) and a reboot before taking effect. |
| `AT+UTMP?` | Get current persistent transparent mode configuration |

| <div style="width:350px">Response</div> | Description |
| ----------|----------|
| `+UTMP:<link_type_read>,<config_id>` | Successful read response. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| config\_id | integer | For SPS, set this to the config_id returned by [AT+UBTP](#atubtp).<br>For sockets, set this to the config_id returned by [AT+USOP](#atusop).<br> |
| link\_type | enumerator | Valid values:<br>0: BLE SPS Link<br>1: Socket |
| link\_type\_read | enumerator | Valid values:<br>-1: No link type set<br>0: BLE SPS Link<br>1: Socket |

<a name="atutmpc" id="atutmpc"></a>
### **12.1.3 AT+UTMPC - Transparent Mode Persistent Clear**

Clears the persistent link configuration for transparent mode.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UTMPC` | Clears persistent transparent mode settings<br><br>Notes:<br>Can be stored using [AT&W](#atw). |

<a name="diagnostics" id="diagnostics"></a>
# **13 Diagnostics**

Diagnostics Tools

<a name="u_131-at-commands" id="u_131-at-commands"></a>
## **13.1 AT Commands**

| AT Command | Description |
| ----------|----------|
| [AT+UDGP](#atudgp) | Diagnostics Ping |
| [AT+UDGSP](#atudgsp) | Stop an ongoing Ping |
| [AT+UDGI](#atudgi) | Diagnostics Iperf |

<a name="atudgp" id="atudgp"></a>
### **13.1.1 AT+UDGP - Diagnostics Ping**

Send a ping command.


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UDGP=<destination>[,<count>]` | Sends a ping command to a destination address every second, repeating it (count) times. |


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| destination | string | Destination host to send a ping call to in the form of an IPv4 address (i.e. 192.168.1.10) or hostname (i.e. www.u-blox.com).<br><br>Valid length: 4..80 |
| count | integer | The number of pings (or packets) that will be transmitted. 0 means ping continuously.<br><br>Valid values: 0..65535<br><br>Default value: 4 |

<a name="atudgsp" id="atudgsp"></a>
### **13.1.2 AT+UDGSP - Stop an ongoing Ping**


**Syntax**<br>
| <div style="width:350px">AT Command</div> | Description |
| ----------|----------|
| `AT+UDGSP` | This command will stop any ping in progress.<br><br><br>Notes:<br>The command is asynchronous, and the ping will not be interrupted immediately, but right after the next ping packet has a response, which might take a few seconds if the packet response times out. This command always returns OK and does nothing if there is no ping in progress. |

<a name="atudgi" id="atudgi"></a>
### **13.1.3 AT+UDGI - Diagnostics Iperf**


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
| port | integer | Port |
| report\_interval | integer | Report interval |
| time\_boundary | integer | Time boundary. Client only. Ignored if role is server |
| ip\_addr | ip\_addr | IP address to connect to. Client only. Ignored if role is server |
| bandwidth | integer | Bandwidth to be used for UDP |
| length | integer | Size of packets.<br><br>Valid values: 1..1460<br><br>Default value: 1460 |
| bidirectional | enumerator | Bidirectional flag. Client only. Ignored if role is server<br><br>Valid values:<br>0: Off<br>1: On<br>When starting bidirectional TCP test, start a server on both tester and DUT, then start a client with bidirectional flag on the DUT.<br>If doing bidirectional UDP test, start a server on both DUT and tester and then start a client with a bidirectional flag on both.<br> |

<a name="u_132-unsolicited-response-codes" id="u_132-unsolicited-response-codes"></a>
## **13.2 Unsolicited Response Codes**

| Unsolicited Response Code | Description |
| ----------|----------|
| [+UEDGPC](#uedgpc) | Ping Complete Event |
| [+UEDGP](#uedgp) | Event Ping Response |
| [+UEDGI](#uedgi) | Event Iperf output |

<a name="uedgpc" id="uedgpc"></a>
### **13.2.1 +UEDGPC - Ping Complete Event**

Event is sent out with a summary of the ping results after all packets are transmitted.


**Syntax**<br>
```+UEDGPC:<transmitted_packets>,<received_packets>,<packet_loss_rate>,<avg_response_time>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| transmitted\_packets | integer | Total number of packets transmitted successfully. |
| received\_packets | integer | Total number of packets received successfully. |
| packet\_loss\_rate | integer | Packet loss rate in percentage between transmitted and received packets. |
| avg\_response\_time | integer | Average ping response time in milliseconds. |

<a name="uedgp" id="uedgp"></a>
### **13.2.2 +UEDGP - Event Ping Response**

Event is sent out when a single ping has a result.


**Syntax**<br>
```+UEDGP:<ping_response>,<response_time>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| ping\_response | enumerator | Ping Response result. 0 - ping failed, 1 - ping successful<br><br>Valid values:<br>0: Ping failed.<br>1: Ping succeeded. |
| response\_time | integer | Ping response time in milliseconds. |

<a name="uedgi" id="uedgi"></a>
### **13.2.3 +UEDGI - Event Iperf output**

Event is sent out for all output string send by iperf tool


**Syntax**<br>
```+UEDGI:<iperf_output>```


**Defined values**<br>
| Parameter | Type | Description |
| ----------|----------|----------|
| iperf\_output | string | Iperf readable output string<br><br>Valid length: 0..99 |

