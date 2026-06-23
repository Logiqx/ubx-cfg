## Fundamentals Testing

Choosing the right constellations, satellite limits, and logging rates is a complex, but crucial decision.

It would be good to identify the best performing configurations for the various M10 and ESP32 clock speeds.

Static testing provides a controlled environment to test devices systematically, and is very easy to perform.

Be aware that the +/- values in the software may mislead you... see [earlier test](../testing/static-5hz-10hz.md) comparing 5 Hz and 10 Hz.



### Overview

There are several phases planned, which can each be split up over a number of days:

1. Compare all of the different constellations - 12 hours
2. Test the effect of limiting the maximum number of satellites - 10 hours
3. Determine the maximum possible logging rates with up to 32 satellites - 10 hours
4. Determine the optimal balance between numbers of satellites and logging rates
5. Test additional configurations against the defaults - elevation mask, minimum C/N₀, etc.

The final outcome should be an optimal configuration for M10 receivers.



### Approach

#### Test Duration

- Individual tests should record for a total of 2 hours
- Ideally, ESP-32 devices should switch roles after 1 hour
- 2 x Mini Motions @ 5 Hz to be included in all tests

#### Configuration

- M10 clocked at 192 MHz - high performance
- Baud rate of 115,200
- Logging rate of 5 Hz, unless specified
- ESP32 clocked according to the logging rate
  - 80 MHz for 8 Hz
  - 160 MHz to 16 Hz
  - 240 MHz for 20 Hz

#### Data Analysis

- Acquisition times
  - Time taken to acquire all of the signals
- Cumulative results in GPS Speedreader
  - Speed - 1 hour averages
  - Total distance - derived from speed data
- Percentiles from individual values - 50, 68, 95, 99.7
  - Speed over Ground (SOG)
  - Speed Accuracy (sAcc)
  - Horizontal Dilution of Precision (HDOP)
- Dropped frames
  - Indication of CPU bandwidth being exceeded



### Phase 1

Compare all of the different constellations:

| Test | Device 1         | Device 2         |
| :--: | ---------------- | ---------------- |
| 1.1  | GPS + Galileo    | GPS + GLONASS    |
| 1.2  | GPS + Galileo    | GPS + BeiDou B1I |
| 1.3  | GPS + GLONASS    | GPS + BeiDou B1I |
| 1.4  | GPS + GLONASS    | GPS + BeiDou B1C |
| 1.5  | GPS + Galileo    | GPS + BeiDou B1C |
| 1.6  | GPS + BeiDou B1I | GPS + BeiDou B1C |

The tests have been ordered such that only one device needs to be reconfigured, prior to the next test.

Total duration = 12 hours, excluding analysis

#### Expectations

Interim results are possible whilst later tests are still underway.

- After the first 3 tests we should know the best 2 out of Galileo, GLONASS, and BeiDou B1I.
- After the first 5 tests we should know the best 2 out of Galileo, GLONASS, and BeiDou B1C.
- The final test will establish which is the best out of BeiDou B1I and BeiDou B1C.

I suspect that GLONASS will have the least favourable results, but it needs some actual proof.



### Phase 2

Test the effect of limiting the number of satellites for GPS + Galileo + BeiDou B1C:

| Test |    Unit 1     |    Unit 2     |
| :--: | :-----------: | :-----------: |
| 2.1  | Max Sats = 12 | Max Sats = 16 |
| 2.2  | Max Sats = 16 | Max Sats = 20 |
| 2.3  | Max Sats = 20 | Max Sats = 24 |
| 2.4  | Max Sats = 24 | Max Sats = 28 |
| 2.5  | Max Sats = 28 | Max Sats = 32 |

Total duration = 10 hours, excluding analysis

#### Expectations

Hopefully it will become clear how the number of satellites impacts the accuracy of results.

This is important because increasing the logging rate will necessitate a reduction in the number of satellites.



### Phase 3

