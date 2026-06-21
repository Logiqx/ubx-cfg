## Constellation Testing

Constellations and logging rates are fundamentals, prior to exploring dynamic models and output filtering.

Static testing provides a controlled environment to test devices systematically, and is very easy to perform.

Be aware that the +/- values in the software may mislead you... see [earlier test](../testing/static-5hz-10hz.md) comparing 5 Hz and 10 Hz.



### Approach to Testing

#### Standard Configuration

Hardware

- M10 clocked at 192 MHz - high performance
- Baud rate of 115,200
- ESP32 clocked according to the logging rate

M10

- Logging rate of 5 Hz
- Default satellite limit of 32
- Default elevation mask of 5°
- Default C/N₀ criteria



#### Data Analysis

- Acquisition times
  - Time taken to acquire all of the signals
- Cumulative results in GPS Speedreader
  - Speed - 1 hour averages
  - Total distance - derived from speed data
- Percentiles from individual values - 50, 68, 95, 99.7
  - Speed over Ground (SOG)
  - sAcc
  - HDOP
- Dropped points
  - Exceeded the CPU bandwidth?




### Phase 1

Compare each of the following configurations, recording data for a minimum of 2 hours:

| Test | Device 1         | Device 2         |
| :--: | ---------------- | ---------------- |
| 1.1  | GPS + Galileo    | GPS + GLONASS    |
| 1.2  | GPS + Galileo    | GPS + BeiDou B1I |
| 1.3  | GPS + GLONASS    | GPS + BeiDou B1I |
| 1.4  | GPS + GLONASS    | GPS + BeiDou B1C |
| 1.5  | GPS + Galileo    | GPS + BeiDou B1C |
| 1.6  | GPS + BeiDou B1I | GPS + BeiDou B1C |

The tests have been ordered such that only one device needs to be reconfigured, prior to the next test.

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 12 hours



#### Expectations

Interim results are possible whilst later tests are still underway.

- After the first 3 tests we should know the best 2 out of Galileo, GLONASS, and BeiDou B1I.
- After the first 5 tests we should know the best 2 out of Galileo, GLONASS, and BeiDou B1C.
- The final test will establish which is the best out of BeiDou B1I and BeiDou B1C.

I suspect that GLONASS will have the least favourable results, put it needs some actual proof.



### Phase 2

Test the effect of limiting the number of satellites, recording data for a minimum of 2 hours:

| Test | Unit 1                     | Unit 2        | Max Sats |
| :--: | -------------------------- | ------------- | :------: |
| 2.1  | GPS + Galileo + BeiDou B1C | GPS + Galileo |    12    |
| 2.2  | GPS + Galileo + BeiDou B1C | GPS + Galileo |    16    |
| 2.3  | GPS + Galileo + BeiDou B1C | GPS + Galileo |    20    |
| 2.4  | GPS + Galileo + BeiDou B1C | GPS + Galileo |    24    |
| 2.5  | GPS + Galileo + BeiDou B1C | GPS + Galileo |    28    |
| 2.6  | GPS + Galileo + BeiDou B1C | GPS + Galileo |    32    |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 12 hours



#### Expectations

Hopefully it will become clear how the number of satellites impacts the accuracy of results.

This is important because increasing the logging rate will necessitate a reduction in the number of satellites.



### Phase 3

Investigate the maximum possible logging rates, recording data for a minimum of 2 hours:

| Test | Unit 1                     | Unit 2        | Rate  |
| :--: | -------------------------- | ------------- | :---: |
| 3.1  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 4 Hz  |
| 3.2  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 5 Hz  |
| 3.3  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 8 Hz  |
| 3.4  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 10 Hz |
| 3.5  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 16 Hz |
| 3.6  | GPS + BeiDou B1C           | GPS + Galileo | 20 Hz |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 12 hours

Notes:

- 16 Hz is not a divisor of 1000, it still closely related to 4 Hz and 8 Hz.
- The ESP32 will need to be clocked accordingly
  - 80 MHz for 8 Hz
  - 160 MHz to 16 Hz
  - 240 MHz for 20 Hz



#### Expectations

20 Hz logging will be impossible with 3 constellations, but these tests should establish the practical limit.



### Phase 4

The final phase will aim to find the perfect balance between number of satellites and logging rate.

The precise planning of this phase can be done after interpreting the results from phases 2 and 3.



#### Expectations

Suspect that accuracy of results from 2 constellations at 20 Hz may not exceed 3 constellations at 10 Hz.

It is not yet known whether 3 constellations will be best at 10 Hz or 16 Hz, due to the required satellite limits.



### Summary

This series of tests aims to identify the optimal configuration - 3 constellations, satellite limits and logging rate.

The testing will take a significant length of time, but at the end of it there should be some definitive results.

The optimal configuration should then be clearly apparent - e.g. GPS + Galileo + BeiDou B1C @ 10 Hz.



### Useful Tools

Use [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html) with mask angle of 5 degrees to ascertain the expected number of satellites for each constellation.

Ignore the square satellites (geo-stationary) and focus only on the round ones (MEO).