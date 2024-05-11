APRS DATA EXTENSIONS
====================

A fixed-length 7-byte field may follow APRS position data. This field
is an APRS Data Extension. The extension may be one of the following:

- CSE\ **/**\ SPD Course and Speed (this may be followed by a further
  8 bytes containing DF bearing and Number/Range/Quality parameters)
- DIR\ **/**\ SPD Wind Direction and Wind Speed
- **PHG**\ phgd Station Power and Effective Antenna Height/Gain/
  Directivity
- **RNG**\ rrrr Pre-Calculated Radio Range
- **DFS**\ shgd DF Signal Strength and Effective Antenna Height/Gain
- Tyy/Cxx Area Object Descriptor


**Course and Speed** The 7-byte CSE\ **/**\ SPD Data Extension can be
used to represent the course and speed of a vehicle or APRS Object.

The course is expressed in degrees (001-360), clockwise from due
north. The speed is expressed in knots. A slash **/** character
separates the two.

For example:

088/036 represents a course 88 degrees, traveling at 36 knots.

If the course and speed are unknown or not relevant, they can be set
to

**000/000** or **.../...** or **␣␣␣/␣␣␣**.

**Note**: In the special case of DF reports, a course of 000 means
that the DF station is fixed. If the course is non-zero, the station
is mobile.

**Wind Direction and Wind Speed**

The 7-byte DIR\ **/**\ SPD Data Extension can be used to represent
the wind direction and sustained one-minute wind speed in a Weather
Report.

The wind direction is expressed in degrees (001-360), clockwise from
due north. The speed is expressed in knots. A slash **/** character
separates the two.

For example:

220/004 represents a wind direction of 220 degrees and a speed of 4
knots.

If the wind direction and speed are unknown or not relevant, they can
be set to **000/000** or **.../...** or **␣␣␣/␣␣␣**.

**Power, Effective Antenna**

**Height/Gain/ Directivity**

PHG Codes
---------

The 7-byte **PHG**\ phgd Data Extension specifies the transmitter
power, effective antenna height-above-average-terrain, antenna gain
and antenna directivity. APRS uses this information to plot radio
range circles around stations.

The 7 characters of this Data Extension are encoded as follows:
Characters 1–3: **PHG** (fixed)

Character 4: p Power code Character 5: h Height code Character 6: g
Antenna gain code Character 7: d Directivity code

The PHG codes are listed in the table below:

+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| phgd  |       |       |       |       |       |       |       |       |       |       |       |
| **Co  | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** |  **Un |
| de:** |       |       |       |       |       |       |       |       |       |       | its** |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| Power |    0  |    1  |    4  |    9  |    16 |    25 |    36 |    49 |    64 |    81 |       |
|       |       |       |       |       |       |       |       |       |       |       | watts |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| H     |    10 |    20 |    40 |    80 |       |       |       |       |       |       |       |
| eight |       |       |       |       |   160 |   320 |   640 |  1280 |  2560 |  5120 |  feet |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Gain  |    0  |    1  |    2  |    3  |    4  |    5  |    6  |    7  |    8  |    9  |    dB |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| D     |       |    45 |    90 |       |       |       |       |       |       |       |       |
| irect |  omni |       |       |   135 |   180 |   225 |   270 |   315 |   360 |       |   deg |
| ivity |       |    NE |    E  |       |       |       |       |       |       |       |       |
|       |       |       |       |    SE |    S  |    SW |    W  |    NW |    N  |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+



The height code represents the effective height of the antenna *above
average local terrain*, not above ground or sea level — this is to
provide a rough indication of the antenna’s effectiveness in the
local area .

The height code may in fact be any ASCII character 0–9 and above.
This is so that larger heights for balloons, aircraft or satellites
may be specified.

For example:

**:** is the height code for 10240 feet (approximately 1.9 miles).

**;** is the height code for 20480 feet (approximately 3.9 miles),
and so on.

The Directivity code offsets the PHG circle by one third in the
indicated direction. This means a front-to-back ratio of 2 to 1. Most
often this is used to indicate a favored direction or a null, even if
an omni antenna is at the site.

An example of the PHG Data Extension:

PHG5132 means a power of 25 watts,

an antenna height of 20 feet above the average local terrain, an
antenna gain of 3 dB,

and maximum gain due east.

**Range Circle Plot** On receipt, APRS uses the **p**, **h**, **g**
and **d** codes to calculate the usable radio range (in miles), for
plotting a range circle representing the local radio horizon around
the station. The radio range is calculated as follows:

