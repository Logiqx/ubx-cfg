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



### Charts

BLAH

![sog-mean.png](img/sog-mean.png)

BLAH

![sog-median.png](img/sog-median.png)

BLAH

![sog-stddev.png](img/sog-stddev.png)

BLAH

![sacc-mean.png](img/sacc-mean.png)

BLAH

![sacc-median.png](img/sacc-median.png)

BLAH

![sacc-stddev.png](img/sacc-stddev.png)



### Results

Test 7

puts equally performing devices up against each other (e.g. D1 and D3) but 5 Hz vs 10 Hz

I have taken into consideration that S3 may use GGB (hopefully it will), and knowing that SY2 could not handle 10 Hz, put it on 5 Hz

Results

- 5 Hz significantly better than 10 Hz
  - There is no advantage to 10 Hz
- sAcc is misleading
  - It says that 10 Hz is performing better
- Performance of all 5 Hz devices comparable
  - SY1 performed less well than D1 and D2 @ 10 Hz, maybe baud rate?