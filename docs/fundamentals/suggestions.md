## Suggestions

### Satellites

#### Constellations

Simple [static testing](../testing/static-5hz-10hz.md) has shown that 10 Hz can sometimes be worse than 5 Hz.

It showed that reducing the number of constellations to achieve higher logging rates can be counterproductive.

Optimal configurations may prove to be something like 3 systems logging at 10 Hz; e.g. GPS, Galileo and BeiDou B1C.



#### Logging Rates

Systematic testing of various constellations and logging rates should help to confirm the relative performances.

Static testing is likely to provide quick performance insights, prior to embarking on dynamic testing on the water.

It may become transpire that a short list logging rates is optimal; e.g. 1 / 2 / 4 / 5 / 8 / 10 Hz.



#### Strongest Candidates

The following configurations with 3 or 4 constellations have the potential to produce the best M10 performances.

M10 CPU @ 128 MHz, ESP-32 MCU @ 80 MHz:

|            Constellations            | Max Sats |  Log Rate   |
| :----------------------------------- | :------: | :---------: |
|      GPS + Galileo + BeiDou B1C      |    ?     | 5 or 8 Hz ? |
|       GPS + Galileo + GLONASS        |    ?     | 5 or 6 Hz ? |
| GPS + Galileo + BeiDou B1C + GLONASS |    ?     |   4 Hz ?    |

M10 CPU @ 192 MHz, ESP-32 MCU @ 160 MHz:

|            Constellations            | Max Sats |   Log Rate    |
| :----------------------------------- | :------: | :-----------: |
|      GPS + Galileo + BeiDou B1C      |    ?     | 10 or 16 Hz ? |
|       GPS + Galileo + GLONASS        |    ?     | 10 or 16 Hz ? |
| GPS + Galileo + BeiDou B1C + GLONASS |    ?     | 8 or 10 Hz ?  |

Notes:

- Upper bounds for log rate are based on minimum 98% fix rate under typical conditions.
- Lower bounds for log rate use positive divisors of 1000, and less likely to see dropped frames.
- Limiting the number of satellites is another way to reduce the likelihood of dropped frames.
- GPS + Galileo + BeiDou B1C may be suitable for all end users, thus avoiding confusing choices.



#### Weakest Candidates

The following configurations using 2 constellations are not expected to perform as well as 3 constellations.

M10 CPU @ 128 MHz, ESP-32 MCU @ 160 MHz:

|  Constellations  | Max Sats | Log Rate |
| :--------------- | :------: | :------: |
|  GPS + Galileo   |    ?     | 10 Hz ?  |
| GPS + BeiDou B1C |    ?     | 10 Hz ?  |
|  GPS + GLONASS   |    ?     | 10 Hz ?  |

M10 CPU @ 192 MHz, ESP-32 MCU @ 240 MHz:

|  Constellations  | Max Sats | Log Rate |
| :--------------- | :------: | :------: |
|  GPS + Galileo   |    ?     | 20 Hz ?  |
| GPS + BeiDou B1C |    ?     | 20 Hz ?  |
|  GPS + GLONASS   |    ?     | 20 Hz ?  |

The weak candidates should be tested in the same way as the strong candidates, but with lower expectations!

A variety of other configurations have been dismissed:

- BeiDou B1I in any configurations.
  - Legacy system, superseded by BeiDou B1C and requires more power on the M10.
- Single constellations logging at 25 Hz - e.g. GPS only.
  - Likely to be worse than multiple constellations, and the ESP32 needs to be 240 MHz.
- Logging rates that are multiples of 3, and thus not divisors of 1000; e.g. 3, 6, and 15 Hz.
  - Inconsistent timestamps from one second to the next can be undesirable.



#### Augmentation Systems

What about SBAS and QZSS?

- SBAS may improve positional accuracy, but must not be used as additional satellites.
  - Ensure SBAS differential corrections are enabled
    - `CFG-SBAS-USE_DIFFCORR = 1`
  - Ensure SBAS is not used for ranging
    - `CFG-SBAS-USE_RANGING = 0`
- QZSS may be useful in the Pacific region, especially Japan and Australia.
  - Use [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951) to determine where the QZSS QZO (orbiting) satellites are visible.

SBAS and QZSS certainly warrant some investigation, but perhaps not a top priority.



### Filters

Suggest experimenting with the following the following filters:

- Maximum number of satellites, but no lower than the 24 of the Motion
- Elevation mask of 10° or 15°

Propose ignoring the following filters at this time:

- C/N₀ thresholds
- Advanced filtering

Note: Restricting the number of satellites is one way to prevent frames from being dropped by the M10.



### Testing

Choosing the right constellations, satellite limits, and logging rates is a crucial decision.

Static testing provides a controlled environment to test devices systematically, and is very easy to perform.

The approach for testing these crucial fundamentals is described on another [page](../testing/fundamentals.md).
