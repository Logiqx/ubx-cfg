## Static ESP Testing - GPY vs SBP

### Overview

GPY is superior to SBP, partly due to minimal file sizes.

- Averages just over 20 bytes per record for GPY, instead of 32 for SBP

Increased precision of GPY.
- SOG and sAcc are 3 decimals, instead of 2 decimals in SBP
  - sAcc is not limited to 2.55 m/s (4.96 kt) like SBP
- HDOP is 2 decimals, instead of 1 decimal in SBP
  - GPY is not restricted to increments of 0.2 like SBP



### Losses

SBP contains some fields that are not in GPY, but they are no biggie.
- Altitude (MSL)
  - The increased precision of other fields makes up for this loss
- Space Vehicle IDs - flags indicating the 32 GPS satellites in use
  - They are nice in GPS-only receivers, but fairly redundant in multi-GNSS
- Climb Rate (Vertical Speed) + Vertical Speed DOP (VSDOP)
  - The increased precision of other fields makes up for this loss



### Headers

- SBP header contains log rate, which is not in GPY header.
  - User Name : MAX CHAR(13)
  - Serial Number : MAX CHAR(8)
  - Log Rate : MAX CHAR 3, 0..255 in seconds
  - Firmware Version  :  MAX CHAR (14) , V1.62(B0820T)
- GPY header has longer fields.
  - uint16_t DeviceType=2;//ublox = 2
  - char deviceDescription[16]="ESP-GPS";
  - char deviceName[16]= "Boom";
  - char serialNumber[16]="macAddr";
  - char firmwareVersion[16]="SW_version";



### Proposal

This testing has made the strengths of GPY very clear, but it would be benefit from some minor enhancements.

A proposal for these enhancements can be found on a page inside the GPS Wizard repository - [GPY 1.1](https://logiqx.github.io/gps-wizard/ideas/gpy/)
