## Static ESP Testing - Phase 4

### Overview

Satellite limits @ 5 Hz



### Conclusions



### Configuration

|  ID  | Constellations             | Rate  | Max Sats |   ESP   |    Baud |
| :--: | -------------------------- | :---: | :------: | :-----: | ------: |
| SY1  | GPS + Galileo + BeiDou B1C | 5 Hz  |    24    | 80 MHz  |  38,400 |
|  S3  | **GPS + Galileo**          | 5 Hz  |    24    | 80 MHz  |  38,400 |
|  D1  | GPS + Galileo + BeiDou B1C | 5 Hz  |    28    | 80 MHz  | 115,200 |
|  D2  | GPS + Galileo + BeiDou B1C | 5 Hz  |    28    | 80 MHz  | 115,200 |
|  D3  | GPS + Galileo + BeiDou B1C | 5 Hz  |    32    | 80 MHz  | 115,200 |
|  D5  | GPS + Galileo + BeiDou B1C | 5 Hz  |    32    | 80 MHz  | 115,200 |
| SY2  | GPS + Galileo + BeiDou B1C | 10 Hz |    32    | 160 MHz |  38,400 |

S3 was intended to be GPS + Galileo + BeiDou B1C, but somehow reset itself to GPS + Galileo.



### Charts

![phase-4-sog](img\phase-4-sog.png)



### Results

Test 4

- Similar in nature to test 3, but 5 Hz and no GLONASS
- 5 Hz GGB with various sat limits
- S3 is incorrectly configured (GPS + Galileo) and should be ignored
- Max of 28 sats is optimal, but dropping frames
  - Rankings: 28 sats, 32 sats, 24 sats
- Results suggest that 10 Hz is much worse than 5 Hz for accuracy
  - SY2 (10 Hz) mean SOG is much worse than the 5 Hz devices
- HOWEVER this was D1 and D2 which performed best in test 3
  - Test 3 showed 24 sats was best, but also D1 and D2
