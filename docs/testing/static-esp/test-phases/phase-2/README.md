## Static ESP Testing - Phase 2

### Overview

GLONASS vs BeiDou



### Conclusions



### Configuration

|   ID   | Constellations             | Rate  | Max Sats |   ESP   |    Baud |
| :----: | -------------------------- | :---: | :------: | :-----: | ------: |
|  SY1   | GPS + Galileo              | 10 Hz |    32    | 160 MHz |  38,400 |
|  SY2   | GPS + Galileo + GLONASS    | 10 Hz |    32    | 160 MHz |  38,400 |
| **S3** | **GPS + Galileo**          | 10 Hz |    32    | 160 MHz |  38,400 |
|   D3   | GPS + Galileo              | 15 Hz |    32    | 240 MHz | 115,200 |
|   D1   | GPS + Galileo + GLONASS    | 15 Hz |    32    | 240 MHz | 115,200 |
|   D5   | GPS + Galileo + BeiDou B1C | 15 Hz |    32    | 240 MHz | 115,200 |
|   D2   | GPS + Galileo              | 20 Hz |    32    | 240 MHz | 115,200 |

S3 was intended to be GPS + Galileo + BeiDou B1C @ 10 Hz, but somehow reset itself to GPS + Galileo.



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
