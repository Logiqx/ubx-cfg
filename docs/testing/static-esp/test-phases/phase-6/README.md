## Static ESP Testing - Phase 6

### Overview

Satellite limits @ 10 Hz

2026-07-13 @ 1348



### Configurations

The following device configurations were tested.

|  ID  | Constellations             | Rate  | Max Sats |   ESP   | Observed time distribution (ms)               | Drops? |
| :--: | -------------------------- | :---: | :------: | :-----: | :-------------------------------------------- | :----: |
| SY1  | GPS + Galileo + BeiDou B1C | 10 Hz |    24    | 160 MHz | 99: 1, 100: 190916, 101: 1                    |   -    |
|  S3  | **GPS + Galileo**          | 10 Hz |    24    | 160 MHz | 99: 6, 100: 191198, 101: 6                    |   -    |
|  D1  | GPS + Galileo + BeiDou B1C | 10 Hz |    28    | 160 MHz | 99: 8, 100: 191205, 101: 8                    |   -    |
|  D2  | GPS + Galileo + BeiDou B1C | 10 Hz |    24    | 160 MHz | 99: 5, 100: 191132, 101: 5                    |   -    |
|  D3  | GPS + Galileo + BeiDou B1C | 10 Hz |    28    | 160 MHz | 99: 11, 100: 191851, 101: 11                  |   -    |
|  D5  | GPS + Galileo + BeiDou B1C | 10 Hz |    20    | 160 MHz | 99: 8, 100: 191009, 101: 8                    |   -    |
| SY2  | GPS + Galileo + BeiDou B1C | 10 Hz |    20    | 160 MHz | 99: 19, 100: 190978, 101: 22, 199: 3, 200: 32 |   Y    |

Notes:

- S3 was intended to be GPS + Galileo + BeiDou B1C, but somehow reset itself to GPS + Galileo
- SY2 is problematic



### Statistics

The following statistics were produced by a Python script, although it needed to use an SBP file instead of GPY.

| File                  | Description                     | Mean  | Median | Stddev |
| --------------------- | ------------------------------- | :---: | :----: | :----: |
| D3\_\_2607131348.sbp  | GPS + Galileo + BeiDou, 28 sats @ 10 Hz  | 0.043 | 0.039      | 0.024              |
| D1\_2607131349.sbp   | GPS + Galileo + BeiDou, 28 sats @ 10 Hz  | 0.044 | 0.039      | 0.024              |
| S3\_\_2607131349.sbp  | **GPS + Galileo, 24 sats @ 10 Hz**       | 0.045 | 0.039      | 0.025              |
| D2\_\_2607131349.sbp  | GPS + Galileo + BeiDou, 24 sats @ 10 Hz  | 0.045 | 0.039      | 0.025              |
| D5\_2607131349.sbp   | GPS + Galileo + BeiDou, 20 sats @ 10 Hz  | 0.047 | 0.039      | 0.025              |
| SY1\_\_2607131350.sbp | GPS + Galileo + BeiDou, 24 sats @ 10 Hz | 0.049 | 0.039      | 0.027              |
| SY2\_2607131349.sbp  | GPS + Galileo + BeiDou, 20 sats @ 10 Hz | 0.050 | 0.039      | 0.027              |



### Charts

BLAH

![sog-mean.png](img/sog-mean.png)

BLAH

![sog-median.png](img/sog-median.png)

BLAH

![sog-stddev.png](img/sog-stddev.png)



### Results

Test 6 - 10 Hz tests

- S3 on wrong config
- SY2 could not handle GGB with 20 sats at 10 Hz
  - There is perhaps something wrong with the device
- Python stats are crucial and give different answer to distance alone
  - D3 and D1 best with 28 sats

Findings

1. Only SY2 dropped frames, but based on previous tests I can see it has often been struggling
2. The other 6 devices did not drop frames
3. just like 5 Hz, 28 sats was best