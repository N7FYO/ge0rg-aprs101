PREAMBLE
========

**APRS Working**

**Group**

The APRS Working Group is an unincorporated association whose members
undertake to further the use and enhance the value of the APRS
protocols by

a. publishing and maintaining a formal APRS Protocol Specification;
b. publishing validation tests and other tools to enable compliance
with the Specification;
c. supporting an APRS Certification program; and
d. generally working to improve the capabilities of APRS within the
amateur radio community.

..

Although the Working Group may receive support from TAPR and other
organizations, it is an independent body and is not affiliated with
any organization. The Group has no budget, collects no dues, and owns
no assets.

The current members of the APRS Working Group are:

John Ackermann, N8UR Administrative Chair & TAPR Representative Bob
Bruninga, WB4APR Technical Chair, founder of APRS

Brent Hildebrand, KH2Z Author of APRS+SA Stan Horzepa, WA1LOU
Secretary

Mike Musick, N0QBF Author of pocketAPRS

Keith Sproul, WU2Z Co-Author of WinAPRS/MacAPRS/X-APRS Mark Sproul,
KB2ICI Co-Author of WinAPRS/MacAPRS/X-APRS

**Acknowledgements** This document is the result of contributions
from many people. It includes much of the material produced by
individual members of the Working Group.

In addition, the paper on the Mic-E data format by Alan Crosswell,
N2YGK, and Ron Parsons, W5RKN was a useful starting point for
explaining the complications of this format.

**Document Version Number**

Except for the very first public draft release of the APRS Protocol
Reference, the document version number is a 3-part number “P.p.D”
(for an approved document release) or a 4-part number “P.p.Dd” (for a
draft release):

============================== ======================= ============ ====
**Document Version Number**                                      
============================== ======================= ============ ====
**APRS Protocol Version**      **Document Release**    **Draft** 
**Major Release**              **Minor Release**                 
P.                             p.                      D            d
============================== ======================= ============ ====

..

Thus, for example:

-  Document version number “1.2.3” refers to document release 3 covering
APRS Protocol Version 1.2.

-  Document version number “1.2.3c” is draft “c” of that document.

..

**Release History** The release history for this document is listed
in Appendix 7.

**Document Conventions**

This document uses the following conventions:

-  Courier font ASCII characters in APRS data.

-  ␣ ASCII space character.

-  … (ellipsis) zero or more characters.

-  /$ Symbol from Primary Symbol Table.

-  \\$ Symbol from Alternate Symbol Table.

-  0x hexadecimal (e.g. 0x1d).

-  All callsigns are assumed to have SSID –0 unless otherwise specified.

-  **Yellow marker** (appears as light gray background in hard copy).
Marks text of interest — especially useful for highlighting single
literal ASCII characters (e.g. **"**) where they appear in APRS
data.

-  Shaded areas in packet format diagrams are optional fields.

..

**Feedback** Please address your feedback or other comments regarding
this document to the TAPR *aprsspec* mail list.

To join the list, start at
`http://www.tapr.org <http://www.tapr.org/>`__ and then follow the
path Special Interest Groups  APRS Specification  Join APRS Spec
Discussion List.
