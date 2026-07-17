## Static ESP Testing - Phase 7

### Overview

Optimal 5 Hz vs 10 Hz



### Conclusions



### Configuration

|   ID   | Constellations              | Rate  | Max Sats |    ESP     |    Baud |
| :----: | --------------------------- | :---: | :------: | :--------: | ------: |
|   D1   | GPS + Galileo + BeiDou B1C  | 10 Hz |    28    |  160 MHz   | 115,200 |
|   D2   | GPS + Galileo + BeiDou B1C  | 10 Hz |    28    |  160 MHz   | 115,200 |
|   D3   | GPS + Galileo + BeiDou B1C  | 5 Hz  |    28    |  160 MHz   | 115,200 |
|   D5   | GPS + Galileo + BeiDou B1C  | 5 Hz  |    28    |  160 MHz   | 115,200 |
| **S3** | **GPS + Galileo + GLONASS** | 5 Hz  |    32    | **80 Mhz** |  38,400 |
|  SY1   | GPS + Galileo + BeiDou B1C  | 10 Hz |    28    |  160 MHz   |  38,400 |
|  SY2   | GPS + Galileo + BeiDou B1C  | 5 Hz  |    28    |  160 MHz   |  38,400 |

S3 was intended to be GPS + Galileo + BeiDou B1C and 160 MHz, but somehow reset itself to GPS + Galileo + GLONASS and 80 MHz.



### Results