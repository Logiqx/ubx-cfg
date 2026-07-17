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



### Results
