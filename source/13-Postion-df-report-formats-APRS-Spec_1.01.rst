
POSITION AND DF REPORT DATA FORMATS
===================================

**Position Reports** Lat/Long Position Reports are contained in the
Information field of an APRS AX.25 frame.

The following diagrams show the permissible formats of these reports,
together with some examples. The gray areas indicate optional fields,
and the shaded (yellow) characters are literal ASCII characters. In
all cases there is a maximum of 43 characters after the Symbol Code.

Bytes:

Bytes:

Bytes:

Bytes:

Bytes:

Bytes:

Bytes:

**DF Reports** DF Reports are contained in the Information field of
an APRS AX.25 frame. The Bearing and Number/Range/Quality (BRG/NRQ)
parameters follow the Data Extension field.

**Note**: The BRG/NRQ parameters are only meaningful when the report
contains the DF symbol (i.e. the Symbol Table ID is **/** and the
Symbol Code is **\\**).

**Note**: If the DF station is fixed, the Course value is zero. If
the station is moving, the Course value is non-zero.

Bytes:

COMPRESSED POSITION REPORT DATA FORMATS
=======================================

In compressed data format, the Information field contains the
station’s latitude and longitude, together with course and speed or
pre-calculated radio range or altitude.

This information is compressed to minimize the length of the
transmitted packet (and therefore improve its chances of being
received correctly under less than ideal conditions).

The Information field also contains a display Symbol Code, and there
may optionally be a plain text comment (uncompressed) as well.

**The Advantages of Data Compression**

Compressed data format may be used in place of the numeric lat/long
coordinates already described, such as in the **!**, **/**, **@** and
**=** formats.

Data compression has several important benefits:

- Fully backwards compatible with all existing formats.
- Fully supports any comment string.
- Speed is accurate to +/-1 mph up to about 40 mph and within 3% at
   600 mph.
- Altitude in feet is accurate to +/- 0.4% from 1 foot to 3000 miles.
- Consistent one-algorithm processing of compressed latitude and
   longitude.
- Improved position to 1 foot worldwide.
- Pre-calculated radio range, compressed to one byte.
- Potential 50% compression of every position format on the air.
- Potential 40% reduction of raw GPS NMEA data length.
- Additional 7-byte reduction for NEMA GGA altitudes.
- Support for TNC compression at the NMEA source (from the GPS
   receiver).
- Digipeater compression of old NMEA trackers on the fly.
- Usage is optional in all cases.



The only minor disadvantages are that the course only resolves to +/-
2 degrees, and this format does not support PHG.

**Compressed Data**

**Format**

Bytes:

Compressed data may be generated in several ways:

- by APRS software.
- pre-entered manually into a digipeater’s beacon text.
- by a digipeater converting raw tracker NMEA packets to compressed.
.

[In future, there is the possibility that a Kantronics KPC-3 or other
tracker TNC will be able to compress data directly from an attached
GPS receiver].

In all cases the compressed format is a fixed 13-character field:

/YYYYXXXX$csT

where / is the Symbol Table Identifier YYYY is the compressed
latitude XXXX is the compressed longitude

$ is the Symbol Code

cs is the compressed course/speed or compressed pre-calculated radio
range or compressed altitude

T is the compression type indicator

+----------+----------+----------+----------+----------+----------+
|    **Co  |          |          |          |          |          |
| mpressed |          |          |          |          |          |
|          |          |          |          |          |          |
| Position |          |          |          |          |          |
|          |          |          |          |          |          |
|   Data** |          |          |          |          |          |
+==========+==========+==========+==========+==========+==========+
|    **Sym |    **Co  |    **Co  |          |    **Co  |          |
|    Table | mpressed | mpressed | **Symbol | mpressed |   **Comp |
|    ID**  |    Lat** |          |          |          |          |
|          |    YYYY  |   Long** |   Code** |   Course |   Type** |
|          |          |    XXXX  |          | /Speed** |    T     |
+----------+----------+----------+----------+----------+----------+
|          |          |          |          |    **Co  |          |
|          |          |          |          | mpressed |          |
|          |          |          |          |    Radio |          |
|          |          |          |          |          |          |
|          |          |          |          |  Range** |          |
+----------+----------+----------+----------+----------+----------+
|          |          |          |          |    **Co  |          |
|          |          |          |          | mpressed |          |
|          |          |          |          |    Al    |          |
|          |          |          |          | titude** |          |
+----------+----------+----------+----------+----------+----------+
|    1     |    4     |    4     |    1     |    2     |    1     |
+----------+----------+----------+----------+----------+----------+


Compressed format can be used in place of lat/long position format
anywhere that …ddmm.hhN/dddmm.hhW$xxxxxxx… occurs.

All bytes except for the **/** and **$** are base-91 printable ASCII
characters (**!**..\ **{**). These are converted to numeric values by
subtracting 33 from the decimal ASCII character code. For example,
**#** has an ASCII code of 35, and represents a numeric value of 2
(i.e. 35-33).

**Symbol** The presence of the leading Symbol Table Identifier
instead of a digit indicates that this is a compressed Position
Report and not a normal lat/long report.

**Lat/Long Encoding** The values of YYYY and XXXX are computed as
follows:

YYYY is 380926 x (90 – latitude) [base 91]

latitude is positive for north, negative for south, in degrees.

XXXX is 190463 x (180 + longitude) [base 91]

longitude is positive for east, negative for west, in degrees.

For example, for a longitude of 72° 45' 00" west (i.e. -72.75
degrees), the math is 190463 x (180 – 72.75) = 20427156. Because this
is to base 91, it is then necessary to progressively divide this
value by reducing powers of 91, to obtain the numerical values of X:

20427156 / 91\ :sup:`3` = **27**, remainder 80739

80739 / 91\ :sup:`2` = **9**, remainder 6210

6210 / 91\ :sup:`1` = **68**, remainder **22**

To obtain the corresponding ASCII characters, 33 is added to each of
these values, yielding 60 (i.e. 27+33), 42, 101 and 55. From the
ASCII Code Table (in Appendix 3), this corresponds to **<*e7** for
XXXX.

**Lat/Long Decoding** To decode a compressed lat/long, the reverse
process is needed. That is, if

YYYY is represented as
y\ :sub:`1`\ y\ :sub:`2`\ y\ :sub:`3`\ y\ :sub:`4` and XXXX as
x\ :sub:`1`\ x\ :sub:`2`\ x\ :sub:`3`\ x\ :sub:`4`, then:

Lat = 90 - ((y\ :sub:`1`-33) x 91\ :sup:`3` + (y\ :sub:`2`-33) x
91\ :sup:`2` + (y\ :sub:`3`-33) x 91 + y\ :sub:`4`-33) / 380926

Long = -180 + ((x\ :sub:`1`-33) x 91\ :sup:`3` + (x\ :sub:`2`-33) x
91\ :sup:`2` + (x\ :sub:`3`-33) x 91 + x\ :sub:`4`-33) / 190463

For example, if the compressed value of the longitude is **<*e7** (as
computed above), the calculation becomes:

Long = -180 + (27 x 91\ :sup:`3` + 9 x 91\ :sup:`2` + 68 x 91 + 22) /
190463

= -180 + (20346417 + 74529 + 6188 + 22) / 190463

= -180 + 107.25

= -72.75 degrees

**Course/Speed, Pre-Calculated Radio Range and**

**Altitude**

The two cs bytes following the Symbol Code character can contain
either the compressed course and speed or the compressed
pre-calculated radio range or the station’s altitude. These two bytes
are in base 91 format.

In the special case of c = **␣** (space), there is no course, speed
or range data, in which case the csT bytes are ignored.

**Course/Speed** — If the ASCII code for c is in the range **!** to
**z** inclusive — corresponding to numeric values in the range 0–89
decimal (i.e. after subtracting 33 from the ASCII code) — then cs
represents a compressed course/speed value:

course = **c** x 4

speed = 1.08\ **s** – 1

For example, if the cs characters are **7P**, the corresponding
values of **c** and **s** (after subtracting 33 from the ASCII
character code) are 22 and 47 respectively. Substituting these values
in the above equations:

course = **22** x 4 = 88 degrees

speed = 1.08\ **47** – 1 = 36.2 knots

**Pre-Calculated Radio Range** — If c = **{**, then cs represents a
compressed pre-calculated radio range value:

range = 2 x 1.08\ **s**

For example, if the cs bytes are **{?**, the ASCII code for **?** is
63, so the value of **s** is 30 (i.e. 63-33). Thus:

range = 2 x 1.08\ **30**

~ 20 miles

So APRS will draw a circle of radius 20 miles around the station plot
on the screen.

**The Compression Type (T) Byte**

Bit:

Value:

The T byte follows the cs bytes. The T byte contains several bit
fields showing the GPS fix status, the NMEA source of the position
data and the origin of the compression.

The T byte is not meaningful if the c byte is **␣** (space).

+--------+--------+--------+--------+--------+------+---+---+
|    *   |        |        |        |        |      |   |   |
| *Compr |        |        |        |        |      |   |   |
| ession |        |        |        |        |      |   |   |
|        |        |        |        |        |      |   |   |
|   Type |        |        |        |        |      |   |   |
|    (T) |        |        |        |        |      |   |   |
|        |        |        |        |        |      |   |   |
|   Byte |        |        |        |        |      |   |   |
|    Fo  |        |        |        |        |      |   |   |
| rmat** |        |        |        |        |      |   |   |
+========+========+========+========+========+======+===+===+
|    7   |    6   |    5   |    4   |    3   |    2 | 1 | 0 |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    *   |      |   |   |
|   *Not |   *Not |  **GPS | **NMEA | *Compr |      |   |   |
|        |        |        |    So  | ession |      |   |   |
|  used* |  used* |  Fix** | urce** |    Or  |      |   |   |
|        |        |        |        | igin** |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|    0   |    0   |    0 = |    0 0 |    0 0 |      |   |   |
|        |        |    old |    =   |    0 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        | (last) |  other |   Comp |      |   |   |
|        |        |        |        | ressed |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |    1 = |    0 1 |    0 0 |      |   |   |
|        |        |    c   |    =   |    1 = |      |   |   |
|        |        | urrent |    GLL |    TNC |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  BText |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |    1 0 |    0 1 |      |   |   |
|        |        |        |    =   |    0 = |      |   |   |
|        |        |        |    GGA |    So  |      |   |   |
|        |        |        |        | ftware |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  (DOS/ |      |   |   |
|        |        |        |        | Mac/Wi |      |   |   |
|        |        |        |        | n/+SA) |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |    1 1 |    0 1 |      |   |   |
|        |        |        |    =   |    1 = |      |   |   |
|        |        |        |    RMC |        |      |   |   |
|        |        |        |        |  [tbd] |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 0 |      |   |   |
|        |        |        |        |    0 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   KPC3 |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 0 |      |   |   |
|        |        |        |        |    1 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   Pico |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 1 |      |   |   |
|        |        |        |        |    0 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  Other |      |   |   |
|        |        |        |        |    t   |      |   |   |
|        |        |        |        | racker |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  [tbd] |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 1 |      |   |   |
|        |        |        |        |    1 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   Digi |      |   |   |
|        |        |        |        | peater |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   conv |      |   |   |
|        |        |        |        | ersion |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+

..

For example, if the compressed position was derived from an RMC
sentence, the fix is current, and the compression was performed by
APRSdos software, then the value of T in binary is 0 0 1 11 010,
which equates to 58 decimal.

Adding 33 to this value gives the ASCII code for the T byte (i.e.
91), which

corresponds to the **[** character.

Thus, using data from all the earlier examples, if the RMC sentence
contains (among other parameters) the following data:

Latitude = 49° 30' 00" north

Longitude = 72° 45' 00" west Speed = 36.2 knots

Course = 88°

and: the fix is current

compression is performed by APRSdos software the display symbol is a
“car”

then the complete 13-character compressed location field is
transmitted as:

===== ======== ======== ======== ==========
/     YYYY     XXXX        $        csT
===== ======== ======== ======== ==========
**/** **5L!!** **<*e7**    **>**    **7P[**
===== ======== ======== ======== ==========



**Altitude** If the T byte indicates that the raw data originates
from a GGA sentence (i.e. bits 4 and 3 of the T byte are 10), then
the sentence contains an altitude value, in feet. After compression,
the compressed altitude data is placed in the cs bytes, such that:

altitude = 1.002\ **cs** feet

For example, if the received cs bytes are **S]**, the computation is
as follows:

-  Subtract 33 from the ASCII code for each character:



**c** = 83 – 33 = 50

**s** = 93 – 33 = 60

-  Multiply **c** by 91 and add **s** to obtain **cs**: **cs** = 50 x 91
+ 60



= 4610

-  Then altitude = 1.002\ **4610**

= 10004 feet

**New Trackers** Tracker firmware may compress GPS data directly to
APRS compressed format. They would use the **!** Data Type Indicator,
showing that the position is real-time and that the tracker is not
APRS-capable.

If the Position Report is not real-time, then the **/** Data Type
Indicator can be used instead, so that the latest fix time may be
included.

**Old Trackers** Some digipeaters have the ability to convert raw
NMEA strings from existing trackers to compressed data format for
further forwarding.

These digipeaters will compress the data if the tracker Destination
Address is

GPS. (**Note**: This is the 3-letter address GPS, not GPS*).

Trackers desiring for their packets to not be modified by the APRS
network will use any other valid generic APRS Destination Address.

**Compressed Report**

**Formats**

Compressed data is contained in the AX.25 Information field, in these
formats:

Bytes:

Bytes:
