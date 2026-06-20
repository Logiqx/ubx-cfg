## Suggestions

### Constellations

Use least 3

https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951 - mask angle 10 degrees

Consider QZSS + SBAS



### Rates

It might be worth limiting users to a smaller selection.

e.g. 1, 2, 5, and 10 Hz.

Static test - HDOP better at 5 Hz

Suggest systematic test *
Less systems = worse HDOP, translate into worse hAcc and sAcc

I do not like 15 Hz
C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Organised\ESP-GPS\Salvador, SYRAC-GPS\2026-04-26, SYRAC-GPS, 15 Hz



### Combinations

#### Potential Candidates

The following configurations using 3 or 4 constellations are expected to produce the best performances on the M10:

| Constellations  | Max Log Rate |   M10   |  ESP32  | Useful? |
| :-------------: | :----------: | :-----: | :-----: | :-----: |
| GPS+GAL+B1C+GLO |    4 Hz ?    | 128 MHz | 80 MHz  |    ❓    |
|   GPS+GAL+B1C   |     5 Hz     | 128 MHz | 80 MHz  |    ✅    |
| GPS+GAL+B1C+GLO |   10 Hz ?    | 192 MHz | 160 MHz |    ❓    |
|   GPS+GAL+B1C   |    10 Hz     | 192 MHz | 160 MHz |    ✅    |

Notes:

- GPS+GAL+B1C+GLO logging at 4 Hz / 10 Hz is based on the u-blox claim of a minimum 98% fix rate under typical conditions.
  - It is very likely that GPS+GAL+B1C+GLO can be logged at 8 Hz without dropping frames when the M10 is at 192 MHz.

- GPS+GAL+B1C can potentially log at 8 Hz / 16 Hz, but that is based on the basis of a minimum 98% fix rate under typical conditions.
  - Propose logging at 5 Hz / 10 Hz since they are the nearest divisors of 1000, and will ensure that points are not dropped.

- It has yet to be determined whether GPS+GAL+B1C+GLO has any performance benefits over GPS+GAL+B1C.
  - It might be that only two configurations need to be available to end users - GPS+GAL+B1C @ 5 Hz or 10 Hz.




#### Unlikely to be Useful

2 constellations are not expected to perform as well as 3 constellations, so probably not useful:

| Constellations | Max Log Rate |   M10   |  ESP32  | Useful? |
| :------------: | :----------: | :-----: | :-----: | :-----: |
|    GPS+B1C     |    10 Hz     | 128 MHz | 160 MHz |    -    |
|    GPS+GAL     |    10 Hz     | 128 MHz | 160 MHz |    -    |
|    GPS+B1C     |    20 Hz     | 192 MHz | 240 MHz |    -    |
|    GPS+GAL     |    20 Hz     | 192 MHz | 240 MHz |    -    |

IMPORTANT: Changing the M10 to 192 MHz is irreversible, and it CANNOT be changed back to 128 MHz. 



#### Dismissed

- Single constellation configurations logging at 20 Hz or 25 Hz
  - The fix quality is likely to be much worse than multiple constellations
- GLONASS in 2 and 3 constellation configurations
  - Galileo and BeiDou are much better systems, and usually more accurate
- BeiDou B1I in any configurations
  - Legacy system, superseded by BeiDou B1C and more intensive for the M10
- Logging rates that are not a divisor of 1000, such as 15 Hz
  - Inconsistent timestamps from one second to the next are undesirable



### Filters

Suggest experimenting with the following:

- Maximum number of satellites, no lower than the 24 of the Motion
- Elevation mask of 10 or 15 degrees

Not enough known about the following:

- C/N₀ thresholds
- Advanced filtering



