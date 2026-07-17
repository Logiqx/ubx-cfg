## Static ESP Testing - Phase 6

### Overview

Satellite limits @ 10 Hz



### Conclusions



### Configuration

|  ID  | Constellations             | Rate  | Max Sats |   ESP   |    Baud |
| :--: | -------------------------- | :---: | :------: | :-----: | ------: |
| SY1  | GPS + Galileo + BeiDou B1C | 10 Hz |    24    | 160 MHz |  38,400 |
|  S3  | **GPS + Galileo**          | 10 Hz |    24    | 160 MHz |  38,400 |
|  D1  | GPS + Galileo + BeiDou B1C | 10 Hz |    28    | 160 MHz | 115,200 |
|  D2  | GPS + Galileo + BeiDou B1C | 10 Hz |    24    | 160 MHz | 115,200 |
|  D3  | GPS + Galileo + BeiDou B1C | 10 Hz |    28    | 160 MHz | 115,200 |
|  D5  | GPS + Galileo + BeiDou B1C | 10 Hz |    20    | 160 MHz | 115,200 |
| SY2  | GPS + Galileo + BeiDou B1C | 10 Hz |    20    | 160 MHz |  38,400 |

S3 was intended to be GPS + Galileo + BeiDou B1C, but somehow reset itself to GPS + Galileo.



### Results