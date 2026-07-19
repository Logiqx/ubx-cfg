## Static ESP Testing - Phase 2

### Overview

GLONASS vs BeiDou

2026-07-09 @ 1314



### Configurations

The following device configurations were tested.

|   ID    | Constellations             | Rate  | Max Sats |   ESP   | Observed time distribution (ms)                      | Drops? |
| :-----: | -------------------------- | :---: | :------: | :-----: | :--------------------------------------------------- | :----: |
|   SY1   | GPS + Galileo              | 10 Hz |    32    | 160 MHz | 99: 2, 100: 273003, 101: 2, 200: 1                   |   Y    |
| **SY2** | GPS + Galileo + GLONASS    | 10 Hz |    32    | 160 MHz | 99: 19, 100: 270042, 101: 31, **199: 12, 200: 1406** |   Y    |
| **S3**  | **GPS + Galileo**          | 10 Hz |    32    | 160 MHz | 99: 7, 100: 272833, 101: 7                           |   -    |
|   D3    | GPS + Galileo              | 15 Hz |    32    | 240 MHz | 65: 1, 66: 1850, 67: 403800, 68: 1852                |   -    |
|   D1    | GPS + Galileo + GLONASS    | 15 Hz |    32    | 240 MHz | 66: 1869, 67: 410428, 68: 1875, 133: 6               |   Y    |
|   D5    | GPS + Galileo + BeiDou B1C | 15 Hz |    32    | 240 MHz | 65: 1, 66: 1864, 67: 410030, 68: 1870, 133: 4        |   Y    |
|   D2    | GPS + Galileo              | 20 Hz |    32    | 240 MHz | 50: 554566, 51: 8, 99: 8                             |   Y    |

Notes:

- SY2 dropped a lot of frames during this test, and the Python charts show clear issues with speed + sAcc
- S3 was intended to be GPS + Galileo + BeiDou B1C @ 10 Hz, but it somehow switched to GPS + Galileo



### Statistics

The following statistics were produced by a Python script, although it needed to use an SBP file instead of GPY.

| File                 | Description                         | Mean  | Median | Stddev |
| -------------------- | ---------------------------------- | :---: | :----: | :----: |
| S3\_\_2607091314.sbp  | GPS + Galileo @ 10 Hz            | 0.044 | 0.039      | 0.025              |
| SY2\_2607091314.sbp  | GPS + Galileo + GLONASS @ 10 Hz | 0.047 | 0.039      | 0.032              |
| SY1\_\_2607091314.sbp | GPS + Galileo @ 10 Hz           | 0.047 | 0.039      | 0.026              |
| D5\_2607091307.sbp   | GPS + Galileo + BeiDou @ 15 Hz   | 0.053 | 0.058      | 0.029              |
| D3\_\_2607091314.sbp  | GPS + Galileo @ 15 Hz            | 0.054 | 0.058      | 0.030              |
| D1\_2607091307.sbp   | GPS + Galileo + GLONASS @ 15 Hz  | 0.054 | 0.058      | 0.029              |
| D2\_\_2607091307.sbp  | GPS + Galileo @ 20 Hz            | 0.058 | 0.058      | 0.031              |



### Charts

BLAH

![sog-mean-1.png](img/sog-mean-1.png)

BLAH

![sog-mean-2.png](img/sog-mean-2.png)

BLAH

![sog-median.png](img/sog-median.png)

BLAH

![sog-stddev.png](img/sog-stddev.png)



### Results

Test 2

- S3 was incorrectly configured
  - Shame because we cannot compare the 10 Hz configurations
  - Will have to rely on phase 3 for GLONASS vs B1C
- SY2 (GPS + GAL + B1C) dropped lots of frames and saw quite a few mini spikes
  - Perhaps due to "balanced" power mode?
  - Maybe the clock is drifting quickly as well?
- Practically no difference between 15 Hz and 20 Hz
  - Arguably, 10 Hz was better
- Overall GLONASS performed worst, Galileo performed best
  - GPS + Galileo > GPS + Galileo + GLONASS @ 10 Hz
  - GPS + Galileo + BeiDou B1C > GPS + Galileo + GLONASS > GPS + Galileo @ 15 Hz
  - GPS + Galileo > GPS + GLONASS @ 20 Hz
