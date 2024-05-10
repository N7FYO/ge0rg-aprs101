APRS DATA IN THE AX.25 DESTINATION AND SOURCE ADDRESS FIELDS
============================================================

**The AX.25**

**Destination Address Field**

The AX.25 Destination Address field can contain 6 different types of
APRS information:

-  A generic APRS address.
-  A generic APRS address with a symbol.
-  An APRS software version number.
-  Mic-E encoded data.
-  A Maidenhead Grid Locator (obsolete).
-  An Alternate Net (ALTNET) address.


In all of these cases, the Destination Address SSID may specify a
generic APRS digipeater path.

**Generic APRS Destination Addresses**

APRS uses the following generic beacon-style destination addresses:

AIR\* †  ALL\*  AP\*  BEACON CQ\*  GPS\*  DF\*
DGPS\*  DRILL\* DX\*  ID\*  JAVA\* MAIL\*  MICE\*
QST\*  QTH\*  RTCM\*  SKY\*  SPACE\* SPC\*  SYM\*
TEL\*  TEST\* TLM\*  WX\*  ZIP\* †


The asterisk is a wildcard, allowing the address to be extended (up
to a total of 6 alphanumeric characters). Thus, for example, WX1,
WX12 and WX12CD are all valid APRS destination addresses.

† The **AIR**\* and **ZIP**\* addresses are being phased out, but
are needed at present for backward compatibility.

All of these addresses have an SSID of –0. Non-zero SSIDs are
reserved for generic APRS digipeating.

These addresses are copied by everyone. All APRS software must accept
packets with these destination addresses.

The address **GPS** (i.e. the 3-letter address **GPS**, not
**GPS\***) is specifically intended for use by trackers sending
lat/long positions via digipeaters which have the capability of
converting positions to compressed data format.

The addresses **DGPS** and **RTCM** are used by differential GPS
correction stations. Most software will not make use of packets using
this address, other than to pass them on to an attached GPS unit.

The address **SKY** is used for Skywarn stations.

Packets addressed to **SPCL** are intended for special events. APRS
software can display such packets to the exclusion of all others, to
minimize clutter on

the screen from other stations not involved in the special event. The
addresses **TEL** and **TLM** is used for telemetry stations.

**Generic APRS Address with**

**Symbol**

APRS uses several of the above-listed generic addresses in a special
way, to specify not only an address but also a display symbol. These
special addresses are GPSxyz, GPSCnn, GPSEnn, SPCxyz and SYMxyz, and
are intended for use where it is not possible to include the symbol
in the AX.25 Information field.

The GPS addresses above are for general use.

The SPC addresses are intended for special events. The SYM addresses
are reserved for future use.

The characters xy and nn refer to entries in the APRS Symbol Tables.
The character z specifies a symbol overlay. See Chapter 20: APRS
Symbols and Appendix 2 for more information.

**APRS Software Version Number**

The AX.25 Destination Address field can contain the version number of
the APRS software that is running at the station. Knowledge of the
version number can be useful when debugging.

The following software version types are reserved (xx and xxx
indicate a version number):

**APC** xxx APRS/CE, Windows CE

**APD** xxx Linux aprsd server

**APE** xxx PIC-Encoder

**API** xxx Icom radios (future)

**APIC**\ xx ICQ messaging

**APK**\ xxx Kenwood radios

**APM**\ xxx MacAPRS

**APP**\ xxx pocketAPRS

**APR**\ xxx APRSdos

**APRS**\ older versions of APRSdos

**APRSM**\ older versions of MacAPRS

**APRSW**\ older versions of WinAPRS

**APS**\ xxx APRS+SA

**APW**\ xxx WinAPRS

**APX**\ xxx X-APRS

**APY**\ xxx Yaesu radios (future)

**APZ**\ xxx Experimental

This table will be added to by the APRS Working Group.

For example, a station using version 3.2.6 of MacAPRS could use the

destination callsign APM326.

The Experimental destination is designated for *temporary* use only
while a product is being developed, before a special APRS Software
Version address is assigned to it.

**Mic-E Encoded**

**Data**

Another alternative use of the AX.25 Destination Address field is to
contain Mic-E encoded data. This data includes:

-  The latitude of the station.
-  A West/East Indicator and a Longitude Offset Indicator (used in
   longitude computations).
-  A Message Code.
-  The APRS digipeater path.


This data is used with associated data in the AX.25 Information field
to provide a complete Position Report and other information about the
station (see Chapter 10: Mic-E Data Format).

**Maidenhead Grid**

**Locator in Destination Address**

The AX.25 Destination Address field may contain a 6-character
Maidenhead Grid Locator. For example: **IO91SX**. This format is
typically used by meteor scatter and satellite operators who need to
keep packets as short as possible.

This format is now obsolete.

**Alternate Nets** Any other destination address not included in the
specific generic list or the other categories mentioned above may be
used in Alternate Nets (ALTNETs) by groups of individuals for special
purposes. Thus they can use the APRS infrastructure for a variety of
experiments without cluttering up the maps and lists of other APRS
stations. Only stations using the same ALTNET address should see
their data.

**Generic APRS Digipeater Path**

The SSID in the Destination Address field of all packets is coded to
specify the APRS digipeater path.

If the Destination Address SSID is –0, the packet follows the
standard AX.25 digipeater (“VIA”) path contained in the Digipeater
Addresses field of the AX.25 frame.

If the Destination Address SSID is non-zero, the packet follows one
of 15 generic APRS digipeater paths.

The SSID field in the Destination Address (i.e. in the 7th address
byte) is encoded as follows:

**APRS Digipeater Paths in Destination Address SSID**

**The AX.25 Source Address SSID to specify Symbols**

The AX.25 Source Address field contains the callsign and SSID of the
originating station. If the SSID is –0, APRS does not treat it in any
special way.

If, however, the Source Address SSID is non-zero, APRS interprets it
as a display icon. This is intended for use only with stand-alone
trackers where there is no other method of specifying a display
symbol or a destination address (e.g. MIM trackers or NMEA trackers).

For more information, see Chapter 20: APRS Symbols.
