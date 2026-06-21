## Suggestions

### Satellites

#### Constellations

Simple [static testing](../testing/static-5hz-10hz.md) has shown that 10 Hz can sometimes be worse than 5 Hz.

It showed that reducing the number of constellations for higher logging rates can be counterproductive.

The best results may well come from 3 systems logging at 10 Hz; e.g. GPS, Galileo and BeiDou B1C.



#### Logging Rates

Systematic testing of various constellations and logging rates should help to clarify the relative performances.

Static testing is likely to provide early performance insights, prior to embarking on dynamic testing on the water.

It may become apparent that a smaller choice of logging rates is desirable, such as 1 / 2 / 4 / 5 / 8 / 10 Hz.



#### Strong Candidates

The following configurations using 3 or 4 constellations are expected to produce the best performances on the M10:

|            Constellations            | Max Log Rate  |   M10   |  ESP32  | Useful? |
| :----------------------------------: | :-----------: | :-----: | :-----: | :-----: |
| GPS + Galileo + BeiDou B1C + GLONASS |    4 Hz ?     | 128 MHz | 80 MHz  |    ❓    |
|      GPS + Galileo + BeiDou B1C      |  5 or 8 Hz ?  | 128 MHz | 80 MHz  |    ✅    |
| GPS + Galileo + BeiDou B1C + GLONASS | 8 or 10 Hz ?  | 192 MHz | 160 MHz |    ❓    |
|      GPS + Galileo + BeiDou B1C      | 10 or 16 Hz ? | 192 MHz | 160 MHz |    ✅    |

Notes:

- GPS+GAL+B1C+GLO logging at 4 Hz / 10 Hz is based on the u-blox claim of a minimum 98% fix rate under typical conditions.
  - It is likely that GPS+GAL+B1C+GLO can be logged at 8 Hz, without dropping frames when the M10 is at 192 MHz.

- GPS+GAL+B1C can potentially log at 8 Hz / 16 Hz, but that is based on the basis of a minimum 98% fix rate under typical conditions.
  - Propose trying 5 Hz / 10 Hz since they are the nearest divisors of 1000, and will ensure that no points are dropped.

- It has yet to be determined whether GPS+GAL+B1C+GLO has any performance benefits over GPS+GAL+B1C.
  - It may transpire that GPS + Galileo + BeiDou B1C is the most suitable for all end users, thus avoiding the need for choice.
  




#### Weak Candidates

The following configurations using 2 constellations are not expected to perform as well as the strong candidates:

|  Constellations  | Max Log Rate |   M10   |  ESP32  | Useful? |
| :--------------: | :----------: | :-----: | :-----: | :-----: |
| GPS + BeiDou B1C |   10 Hz ?    | 128 MHz | 160 MHz |    ❌    |
|  GPS + Galileo   |   10 Hz ?    | 128 MHz | 160 MHz |    ❌    |
| GPS + BeiDou B1C |   20 Hz ?    | 192 MHz | 240 MHz |    ❓    |
|  GPS + Galileo   |   20 Hz ?    | 192 MHz | 240 MHz |    ❓    |

The weak candidates should be tested in the same way as the strong candidates, but with lower expectations!

A variety of other signals and logging rates have also been dismissed:

- GLONASS in the 2 or 3 constellation configurations
  - Galileo and BeiDou are much better systems, and should be more accurate
- BeiDou B1I in any configurations
  - Legacy system, superseded by BeiDou B1C and requires more power on the M10
- Single constellations, like GPS alone logging at 25 Hz
  - Very likely to be worse than multiple constellations, and the ESP32 needs to be 240 MHz
- Logging rates that are not a divisor of 1000, such as 3, 6, or 15 Hz
  - Inconsistent timestamps from one second to the next are undesirable



#### Augmentation Systems

What about SBAS and QZSS?

- SBAS can potentially improve positional accuracy, but should not be used as additional satellites.
  - Need to check if it is possible for the M10 to just use SBAS for the ranging corrections.
- QZSS may be useful in the Pacific region, covering Japan and Australia
  - Use the online [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951) to determine where there QZO (orbiting) satellites are visible.

SBAS and QZSS certainly warrant investigation, but they are not a top priority.



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
