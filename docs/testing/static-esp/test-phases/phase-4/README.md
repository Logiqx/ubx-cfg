## Static ESP Testing - Phase 4

### Overview

The objective of phase 4 was to determine the effects of limiting the number of satellites @ 5 Hz. The SYRAC GPS devices were all intended to use GPS + Galileo + BeiDou B1C (no GLONASS), and various satellite limits - 24, 28, and 32.

The clock rate of the ESP32 was also set to 80 MHz to see whether it would be capable of the 5 Hz rate, without dropping any frames. It was noticeable that almost all of the devices dropped frames, which inspired the 160 MHz tests for phase 5.

The tests were started on 2026-07-10 @ 2311 and the duration was over 10 hours. The results showed max sats = 28 to be optimal @ 5 Hz, and 5 Hz to be more accurate than 10 Hz. There was also a hint that D1 and D2 may have a slight performance advantage.



### Configurations

The following device configurations were tested.

|   ID    | Constellations             | Rate  | Max Sats |   ESP   | Observed time distribution (ms)                      | Drops? |
| :-----: | -------------------------- | :---: | :------: | :-----: | :--------------------------------------------------- | :----: |
|  SSY1   | GPS + Galileo + BeiDou B1C | 5 Hz  |    24    | 80 MHz  | 199: 2, 200: 184003, 201: 2, 400: 6                  |   Y    |
| **S3**  | **GPS + Galileo**          | 5 Hz  |    24    | 80 MHz  | 199: 2, 200: 94680, 201: 2                           |   -    |
|   D1    | GPS + Galileo + BeiDou B1C | 5 Hz  |    28    | 80 MHz  | 199: 13, 200: 183228, 201: 13, 400: 6                |   Y    |
|   D2    | GPS + Galileo + BeiDou B1C | 5 Hz  |    28    | 80 MHz  | 199: 5, 200: 183224, 201: 5, 400: 3                  |   Y    |
|   D3    | GPS + Galileo + BeiDou B1C | 5 Hz  |    32    | 80 MHz  | 199: 18, 200: 183737, 201: 18, 400: 5                |   Y    |
|   D5    | GPS + Galileo + BeiDou B1C | 5 Hz  |    32    | 80 MHz  | 199: 13, 200: 183253, 201: 13, 400: 8                |   Y    |
| **SY2** | GPS + Galileo + BeiDou B1C | 10 Hz |    32    | 160 MHz | 99: 18, 100: 363251, 101: 38, 199: 20, **200: 2098** |   Y    |

Notes:

- S3 was intended to be GPS + Galileo + BeiDou B1C, but it somehow switched to GPS + Galileo
- Devices using 3 systems @ 5 Hz + 80 MHz were all observed to drop frames, but SY2 dropped a LOT of frames
- SY2 @ 10 Hz + 160 MHz dropped a LOT of frames, and problems with speed and sAcc were evident in the data



### Statistics

Click the SBP filenames for charts showing SOG, Sats, HDOP, and sAcc.

| File                 | Configuration                      | Mean  | Median | Stddev |
| -------------------- | -------------------------------------------- | :---: | :----: | :----: |
| [D2\_\_2607112346.sbp](png/D2__2607112346.png)  | GPS + Galileo + BeiDou, 28 sats @ 5 Hz   | 0.021 | 0.019      | 0.014              |
| [D1\_2607112346.sbp](png/D1_2607112346.png)   | GPS + Galileo + BeiDou, 28 sats @ 5 Hz   | 0.021 | 0.019      | 0.014              |
| [D5\_2607112346.sbp](png/D5_2607112346.png)   | GPS + Galileo + BeiDou, 32 sats @ 5 Hz   | 0.023 | 0.019      | 0.015              |
| [D3\_\_2607112345.sbp](png/D3__2607112345.png) | GPS + Galileo + BeiDou, 32 sats @ 5 Hz   | 0.024 | 0.019      | 0.015              |
| [SY1\_\_2607112345.sbp](png/SY1__2607112345.png) | GPS + Galileo + BeiDou, 24 sats @ 5 Hz  | 0.025 | 0.019      | 0.015              |
| [S3\_\_2607120443.sbp](png/S3__2607120443.png)  | **GPS + Galileo, 24 sats @ 5 Hz**        | 0.026 | 0.019      | 0.016              |
| [SY2\_2607112345.sbp](png/SY2_2607112345.png)  | GPS + Galileo + BeiDou, 32 sats @ 10 Hz | 0.045 | 0.039      | 0.025              |

28 satellites @ 5 Hz (green) performed best and 32 satellites @ 10 Hz (orange) performed worst.

![sog-mean.png](img/sog-mean.png)

5 Hz consistently outperformed 10 Hz from the perspective of median values.

![sog-median.png](img/sog-median.png)

5 Hz consistently outperformed 10 Hz from the perspective of standard deviation.

![sog-stddev.png](img/sog-stddev.png)



### Observations

- S3 was intended to be GPS + Galileo + BeiDou B1C
  - Somehow it was switched to GPS + Galileo
- SY2 dropped lots of frames, and saw quite a few "mini spikes"
  - Perhaps due to the M10 using "balanced" [power mode](../../../../performance/signal-quality.md)
- 28 satellites performed best @ 5 Hz
  - 32 sats was next best, and 24 sats slightly worse than 32
- D1 and D2 produced the most accurate results during phase 3
  - D1 and D2 produced the most accurate results during phase 2



### Conclusions

- Max of 28 sats provides the best accuracy, but drops frames @ 80 MHz
  - Order of accuracy @ 5 Hz is 28 sats, 32 sats, 24 sats
- The cause of dropped frames at 5 Hz may be the ESP32 @ 80 MHz
  - Earlier tests coped with higher rates without dropping frames
- Results suggest the accuracy of 10 Hz is significantly worse than 5 Hz
  - The accuracy of SY2 @ 10 Hz was much worse than 5 Hz devices
- D1 and D2 may perform better than the S devices
  - Phase 5 testing will ensure they use different configurations
