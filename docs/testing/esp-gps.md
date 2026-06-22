## ESP-GPS Testing

Choosing the right constellations, satellite limits, and logging rates is a fundamental decision.

Static testing provides a controlled environment to test devices systematically, and is very easy to perform.

Be aware that the +/- values in the software may mislead you... see [earlier test](../testing/static-5hz-10hz.md) comparing 5 Hz and 10 Hz.

This battery of tests has been inspired by the plan for [fundamentals testing](fundamentals.md), but is specific to the ESP-GPS.



### Overview

There are several phases planned, which can be all be split up over a number of days:

1. Test different logging rates for 2 constellations - 6 hours, excluding analysis
2. Test whether addition of Galileo improves the accuracy of the results - 6 hours, excluding analysis
3. Test whether addition of BeiDou B1C improves the accuracy of the results - 6 hours, excluding analysis
4. Test the 3 constellation configurations (GLONASS vs BeiDou B1C) - 6 hours, excluding analysis
5. Compare 4 constellations against the best 3 constellation configuration - 6 hours, excluding analysis

The final outcome should be an optimal configuration for the existing ESP-GPS devices.

Note: 16 Hz is not a divisor of 1000, but it is closely related to 4 Hz and 8 Hz.



### Approach

#### Standard Configuration

- M10 clocked at 192 MHz - high performance
- Baud rate of 115,200
- ESP32 devices clocked according to the logging rate
  - 80 MHz for 8 Hz
  - 160 MHz to 16 Hz
  - 240 MHz for 20 Hz
- 2 x Mini Motion @ 5 Hz included in all tests

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
- Dropped frames
  - Indication of CPU bandwidth being exceeded



### Phase 1

Compare each of the 2 constellation configurations, recording data for a minimum of 2 hours:

| Test |  ESP-GPS #1   |  ESP-GPS #2   | Rate  |
| :--: | :------------ | :------------ | :---: |
| 1.1  | GPS + GLONASS | GPS + Galileo | 10 Hz |
| 1.2  | GPS + GLONASS | GPS + Galileo | 16 Hz |
| 1.3  | GPS + GLONASS | GPS + Galileo | 20 Hz |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 6 hours, excluding analysis

#### Expectations

I suspect that GLONASS will have the least favourable results, put it needs some actual proof.

The 20 Hz tests might result in some dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Phase 2

Test whether addition of Galileo improves the accuracy of the results, recording data for a minimum of 2 hours:

| Test | ESP-GPS #1              | ESP-GPS #2                 | Rate  |
| :--: | :----------------------------------- | :------------------------- | :---: |
| 2.1 | GPS + GLONASS + Galileo | GPS + GLONASS | 10 Hz |
| 2.2 | GPS + GLONASS + Galileo | GPS + GLONASS | 16 Hz |
| 2.3 | GPS + GLONASS + Galileo @ 16 Hz | GPS + GLONASS @ 20 Hz | - |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 6 hours, excluding analysis

#### Expectations

The addition of Galileo should improve the accuracy of the results.

The 16 Hz tests might result in some dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Phase 3

Test whether addition of BeiDou B1C improves the accuracy of the results, recording data for a minimum of 2 hours:

| Test |             ESP-GPS #1             |      ESP-GPS #2       | Rate  |
| :--: | :--------------------------------- | :-------------------- | :---: |
| 3.1  |     GPS + Galileo + BeiDou B1C     |     GPS + Galileo     | 10 Hz |
| 3.2  |     GPS + Galileo + BeiDou B1C     |     GPS + Galileo     | 16 Hz |
| 3.3  | GPS + Galileo + BeiDou B1C @ 16 Hz | GPS + Galileo @ 20 Hz |   -   |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 6 hours, excluding analysis

#### Expectations

The addition of BeiDou B1C should improve the accuracy of the results.

The 16 Hz tests might result in some dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Phase 4

Test the 3 constellation configurations (GLONASS vs BeiDou B1C), recording data for a minimum of 2 hours:

| Test |       ESP-GPS #1        |         ESP-GPS #2         | Rate  |
| :--: | :--------------------- | :------------------------- | :---: |
| 4.1  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 8 Hz  |
| 4.2  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 10 Hz |
| 4.3  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 16 Hz |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 6 hours, excluding analysis

#### Expectations

I suspect that GLONASS will have the least favourable results, put it needs some actual proof.

The 16 Hz tests might result in some dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Phase 5

Compare 4 constellations against the best 3 constellation configuration, recording data for a minimum of 2 hours:

| Test |                  ESP-GPS #1                  |             ESP-GPS #2             | Rate  |
| :--: | :------------------------------------------- | :--------------------------------- | :---: |
| 5.1  |     GPS + Galileo + BeiDou B1C + GLONASS     |     GPS + Galileo + BeiDou B1C     | 8 Hz  |
| 5.2  |     GPS + Galileo + BeiDou B1C + GLONASS     |     GPS + Galileo + BeiDou B1C     | 10 Hz |
| 5.3  | GPS + Galileo + BeiDou B1C + GLONASS @ 10 Hz | GPS + Galileo + BeiDou B1C @ 16 Hz |   -   |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 6 hours, excluding analysis

#### Expectations

I suspect that 4 systems will show negligible benefit, because the maximum number of satellites is limited to 32.

The 10 Hz tests might result in some dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Summary

This series of tests aims to identify the optimal ESP-GPS configuration from the available options.

The testing consists of several phases, but in the end there should be some clarity on the best configuration.

Hopefully the optimal configuration will be unambiguous - e.g. GPS + Galileo + BeiDou B1C @ 10 Hz.

Future refinements to the ESP-GPS configuration may benefit from any findings during [fundamentals testing](fundamentals.md).



### Useful Tools

Use [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html) with mask angle of 5 degrees to ascertain the expected number of satellites for each constellation.

Ignore the square satellites (geo-stationary) and focus only on the round ones (MEO).