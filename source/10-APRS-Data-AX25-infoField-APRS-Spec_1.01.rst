APRS DATA IN THE AX.25 INFORMATION FIELD
========================================

Generic Data

Format

Bytes:

APRS Data Type

Identifier

In general, the AX.25 Information field can contain some or all of
the following information:

-  APRS Data Type Identifier
-  APRS Data
-  APRS Data Extension
-  Comment

+----------------+----------------+----------------+----------------+
|    Generic     |    blank       |  foo           |  moo           |
|    APRS        |                |                |                |
|    Information |                |                |                |
|    Field       |                |                |                |
+================+================+================+================+
|    Data Type   |      APRS      |      APRS Data |      Comment   |
|    ID          |    Data        |    Extension   |                |
+----------------+----------------+----------------+----------------+
|    1           |    n           |    7           |    n           |
+----------------+----------------+----------------+----------------+


Every APRS packet contains an APRS Data Type Identifier (DTI). This
determines the format of the remainder of the data in the Information
field, as follows:

APRS Data Type Identifiers

Note: There is one exception to the requirement for the Data Type
Identifier to be the *first* character in the Information field —
this is the *Position without Timestamp* (indicated by the !
DTI). The ! character may occur *anywhere up to and including the
40th character position* in the Information field. This variability
is required to support X1J TNC digipeaters which have a string of
unmodifiable text at the beginning of the field.

