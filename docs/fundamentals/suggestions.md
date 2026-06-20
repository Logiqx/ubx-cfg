## Suggestions

### Satellites

#### Constellations

Simple [static testing](../testing/static-5hz-10hz.md) has shown that 10 Hz can sometimes be worse than 5 Hz.

Reducing the number of constellations to allow higher logging rates can be counterproductive.

The best results will likely come from the 3 best services; GPS, Galileo and BeiDou B1C.



#### Logging Rates

It might be worth limiting users to a smaller selection; e.g. 1 / 2 / 4 / 5 / 8 / 10 / 16 Hz.

Systematic testing of various constellations and logging rates should clarify the relative performances.

Static testing is likely to be highly beneficial, prior to embarking on dynamic testing on the water.



#### Strong Candidates

The following configurations using 3 or 4 constellations are expected to produce the best performances on the M10:

|            Constellations            | Max Log Rate |   M10   |  ESP32  | Useful? |
| :----------------------------------: | :----------: | :-----: | :-----: | :-----: |
| GPS + Galileo + BeiDou B1C + GLONASS |    4 Hz ?    | 128 MHz | 80 MHz  |    ❓    |
|      GPS + Galileo + BeiDou B1C      |     5 Hz     | 128 MHz | 80 MHz  |    ✅    |
| GPS + Galileo + BeiDou B1C + GLONASS |   10 Hz ?    | 192 MHz | 160 MHz |    ❓    |
|      GPS + Galileo + BeiDou B1C      |    10 Hz     | 192 MHz | 160 MHz |    ✅    |

Notes:

- GPS+GAL+B1C+GLO logging at 4 Hz / 10 Hz is based on the u-blox claim of a minimum 98% fix rate under typical conditions.
  - It is likely that GPS+GAL+B1C+GLO can be logged at 8 Hz, without dropping frames when the M10 is at 192 MHz.

- GPS+GAL+B1C can potentially log at 8 Hz / 16 Hz, but that is based on the basis of a minimum 98% fix rate under typical conditions.
  - Propose trying 5 Hz / 10 Hz since they are the nearest divisors of 1000, and will ensure that no points are dropped.

- It has yet to be determined whether GPS+GAL+B1C+GLO has any performance benefits over GPS+GAL+B1C.
  - It might be that constellations can be pre-decided for end users - GPS+GAL+B1C @ 1 / 2 / 4 / 5 / 10 Hz.
- Changing the M10 to 192 MHz is irreversible, and it CANNOT be reverted back to 128 MHz. 




#### Weak Candidates

2 constellations are not expected to perform as well as 3 constellations at a lower logging rate, so probably not useful:

|  Constellations  | Max Log Rate |   M10   |  ESP32  | Useful? |
| :--------------: | :----------: | :-----: | :-----: | :-----: |
| GPS + BeiDou B1C |    10 Hz     | 128 MHz | 160 MHz |    ❌    |
|  GPS + Galileo   |    10 Hz     | 128 MHz | 160 MHz |    ❌    |
| GPS + BeiDou B1C |    20 Hz     | 192 MHz | 240 MHz |    ❓    |
|  GPS + Galileo   |    20 Hz     | 192 MHz | 240 MHz |    ❓    |

The weak candidates should be tested in the same way as the strong candidates, but with lower expectations!

Some other signals and logging rates have been dismissed:

- GLONASS in 2 and 3 constellation configurations
  - Galileo and BeiDou are much better systems, and typically more accurate
- BeiDou B1I in any configurations
  - Legacy system, superseded by BeiDou B1C and requires more M10 power
- Single constellation (i.e. GPS) logging at 25 Hz
  - Very likely to be worse than multiple constellations, and ESP32 needs to be 240 MHz
- Logging rates that are not a divisor of 1000, such as 15 Hz
  - Inconsistent timestamps from one second to the next are undesirable



#### TBC

What about QZSS + SBAS?

Propose ignoring them for now?



### Filters

Suggest experimenting with the following the following filters:

- Maximum number of satellites, no lower than the 24 of the Motion
- Elevation mask of 10 or 15 degrees

Propose ignoring the following filters at this time:

- C/N₀ thresholds
- Advanced filtering

Note: Reducing the number of satellites is one way to prevent points from being dropped by the M10.



### Testing

The constellations and logging rates are perhaps the most important things to establish, prior to exploring dynamic models and output filtering.

Static testing is one of the most controlled ways to test devices and is easy to perform.

Be aware that the +/- values in the software may mislead you... see previous test comparing [5 Hz and 10 Hz](../testing/static-5hz-10hz.md).