power = **p**\ 2

Height-above-average-terrain (haat) = 10 x 2\ **h**

gain = 10(**g**/10)

range = –( 2 x haat x –( (power/10) x (gain/2) ) ) Thus, for PHG5132:

power = **5**\ 2 = 25 watts

haat = 10 x 2\ **1** = 20 feet

gain = 10(**3**/10) = 1.995262

range = –( 2 x 20 x –( (25/10) x (1.995262/2) ) )

~ 7.9 miles

As the direction of maximum gain is due east, APRS will draw a range
circle of radius 8 miles around the station, offset by 2.7 miles
(i.e. one third of 8 miles) in an easterly direction.

**Note**: In the absence of any PHG data, stations are assumed to be
running 10 watts to a 3dB omni antenna at 20 feet, resulting in a
6-mile radius range circle, centered on the station.

**Pre-Calculated Radio Range**

The 7-byte **RNG**\ rrrr Data Extension allows users to transmit a
pre- calculated omni-directional radio range, where rrrr is the range
in miles (with leading zeros).

For example, RNG0050 indicates a radio range of 50 miles. APRS can
use this value to plot a range circle around the station.

**Omni-DF Signal**

**Strength**

The 7-byte **DFS**\ shgd Data Extension lets APRS localize jammers by
plotting the overlapping signal strength contours of all stations
hearing the signal.

This Omni-DF format replaces the PHG format to indicate DF signal
strength, in that the transmitter power field is replaced with the
relative signal strength (s) from 0 to 9.

DFS Codes
---------

+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| shgd  |       |       |       |       |       |       |       |       |       |       |       |
| **Co  | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** |  **Un |
| de:** |       |       |       |       |       |       |       |       |       |       | its** |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| Str   |    0  |    1  |    2  |    3  |    4  |    5  |    6  |    7  |    8  |    9  |       |
| ength |       |       |       |       |       |       |       |       |       |       |   S-p |
|       |       |       |       |       |       |       |       |       |       |       | oints |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| H     |    10 |    20 |    40 |    80 |       |       |       |       |       |       |       |
| eight |       |       |       |       |   160 |   320 |   640 |  1280 |  2560 |  5120 |  feet |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Gain  |    0  |    1  |    2  |    3  |    4  |    5  |    6  |    7  |    8  |    9  |    dB |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| D     |       |    45 |    90 |       |       |       |       |       |       |       |       |
| irect |  omni |       |       |   135 |   180 |   225 |   270 |   315 |   360 |       |   deg |
| ivity |       |    NE |    E  |       |       |       |       |       |       |       |       |
|       |       |       |       |    SE |    S  |    SW |    W  |    NW |    N  |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+



For example, DFS2360 represents a weak signal (around strength S2)
heard on an omni antenna with 6 dB gain at 80 feet.

A signal strength of zero (0) is particularly significant, because
APRS uses these 0 signal reports to draw (usually black) circles
where the jammer is *not* heard. These black circles are extremely
valuable since there will be a lot more reports from stations that do
not hear the jammer than from those that do. This quickly eliminates
a lot of territory.

**Bearing and Number/Range/**

**Quality**

DF reports contain an 8-byte field **/**\ BRG\ **/**\ NRQ that
follows the CSE\ **/**\ SPD Data Extension, specifying the course,
speed, bearing and NRQ (Number/Range/ Quality) value of the report.
NRQ indicates the Number of hits, the approximate Range and the
Quality of the report.

For example, in:

…088/036/270/729… course = 88 degrees, speed = 36 knots,

bearing = 270 degrees, N = 7, R = 2, Q = 9

If N is 0, then the NRQ value is meaningless. Values of N from 1 to 8
give an indication of the number of hits per period relative to the
length of the time period — thus a value of 8 means 100% of all
samples possible got a hit. A value of 9 for N indicates to other
users that the report is manual.

The N value is not processed, but is just another indicator from the
automatic DF units.

The range limits the length of the line to the original map’s scale
of the sending station. The range is 2R so, for R=4, the range will
be 16 miles.

Q is a single digit in the range 0–9, and provides an indication of
bearing accuracy:

If the course and speed parameters are not appropriate, they should
have the value **000/000** or **.../...** or **␣␣␣/␣␣␣**.

**Area Object Descriptor**

The 7-byte Tyy/Cxx Data Extension is an Area Object Descriptor. The T

parameter specifies the type of object (square, circle, triangle,
etc) and the

/C parameter specifies its fill color.

Area Objects are described in Chapter 11: Object and Item Reports.
