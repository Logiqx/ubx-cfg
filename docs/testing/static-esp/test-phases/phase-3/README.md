## Static ESP Testing - Phase 3

### Overview

Satellite limits @ 15 Hz

2026-07-10 @ 2311



### Configurations

The following device configurations were tested.

|   ID    | Constellations             | Rate  | Max Sats |   ESP   | Observed time distribution (ms)                              | Drops? |
| :-----: | -------------------------- | :---: | :------: | :-----: | :----------------------------------------------------------- | :----: |
|   D3    | GPS + Galileo + GLONASS    | 15 Hz |    28    | 240 MHz | 65: 1, 66: 2844, 67: 623883, 68: 2855, 133: 9                |   Y    |
|   D5    | GPS + Galileo + BeiDou B1C | 15 Hz |    28    | 240 MHz | 66: 2838, 67: 623969, 68: 2842, 133: 4                       |   Y    |
|   D1    | GPS + Galileo + GLONASS    | 15 Hz |    24    | 240 MHz | 65: 1, 66: 2845, 67: 623816, 68: 2854, 132: 1, 133: 5        |   Y    |
|   D2    | GPS + Galileo + BeiDou B1C | 15 Hz |    24    | 240 MHz | 66: 2288, 67: 502609, 68: 2290, 133: 2                       |   Y    |
|   SY1   | GPS + Galileo + GLONASS    | 15 Hz |    20    | 240 MHz | 66: 2806, 67: 623919, 68: 2806                               |   -    |
| **S3**  | **GPS + Galileo**          | 15 Hz |    20    | 240 MHz | 66: 2835, 67: 623912, 68: 2835                               |   -    |
| **SY2** | GPS + Galileo + GLONASS    | 10 Hz |    32    | 160 MHz | 99: 21, 100: 417730, 101: 43, **199: 23, 200: 1987, 201: 1** |   Y    |

Notes:

- S3 was intended to be GPS + Galileo + BeiDou B1C, but it somehow switched to GPS + Galileo
- Many of the devices dropped some frames, but SY2 dropped a LOT of frames



### Charts

The Python charts are best viewed in new tabs... hold the ctrl key when left-clicking the links.

- [D1\_2607102311](png/D1_2607102311.png)
- [D2\_\_2607102312](png/D2__2607102312.png)
- [D3\_\_2607102311](png/D3__2607102311.png)
- [D5\_2607102311](png/D5_2607102311.png)
- [S3\_\_2607102311](png/S3__2607102311.png)
- [SY1\_\_2607102311](png/SY1__2607102311.png)
- [SY2\_2607102311](png/SY2_2607102311.png)



### Statistics

The following statistics were produced by a Python script, although it needed to use an SBP file instead of GPY.

| File                 | Description                                  | Mean  | Median | Stddev |
| -------------------- | ----------------------------------- | :---: | :----: | :----: |
| SY2\_2607102311.sbp  | GPS + Galileo + GLONASS, 32 sats @ 10 Hz | 0.045 | 0.039      | 0.025              |
| D2\_\_2607102312.sbp  | GPS + Galileo + BeiDou, 24 sats @ 15 Hz   | 0.050 | 0.039      | 0.027              |
| S3\_\_2607102311.sbp  | **GPS + Galileo, 20 sats @ 15 Hz**        | 0.051 | 0.039      | 0.028              |
| D5\_2607102311.sbp   | GPS + Galileo + BeiDou, 28 sats @ 15 Hz   | 0.052 | 0.039      | 0.029              |
| D1\_2607102311.sbp   | GPS + Galileo + GLONASS, 24 sats @ 15 Hz  | 0.053 | 0.058      | 0.029              |
| SY1\_\_2607102311.sbp | GPS + Galileo + GLONASS, 20 sats @ 15 Hz | 0.054 | 0.058      | 0.029              |
| D3\_\_2607102311.sbp  | GPS + Galileo + GLONASS, 28 sats @ 15 Hz  | 0.056 | 0.058      | 0.031              |

BLAH

![sog-mean-1.png](img/sog-mean-1.png)

BLAH

![sog-mean-2.png](img/sog-mean-2.png)

BLAH

![sog-median.png](img/sog-median.png)

BLAH

![sog-stddev.png](img/sog-stddev.png)



### Results

Test 3

- 38,400 seemed to cope with 15 Hz
  - SY1
- B1C is clearly better than GLONASS
  - Evident when max sats set at 28 and 24
  - Sadly no data for 20 sats due to incorrect configuration on S3
- Sat limit can prevent dropped frames
  - Does not appear to reduce accuracy...
  - 28 is actually the least accurate
  - 24 is most accurate, but drops frames
  - 20 appears to avoid dropped frames, but accuracy slightly worse than 24
- SY2 is still not working correctly
  - Perhaps dropping frames due to the default limit of 32 sats
