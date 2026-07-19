## Static ESP Testing - Phase 3

### Overview

Satellite limits @ 15 Hz



### Conclusions



### Configuration

|   ID   | Constellations             | Rate  | Max Sats |   ESP   |    Baud |
| :----: | -------------------------- | :---: | :------: | :-----: | ------: |
|   D3   | GPS + Galileo + GLONASS    | 15 Hz |    28    | 240 MHz | 115,200 |
|   D5   | GPS + Galileo + BeiDou B1C | 15 Hz |    28    | 240 MHz | 115,200 |
|   D1   | GPS + Galileo + GLONASS    | 15 Hz |    24    | 240 MHz | 115,200 |
|   D2   | GPS + Galileo + BeiDou B1C | 15 Hz |    24    | 240 MHz | 115,200 |
|  SY1   | GPS + Galileo + GLONASS    | 15 Hz |    20    | 240 MHz |  38,400 |
| **S3** | **GPS + Galileo**          | 15 Hz |    20    | 240 MHz |  38,400 |
|  SY2   | GPS + Galileo + GLONASS    | 10 Hz |    32    | 160 MHz |  38,400 |

S3 was intended to be GPS + Galileo + BeiDou B1C, but somehow reset itself to GPS + Galileo.



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