Note: The Kenwood TM-D700 radio uses the ' DTI for *current*
Mic-E data. The radio does not use the ` DTI.

APRS Data and Data Extension

There are 10 main types of APRS Data:

-  Position
-  Direction Finding
-  Objects and Items
-  Weather
-  Telemetry
-  Messages, Bulletins and Announcements
-  Queries
-  Responses
-  Status
-  Other


Some of this data may also have an APRS Data Extension that provides
additional information.

The APRS Data and optional Data Extension follow the Data Type
Identifier.

The table on the next page shows a complete list of all the different
possible types of APRS Data and APRS Data Extension.

+----------------------+----------------------+----------------------+
|                      |    Possible APRS     | Possible APRS        |
|                      |    Data              | Data Extension       |
+======================+======================+======================+
| Position             |    Time (DHM or HMS) |    Course and Speed  |
|                      |    Lat/long          |                      |
|                      |    coordinates       |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |    Compressed        |    Height/           |
|                      |    lat/long/         |    Gain/Directivity  |
|                      |   course/speed/radio |    Pre-Calculated    |
|                      |    range/altitude    |    Radio Range       |
|                      |    Symbol Table ID   |                      |
|                      |    and Symbol Code   |    Omni DF Signal    |
|                      |                      |    Strength Storm    |
|                      |    Mic-E longitude,  |    Data (in Comment  |
|                      |    speed and course, |    field)            |
|                      |    telemetry or      |                      |
|                      |    status Raw GPS    |                      |
|                      |    NMEA sentence     |                      |
|                      |                      |                      |
|                      |    Raw weather       |                      |
|                      |    station data      |                      |
+----------------------+----------------------+----------------------+
| Direction            |    Time (DHM or HMS) |    Course and Speed  |
| Finding              |    Lat/long          |                      |
|                      |    coordinates       |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |    Compressed        |    Hei               |
|                      |    lat/lon           | ght/Gain/Directivity |
|                      | g/course/speed/radio |    Pre-Calculated    |
|                      |    range/altitude    |    Radio Range       |
|                      |    Symbol Table ID   |                      |
|                      |    and Symbol Code   |    Omni DF Signal    |
|                      |                      |    Strength          |
|                      |                      |                      |
|                      |                      |    Bearing and       |
|                      |                      |                      |
|                      |                      | Number/Range/Quality |
|                      |                      |    (in Comment       |
|                      |                      |    field)            |
+----------------------+----------------------+----------------------+
|                      |    Object name       |    Course and Speed  |
+----------------------+----------------------+----------------------+
|                      |    Item name         |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |                      |    Hei               |
|                      |                      | ght/Gain/Directivity |
+----------------------+----------------------+----------------------+
| Objects and          |    Time (DHM or HMS) |    Pre-Calculated    |
|                      |    Lat/long          |    Radio Range Omni  |
| Items                |    coordinates       |    DF Signal         |
|                      |                      |    Strength Area     |
|                      |    Compressed        |    Object            |
|                      |    lat/lon           |                      |
|                      | g/course/speed/radio |                      |
|                      |    range/altitude    |                      |
+----------------------+----------------------+----------------------+
|                      |    Symbol Table ID   |    Storm Data (in    |
|                      |    and Symbol Code   |    Comment field)    |
+----------------------+----------------------+----------------------+
|                      |    Raw weather       |                      |
|                      |    station data      |                      |
+----------------------+----------------------+----------------------+
| Weather              |    Time (MDHM)       |    Wind Direction    |
|                      |    Lat/long          |    and Speed Storm   |
|                      |    coordinates       |    Data (in Comment  |
|                      |                      |    field)            |
|                      |    Compressed        |                      |
|                      |    lat/lon           |                      |
|                      | g/course/speed/radio |                      |
|                      |    range/altitude    |                      |
|                      |    Symbol Table ID   |                      |
|                      |    and Symbol Code   |                      |
|                      |                      |                      |
|                      |    Raw weather       |                      |
|                      |    station data      |                      |
+----------------------+----------------------+----------------------+
| Telemetry            |    Telemetry (non    |                      |
|                      |    Mic-E)            |                      |
+----------------------+----------------------+----------------------+
|                      |    Addressee         |                      |
+----------------------+----------------------+----------------------+
|    Messages,         |    Message Text      |                      |
|  Bulletins and       |    Message           |                      |
|  Announcements       |    Identifier        |                      |
|                      |                      |                      |
|                      |    Message           |                      |
|                      |    Acknowledgement   |                      |
|                      |    Bulletin ID,      |                      |
|                      |    Announcement ID   |                      |
+----------------------+----------------------+----------------------+
|                      |    Group Bulletin ID |                      |
+----------------------+----------------------+----------------------+
| Queries              |    Query Type        |                      |
|                      |                      |                      |
|                      |    Query Target      |                      |
|                      |    Footprint         |                      |
|                      |    Addressee         |                      |
|                      |    (Directed Query)  |                      |
+----------------------+----------------------+----------------------+
|                      |    Position          |    Course and Speed  |
+----------------------+----------------------+----------------------+
|                      |    Object/Item       |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |                      |    Hei               |
|                      |                      | ght/Gain/Directivity |
+----------------------+----------------------+----------------------+
|                      |    Weather           |    Pre-Calculated    |
|                      |                      |    Radio Range       |
+----------------------+----------------------+----------------------+
|                      |    Status            |    Omni DF Signal    |
|                      |                      |    Strength          |
+----------------------+----------------------+----------------------+
| Responses            |    Message           |    Area Object       |
|                      |    Digipeater Trace  |                      |
|                      |                      |    Wind Direction    |
|                      |                      |    and Speed         |
+----------------------+----------------------+----------------------+
|                      |    Stations Heard    |                      |
+----------------------+----------------------+----------------------+
|                      |    Heard Statistics  |                      |
+----------------------+----------------------+----------------------+
|                      |    Station           |                      |
|                      |    Capabilities      |                      |
+----------------------+----------------------+----------------------+
| Status               |    Time (DHM zulu)   |                      |
|                      |    Status text       |                      |
|                      |                      |                      |
|                      |    Meteor Scatter    |                      |
|                      |    Beam              |                      |
|                      |    Heading/Power     |                      |
|                      |    Maidenhead        |                      |
|                      |    Locator (Grid     |                      |
|                      |    Square) Altitude  |                      |
|                      |    (Mic-E)           |                      |
|                      |                      |                      |
|                      |    E-mail message    |                      |
+----------------------+----------------------+----------------------+
| Other                |    Third-Party       |                      |
|                      |    forwarding        |                      |
|                      |    Invalid Data/Test |                      |
|                      |    Data              |                      |
+----------------------+----------------------+----------------------+


Comment Field In general, any APRS packet can contain a plain
text comment (such as a beacon message) in the Information field,
immediately following the APRS Data or APRS Data Extension.

There is no separator between the APRS data and the comment unless
otherwise stated.

The comment may contain any printable ASCII characters (except \|
and ~, which are reserved for TNC channel switching).

The maximum length of the comment field depends on the report —
details are included in the description of each report.

In special cases, the Comment field can also contain further APRS
data:

-  Altitude in comment text (see Chapter 6: Time and Position
   Formats), or in Mic-E status text (see Chapter 10: Mic-E Data
   Format).
-  Maidenhead Locator (grid square), in a Mic-E status text field
   (see Chapter 10: Mic-E Data Format) or in a Status Report (see
   Chapter 16: Status Reports).
-  Bearing and Number/Range/Quality parameters (/BRG/NRQ), in DF
   reports (see Chapter 7: APRS Data Extensions).
-  Area Object Line Widths (see Chapter 11: Object and Item
   Reports).
-  Signpost Objects (see Chapter 11: Object and Item Reports).
-  Weather and Storm Data (see Chapter 12: Weather Reports).
-  Beam Heading and Power, in Status Reports (see Chapter 16: Status
   Reports).



Base-91 Notation Two APRS data formats use base-91 notation:
lat/long coordinates in compressed format (see Chapter 9) and the
altitude in Mic-E format (see Chapter 10).

Base-91 data is compressed into a short string of characters. All the
characters are printable ASCII, with character codes in the range
33–124 decimal (i.e. ! through \|).

To compute the base-91 ASCII character string for a given data value,
the value is divided by progressively reducing powers of 91 until the
remainder is less than 91. At each step, 33 is added to the modulus
of the division process to obtain the corresponding ASCII character
code.

For example, for a data value of 12345678:

========================== ==== ===================================
   12345678 / 91\ :sup:`3`    =    modulus 16, remainder 288542
========================== ==== ===================================
   288542 / 91\ :sup:`2`      =    modulus 34, remainder 6988
   6988 / 91\ :sup:`1`        =    modulus 76, remainder 72
========================== ==== ===================================


The four ASCII character codes are thus 49 (i.e. 16\ +33), 67
(i.e. 34\ +33), 109 (i.e. 76\ +33) and 105 (i.e.
72\ +33), corresponding to the ASCII string 1Cmi.

APRS Data Units For historical reasons there is some lack of
consistency between units of data in APRS packets — some speeds are
in knots, others in miles per hour; some altitudes are in feet,
others in meters, and so on. It is emphasized that this specification
describes the units of data as they are transmitted on-air. It is the
responsibility of APRS applications to convert the on-air units to
more suitable units if required.

The default GPS earth datum is World Geodetic System (WGS) 1984.
