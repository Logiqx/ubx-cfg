## Static ESP Testing - Phase 1

### Overview

The objective of phase 1 was to determine the relative performances of GLONASS and Galileo. The SYRAC GPS devices were configured to use GPS + GLONASS or GPS + Galileo, and various sample rates - 10 Hz, 15 Hz, 20 Hz.

The tests were started on 2026-07-09 @ 0003 and the duration was more than 9 hours. The results showed that GPS + Galileo outperformed GPS + GLONASS, regardless of the sample rate.



### Configurations

The following device configurations were tested, and the time distributions obtained from GPS Speedreader.

|  ID  | Constellations          | Rate  | Max Sats |   ESP   | Observed time distribution (ms)       | Drops? |
| :--: | ----------------------- | :---: | :------: | :-----: | :------------------------------------ | :----: |
| SY1  | GPS + GLONASS           | 10 Hz |    32    | 160 MHz | 99: 3, 100: 336950, 101: 3            |   -    |
| SY2  | GPS + Galileo           | 10 Hz |    32    | 160 MHz | 99: 34, 100: 336334, 101: 34          |   -    |
|  D3  | GPS + GLONASS           | 15 Hz |    32    | 240 MHz | 65: 1, 66: 2280, 67: 498181, 68: 2282 |   -    |
|  D1  | GPS + Galileo           | 15 Hz |    32    | 240 MHz | 65: 1, 66: 2264, 67: 497605, 68: 2266 |   -    |
|  D5  | GPS + GLONASS           | 20 Hz |    32    | 240 MHz | 50: 672969, 51: 11, 99: 11            |   Y    |
|  D2  | GPS + Galileo           | 20 Hz |    32    | 240 MHz | 50: 673429, 51: 4, 99: 4              |   Y    |
|  S3  | GPS + Galileo + GLONASS | 10 Hz |    32    | 160 MHz | 99: 4, 100: 336891, 101: 4            |        |

Notes:

- The 20 Hz devices (D5 and D2) both dropped frames during this test, but not in huge numbers
- Various time intervals were observed, due to the way the M10 handles clock drift



### Statistics

Click the SBP filenames for charts showing SOG, Sats, HDOP, and sAcc.

| File               | Description                  | Mean | Median | Stddev |
| ------------------- | ---------------------------------- | :---: | :----: | :----: |
| [SY2_2607090003.sbp](png/SY2_2607090003.png) | GPS + Galileo @ 10 Hz          | 0.043 | 0.039  | 0.024  |
| [S3\_\_2607090003.sbp](png/S3__2607090003.png) | GPS + Galileo + GLONASS @ 10 Hz | 0.045 | 0.041  | 0.024  |
| [D1\_2607090003.sbp](png/D1_2607090003.png) | GPS + Galileo @ 15 Hz           | 0.051 | 0.049  | 0.028  |
| [SY1\_\_2607090003.sbp](png/SY1__2607090003.png) | GPS + GLONASS @ 10 Hz          | 0.054 | 0.051  | 0.029  |
| [D2\_\_2607090003.sbp](png/D2__2607090003.png) | GPS + Galileo @ 20 Hz           | 0.057 | 0.052  | 0.031  |
| [D3\_\_2607090003.sbp](png/D3__2607090003.png) | GPS + GLONASS @ 15 Hz           | 0.060 | 0.056  | 0.032  |
| [D5\_2607090004.sbp](png/D5_2607090004.png) | GPS + GLONASS @ 20 Hz           | 0.064 | 0.060  | 0.034  |

GPS + Galileo (green) clearly outperformed GPS + GLONASS (orange) @ 10 Hz.

![sog-mean-1.png](img/sog-mean-1.png)

GPS + Galileo (green) clearly outperformed GPS + GLONASS (orange) @ 15 Hz.

![sog-mean-2.png](img/sog-mean-2.png)

GPS + Galileo (green) clearly outperformed GPS + GLONASS (orange) @ 20 Hz.

![sog-mean-3.png](img/sog-mean-3.png)

The same was also evident in the median values for SOG.

![sog-median.png](img/sog-median.png)

The performances from the perspective of standard deviation were ordered in much the same way as the mean values.

![sog-stddev.png](img/sog-stddev.png)



### Observations

- Time To First Fix (TTFF) was quite variable, and some devices needed quite some time
  - Warm up periods are significant, so analysis excludes the first 30 mins and last 5 mins
- 10 Hz was slightly more accurate than 15 Hz, and 15 Hz was slightly more accurate than 20 Hz
  - Dropped frames were observed @ 20 Hz... slightly more for GLONASS (11) vs Galileo (4)
- No evidence of M10 "balanced" [power mode](../../../../performance/signal-quality.md) issues in SOG



### Conclusions

- GPS + Galileo outperforms GPS + GLONASS... certainly at this latitude
  - 10 Hz
    - GPS + Galileo = 0.043 kt
    - GPS + GLONASS = 0.054 kt
  - 15 Hz
    - GPS + Galileo = 0.051 kt
    - GPS + GLONASS = 0.060 kt
  - 20 Hz
    - GPS + Galileo = 0.057 kt
    - GPS + GLONASS = 0.063 kt
- Additional satellites improve HDOP, but no huge gains beyond 24 satellites
