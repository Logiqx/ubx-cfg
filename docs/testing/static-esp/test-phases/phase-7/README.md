## Static ESP Testing - Phase 7

### Overview

The objective of phase 7 was to compare the optimal 5 Hz and 10 Hz configurations. The SYRAC GPS devices were all intended to use GPS + Galileo + BeiDou B1C (no GLONASS), and a maximum of 28 satellites.

The tests were started on 2026-07-14 @ 0031 and the duration was just under 10  hours. The results showed that 5 Hz is far more accurate than 10 Hz, which is consistent with phase 4, 5, and 6. Speed Accuracy (sAcc) can also be quite misleading.



### Configurations

The following device configurations were tested.

|   ID   | Constellations              | Rate  | Max Sats |    ESP     | Observed time distribution (ms)         | Drops? |
| :----: | --------------------------- | :---: | :------: | :--------: | :-------------------------------------- | :----: |
|   D1   | GPS + Galileo + BeiDou B1C  | 10 Hz |    28    |  160 MHz   | 99: 11, 100: 338258, 101: 11            |   -    |
|   D2   | GPS + Galileo + BeiDou B1C  | 10 Hz |    28    |  160 MHz   | 99: 5, 100: 352086, 101: 5              |   -    |
|   D3   | GPS + Galileo + BeiDou B1C  | 5 Hz  |    28    |  160 MHz   | 199: 18, 200: 176100, 201: 18           |   -    |
|   D5   | GPS + Galileo + BeiDou B1C  | 5 Hz  |    28    |  160 MHz   | 199: 12, 200: 176461, 201: 12           |   -    |
| **S3** | **GPS + Galileo + GLONASS** | 5 Hz  |  **32**  | **80 Mhz** | 199: 4, 200: 176099, **201: 4, 400: 8** |   Y    |
|  SY1   | GPS + Galileo + BeiDou B1C  | 10 Hz |    28    |  160 MHz   | 99: 3, 100: 351202, 101: 3              |   -    |
|  SY2   | GPS + Galileo + BeiDou B1C  | 5 Hz  |    28    |  160 MHz   | 199: 36, 200: 175999, 201: 36           |   -    |

Notes:

- S3 was intended to be GPS + Galileo + BeiDou B1C @ 160 MHz, but somehow reset itself to GPS + Galileo + GLONASS @ 80 MHz
- S3 was the only device to drop any frames, presumably because the ESP32 was running @ 80 MHz



### Statistics

Click the SBP filenames for charts showing SOG, Sats, HDOP, and sAcc.

| File                  | Description                             | Mean  | Median | Stddev |
| --------------------- | --------------------------------------- | :---: | :----: | :----: |
| [SY2\_2607140033.sbp](png/SY2_2607140033.png)    | GPS + Galileo + BeiDou, 28 sats @ 5 Hz     | 0.024 | 0.021  | 0.013  |
| [D5\_2607140031.sbp](png/D5_2607140031.png)     | GPS + Galileo + BeiDou, 28 sats @ 5 Hz      | 0.024 | 0.021  | 0.014  |
| [ubxGPS\_2607140032.sbp](png/ubxGPS_2607140032.png) | **GPS + Galileo + GLONASS, 32 sats @ 5 Hz** | 0.024 | 0.021  | 0.014  |
| [D3\_\_2607140033.sbp](png/D3__2607140033.png)    | GPS + Galileo + BeiDou, 28 sats @ 5 Hz      | 0.024 | 0.021  | 0.013  |
| [D1\_2607140032.sbp](png/D1_2607140032.png)     | GPS + Galileo + BeiDou, 28 sats @ 10 Hz     | 0.042 | 0.039  | 0.022  |
| [D2\_\_2607140033.sbp](png/D2__2607140033.png)    | GPS + Galileo + BeiDou, 28 sats @ 10 Hz     | 0.042 | 0.039  | 0.023  |
| [SY1\_2607140034.sbp](png/SY1__2607140034.png)   | GPS + Galileo + BeiDou, 28 sats @ 10 Hz    | 0.047 | 0.045  | 0.025  |



#### Speed Over Ground (SOG)

The 5 Hz devices all performed significantly better than the 10 Hz devices.

![sog-mean.png](img/sog-mean.png)

The same was also evident in the median values for SOG.

![sog-median.png](img/sog-median.png)

The performances from the perspective of standard deviation were similar to the mean values.

![sog-stddev.png](img/sog-stddev.png)



#### Speed Accuracy (sAcc)

The mean "speed accuracy" at 5 Hz is reported as being WORSE than 10 Hz.

![sacc-mean.png](img/sacc-mean.png)

The median "speed accuracy" at 5 Hz is reported as being WORSE than 10 Hz.

![sacc-median.png](img/sacc-median.png)

The standard deviation for "speed accuracy" at 5 Hz is also WORSE than 10 Hz.

![sacc-stddev.png](img/sacc-stddev.png)

Since we know that the true Speed Over Ground (SOG) we can be sure that the Speed Accuracy (sAcc) is misleading during these tests.



### Observations

- S3 (ubxGPS) was intended to be GPS + Galileo + BeiDou B1C
  - Somehow it was switched to GPS + Galileo
- S3 (ubxGPS) was also the only device to drop any frames
  - Presumably caused by the ESP32 running @ 80 MHz
- SY2 dropped saw a few "mini spikes", similar to previous tests
  - Perhaps due to the M10 using "balanced" [power mode](../../../../performance/signal-quality.md)
- Performance of all 5 Hz devices comparable
  - SY1 not as good as D1 and D2 @ 10 Hz, maybe baud rate?
- 5 Hz accuracy is significantly better than 10 Hz
  - There is no obvious advantage to 10 Hz for speed sailing
- sAcc is very misleading
  - It says that 10 Hz is most accurate, which is NOT correct



### Conclusions

- 5 Hz is significantly more accurate than 10 Hz
  - Phase 7 results are consistent with phases 4, 5, and 6
- Speed Accuracy (sAcc) cannot be taken literally
  - 5 Hz was better than 10 Hz, but sAcc said the opposite!