Determine the maximum possible logging rates with up to 32 satellites:

| Test | Unit 1                     | Unit 2        | Rate  |
| :--: | -------------------------- | ------------- | :---: |
| 3.1  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 4 Hz  |
| 3.2  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 5 Hz  |
| 3.3  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 8 Hz  |
| 3.4  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 10 Hz |
| 3.5  | GPS + Galileo + BeiDou B1C | GPS + Galileo | 16 Hz |

Total duration = 10 hours, excluding analysis

Notes:

- 16 Hz is not a divisor of 1000, but it is closely related to 4 Hz and 8 Hz.

#### Expectations

Some of the tests might result in dropped frames, demonstrating that the CPU bandwidth has been exceeded.

Dropped frames can potential be avoided by reducing the maximum number of satellites from the default of 32.



### Phase 4

The fourth phase will aim to identify the perfect balance between number of satellites and logging rate.

- Best constellations - best combinations of 2 and 3 constellations
- Maximum number of satellites vs possible logging rates

The precise planning of this phase can be done after interpreting the results from phases 2 and 3.

#### Expectations

There may be a point where a 2 constellation performance roughly matches the 3 constellation performance.

Suspect that the accuracy from 2 constellations at 20 Hz may not be able to exceed 3 constellations at 10 Hz.

It is yet to be seen whether whether 3 constellations will be best at 10 Hz or 16 Hz, due to required satellite limits.



### Phase 5

Once the constellations and logging rates have been optimised, additional configurations can be tested against the defaults.

| Test | Configuration  | Parameter                |    Unit 1    |     Unit 2     |
| :--: | -------------- | ------------------------ | :----------: | :------------: |
| 5.1  | Elevation mask | CFG-NAVSPG-INFIL_MINELEV |      5°      |      10°       |
| 5.2  | Elevation mask | CFG-NAVSPG-INFIL_MINELEV |      5°      |      15°       |
| 5.3  | Minimum C/N₀   | CFG-NAVSPG-INFIL_MINCNO  |    6 dBHz    |    30 dBHz     |
| 5.4  | Minimum C/N₀   | CFG-NAVSPG-INFIL_MINCNO  |    6 dBHz    |    35 dBHz     |
| 5.5  | Dynamic model  | CFG-NAVSPG-DYNMODEL      | 1 = portable | 4 = automotive |

Total duration = 10 hours, excluding analysis

Notes:

- Elevation masks and minimum C/N₀ can be investigated with static testing, just like the earlier phases.
- Dynamic model comparisons need to be done on the water.

#### Expectations

The minimum elevation mask should be a reliable way to exclude some bad signals from the solutions.

Likewise with minimum C/N₀, although it may need to be specific to the receiver / antenna.

The dynamic model is a bit of a long shot, but "automotive" may prove to be suitable for speed sailing.



### Summary

The intended outcome of this investigation will be the optimal configurations, based on M10 and ESP32 clock speeds.

For example:

|                     |           M10 @ 128 MHz           |           M10 @ 192 MHz            |
| ------------------- | :-------------------------------: | :--------------------------------: |
| **ESP32 @ 80 MHz**  | GPS + Galileo + BeiDou B1C @ 8 Hz |                 -                  |
| **ESP32 @ 160 MHz** |                 -                 | GPS + Galileo + BeiDou B1C @ 16 Hz |

In order to prevent dropped frames, maximum numbers of satellites will almost certainly need to be restricted.

Different logging rates can be offered to anyone who wants smaller files, e.g. GPS + Galileo + BeiDou B1C @ 4 Hz.

Hopefully the optimal configurations will be unambiguous - e.g. GPS + Galileo + BeiDou B1C @ 8 Hz, 10° elevation.



### Useful Tools

Use [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html) with mask angle of 5 degrees to ascertain the expected number of satellites for each constellation.

Ignore the square satellites (geo-stationary) and focus only on the round ones (MEO).