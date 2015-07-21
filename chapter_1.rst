Supported Systems
=========

Z-Wave
--------
Z-Wave technology minimizes power consumption so that it is suitable for battery-operated devices. Z-Wave is designed to provide, reliable, low-latency transmission of small data packets at data rates up to 100kbit/s,[1] unlike Wi-Fi and other IEEE 802.11-based wireless LAN systems that are designed primarily for high data rates. Z-Wave operates in the sub-gigahertz frequency range, around 900 MHz. This band competes with some cordless telephones and other consumer electronics devices, but avoids interference with Wi-Fi, Bluetooth and other systems that operate on the crowded 2.4 GHz band. Z-Wave is designed to be easily embedded in consumer electronics products, including battery operated devices such as remote controls, smoke alarms and security sensors.

Z-Wave components must be reported to the jOS. To do this, the Z-Wave interface has to be set to the Include Mode. The Include Mode is active for around 30 seconds. The relevant Z-Wave device has to be picked up within that time. This occurs as a rule by tapping the Mode or Program key three times at short intervals (1s). The exact procedure can be found in the description of the devices being used.

A successful reporting of the Z-Wave components to the jOS system is possible only if the components are also present in the Z-Wave databank. There is also the possibility to create one’s own databank files and to introduce them manually into the databank of the jOS. In this case, the appropriate commands are available. If you happen to have a component that is not recognized, we nevertheless recommand that you contact JUCEBOX Support to get it added.

