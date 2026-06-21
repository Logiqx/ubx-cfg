## ESP-GPS Testing

Choosing the right constellations, satellite limits, and logging rates is a fundamental decision.

Static testing provides a controlled environment to test devices systematically, and is very easy to perform.

Be aware that the +/- values in the software may mislead you... see [earlier test](../testing/static-5hz-10hz.md) comparing 5 Hz and 10 Hz.

This battery of tests has been inspired by the plan for [fundamentals testing](fundamentals.md), but is specific to the ESP-GPS.



### Overview

There are several phases planned, which can be all be split up over a number of days:

1. Test different logging rates for 2 constellations - 12 hours, excluding analysis
2. Test different logging rates for 3 constellations - 10 hours, excluding analysis
3. Test different logging rates for 4 constellations - 8 hours, excluding analysis

The final outcome should be an optimal configuration from the existing ESP-GPS options.

Note: 16 Hz is not a divisor of 1000, but it is closely related to 4 Hz and 8 Hz.



### Approach

#### Standard Configuration

**Hardware**

- M10 clocked at 192 MHz - high performance
- Baud rate of 115,200
- ESP32 clocked according to the logging rate
  - 80 MHz for 8 Hz
  - 160 MHz to 16 Hz
  - 240 MHz for 20 Hz

**M10**

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
- Dropped frames
  - Indication of CPU bandwidth being exceeded



### Phase 1

Compare each of the 2 constellation configurations, recording data for a minimum of 2 hours:

| Test | Device 1      | Device 2      | Rate  |
| :--: | ------------- | ------------- | :---: |
| 1.1  | GPS + GLONASS | GPS + Galileo | 4 Hz  |
| 1.2  | GPS + GLONASS | GPS + Galileo | 5 Hz  |
| 1.3  | GPS + GLONASS | GPS + Galileo | 8 Hz  |
| 1.4  | GPS + GLONASS | GPS + Galileo | 10 Hz |
| 1.5  | GPS + GLONASS | GPS + Galileo | 16 Hz |
| 1.6  | GPS + GLONASS | GPS + Galileo | 20 Hz |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 12 hours, excluding analysis

#### Expectations

I suspect that GLONASS will have the least favourable results, put it needs some actual proof.

The 20 Hz tests might result in dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Phase 2

Compare each of the 3 constellation configurations, recording data for a minimum of 2 hours:

| Test | Device 1                | Device 2                   | Rate  |
| :--: | ----------------------- | -------------------------- | :---: |
| 2.1  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 4 Hz  |
| 2.2  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 5 Hz  |
| 2.3  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 8 Hz  |
| 2.4  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 10 Hz |
| 2.5  | GPS + Galileo + GLONASS | GPS + Galileo + BeiDou B1C | 16 Hz |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 10 hours, excluding analysis

#### Expectations

I suspect that GLONASS will have the least favourable results, put it needs some actual proof.

The 16 Hz tests might result in dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Phase 3

Compare 4 constellations against 3 constellations, recording data for a minimum of 2 hours:

| Test | Device 1                             | Device 2                   | Rate  |
| :--: | ------------------------------------ | -------------------------- | :---: |
| 3.1  | GPS + Galileo + BeiDou B1C + GLONASS | GPS + Galileo + BeiDou B1C | 4 Hz  |
| 3.2  | GPS + Galileo + BeiDou B1C + GLONASS | GPS + Galileo + BeiDou B1C | 5 Hz  |
| 3.3  | GPS + Galileo + BeiDou B1C + GLONASS | GPS + Galileo + BeiDou B1C | 8 Hz  |
| 3.4  | GPS + Galileo + BeiDou B1C + GLONASS | GPS + Galileo + BeiDou B1C | 10 Hz |

Ideally after completing these tests they should all be repeated, but with each device having the opposite role.

Halving the duration of individual tests to 1 hour will make it easier, but acquisition times need to be considered.

Total duration = 8 hours, excluding analysis

#### Expectations

I suspect that 4 systems will show negligible (if any) benefit because the maximum number of satellites is 32.

The 10 Hz tests might result in dropped frames, demonstrating that the CPU bandwidth has been exceeded.



### Summary

This series of tests aims to identify the optimal ESP-GPS configuration from the available options.

The testing consists of several phases, but in the end there should be some clarity on the best configuration.

Hopefully the optimal configuration will be unambiguous - e.g. GPS + Galileo + BeiDou B1C @ 10 Hz.

Future refinements to the ESP-GPS configuration may benefit from any findings during [fundamentals testing](fundamentals.md).



### Useful Tools

Use [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html) with mask angle of 5 degrees to ascertain the expected number of satellites for each constellation.

Ignore the square satellites (geo-stationary) and focus only on the round ones (MEO).