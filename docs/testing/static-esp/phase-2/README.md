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

S3 was intended to be GPS + Galileo + BeiDou B1C @ 10 Hz, but was configured as GPS + Galileo.



### Results