The Z-Wave databank of the jOS is based on the data of Pepper One GmbH (http://www.pepper1.net), the certification arm of the Z-Wave Alliance. The jOS system has direct access to the updates of the Pepper One Datenbank. It is therefore recommended that any updating of the databank be accomplished before the inclusion of new devices. An appropriate possibility for this purpose is available in the Admin Portal

ZigBee
--------
The jOS supports ZigBee, ZigBee is a specification for a suite of high-level communication protocols used to create personal area networks built from small, low-power digital radios. ZigBee is based on an IEEE 802.15.4 standard. Its low power consumption limits transmission distances to 10–100 meters line-of-sight, depending on power output and environmental characteristics,[1] ZigBee devices can transmit data over long distances by passing data through a mesh network of intermediate devices to reach more distant ones. ZigBee is typically used in low data rate applications that require long battery life and secure networking (ZigBee networks are secured by 128 bit symmetric encryption keys.) ZigBee has a defined rate of 250 kbit/s, best suited for intermittent data transmissions from a sensor or input device. Applications include wireless light switches, electrical meters with in-home-displays, traffic management systems, and other consumer and industrial equipment that requires short-range low-rate wireless data transfer. The technology defined by the ZigBee specification is intended to be simpler and less expensive than other wireless personal area networks (WPANs), such as Bluetooth or Wi-Fi.

Bluetooth 4.2
--------
Bluetooth is a wireless technology standard for exchanging data over short distances (using short-wavelength UHF radio waves in the ISM band from 2.4 to 2.485 GHz[4]) from fixed and mobile devices, and building personal area networks (PANs). Invented by telecom vendor Ericsson in 1994,[5] it was originally conceived as a wireless alternative to RS-232 data cables. It can connect several devices, overcoming problems of synchronization.

Bluetooth is managed by the Bluetooth Special Interest Group (SIG), which has more than 25,000 member companies in the areas of telecommunication, computing, networking, and consumer electronics.[6] The IEEE standardized Bluetooth as IEEE 802.15.1, but no longer maintains the standard. The Bluetooth SIG oversees development of the specification, manages the qualification program, and protects the trademarks.[7] A manufacturer must make a device meet Bluetooth SIG standards to market it as a Bluetooth device.[8] A network of patents apply to the technology, which are licensed to individual qualifying devices.

IP - TCP/UDP
--------
It is commonly known as TCP/IP, because its most important protocols, the Transmission Control Protocol (TCP) and the Internet Protocol (IP), were the first networking protocols defined in this standard.

Most of the Important devices in building control, and IoT work on TCP/IP. 

IR (InfraRed)
---------

The jOS support IR though most IR/IP Interfces like Global Cache™. Full learning capibities of any device, with the ability to submit your device to us to add to the library of devices, Already we support most of the main manufactures.

JUCEBOX will ship with IR onboard, with a Sender and Reciever. These will be active in a later jOS release mid 2016

Philips HUE™
---------

The jOS also supports HUE Lighting of the Philips corporation. Recognition of the HUE Bridge in the network comes about fully automatically by tapping the „Learn“ Key of the bridge. The command class is then ready to use. No additional configuration file is needed. One can see in the log whether an HUE Bridge is recognized. When an HUE Bridge is on hand, specific data on the bridge will also be returned. The log also gives information on lighting fixtures reporting through the HUE Bridge

Note: A Later update will allow the HUE to connect without the Bridge.

Technical Data:

Maximum number of lamps: 50 per Bridge

Zigbee Light link: Protocol 1.0 certified

Frequency range: 2400-2483.5 MHz

SONOS
---------
Controlling Sonos music players. For every Speaker/Zone installed into the admin interface, an attempt will be made at System Start to establish a connection. The Sonos Engine is based on UPnP.

Sonos works with a queue system, the same as the SONOS App itself, You can control all the Music from the Librarys, Playlists, favourites and all the other SONOS music services. All the SONOS interface details are simalar to the Native App, the ability to join rooms together, control individual rooms seperatly and all the details from the track playing including album artwork has never been easier.

KNXnet/IP
---------
The jOS system also supports the KNXnet/IP protocol. This tie-in currently offers the best interface with KNX/EIB because it imposes practically no restriction on the number of datapoints and no additional parameters must be set up within the ETS, as would be necessary, for example, with the BAOS Object Server.

Both types of protocol, namely KNXnet/IP Routing and KNXnet/IP Tunneling, are supported. It is also possible to set up a „TUNNELING_BRIDGE“. Further explanation of this mode now follows.

The datapoint definitions are laid out in a separate file (knx.esf) in the misc folder. This file is subordinated to the OPC Export Format of the ETS and can be exported directly from ETS. All types of datapoints are supported. This also applies to the names defined therein for the Broadcast output and used in the Logging Monitor. Thus type-conversion and scaling occur automatically and require no further attention. An individual name for the .esf file can also be assigned. This can be adjusted in the CONFIG section of  knx.csv.

A log entry occurs for unknown types of data in the .esf file and the corresponding definition is disregarded. Datapoints which are not entered in the .esf file are ignored.

The following types of datapoints are currently supported:

EIS 1	‘Switching’ (1 Bit)
EIS 2	‘Dimming - position’ (1 Bit)
EIS 2	‘Dimming - control’ (4 Bit)
EIS 2	‘Dimming - value’ (8 Bit)
EIS 3	‘Time’ (3 Byte)
EIS 4	‘Date’ (3 Byte)
EIS 5	‘Value’ (2 Byte)
EIS 6	‘Scaling - percent’ (8 Bit)
EIS 6	‘Scaling - degree’ (8 Bit)
EIS 7	‘Drive control’ (1 Bit)
EIS 8	‘Priority - position’ (1 Bit)
EIS 8	‘Priority - control’ (2 Bit)
EIS 9	‘Float value’ (4 Byte)
EIS 10	‘16Bit Counter’ (2 Byte)
EIS 11	‘32Bit Counter’ (4 Byte)
EIS 12	‘Access’ (4 Byte)
EIS 13	‘EIB-ASCII-Char’ (8 Bit)
EIS 14	‘8Bit Counter’ (8 Bit)
EIS 15	‘Character String’ (14 Byte)

C-Bus/IP/RS232
---------


GIRA Homeserver KO-Gateway
---------
The jOS system supports bi-directional access to the GIRA Homserver KO-Gateway. This makes it possible for a simple transfer of data – from the exchange of information to gaining of access to EIB/KNX, In 2016 a fully connected App will be available for the Homeserver to control the JUCEBOX and allow control of any of the systems supported on JUCEBOX from the Homeserver though the Quad Client.

CEC (With Auto Discovery)
---------
Consumer Electronics Control or CEC is a function that allows you to control multiple devices over HDMI using one remote control by having a secondary device receive commands from a primary device. The jOS can auto discover 80% of all CEC Devices and control them without the need for IR immiters like Global Cache, Although CEC wiring is required for every HDMI port it does not mean that every HDMI port will have the function enabled.

A list of supported CEC Deviec will be made avalable by Early 2016. 

JUCEBOX Ltd will relase a HDMI(CEC) breakout box for controlling other CEC Devices not in reach of the JUCEBOX.


iTunes & Apple TV (Apple Remote)
---------

iTunes and AppleTV control. At System Start there is an attempt to connect each connected library or apple tv. When the application within iTunes or the Private-Clearance/Homesharing of AppleTV is activated, the jOS system recognizes this fully automatically. When this occurs, the rudimentary Remote Command set are at your disposal.

When the pairing is executed, an extended command set becomes available for control. The extended set of commands, however, is at hand solely for controlling a „remote“ iTunes. Always on hand for AppleTV, regardless of whether it is connected by Private-Clearance/Homesharing or through the Pairing Method, is only the rudimentary Remote Command Set.


.........................
