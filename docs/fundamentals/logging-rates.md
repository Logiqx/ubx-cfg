## Logging Rates

### Introduction

10 Hz is twice as accurate as 5 Hz, right? It may be your expectation, but it is not that simple. Simple [static testing](../testing/static-5hz-10hz.md) has shown that 10 Hz can sometimes be worse than 5 Hz.

Reducing the number of constellations to facilitate higher logging rates can be counterproductive. The best accuracy will likely achieved from the best signals (GPS, Galileo and BeiDou B1C), and reliable update rates.



### Max Rates

The [MAX-M10M-00B Data sheet](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_DataSheet_UBX-22028884.pdf) shows some examples of max update rates:

| Constellations / Services                   | Default | High Performance |
| ------------------------------------------- | :-----: | :--------------: |
| GPS / GLONASS / BDS B1I / Galileo / BDS B1C |  18 Hz  |      25 Hz       |
| GPS + Galileo (default)                     |  10 Hz  |      20 Hz       |
| GPS + Galileo + BeiDou B1C                  |  8 Hz   |      16 Hz       |
| GPS + Galileo + GLONASS                     |  6 Hz   |      16 Hz       |
| GPS + Galileo + BeiDou B1I                  |  3 Hz   |      12 Hz       |
| GPS + Galileo + BeiDou B1C + GLONASS        |  4 Hz   |      10 Hz       |

Notes:

- These figures are all on the basis of a minimum 98% fix rate under typical conditions, not 100%.
- The defaults of 1 system at 18 Hz or 2 systems at 10 Hz are identical to the [NEO-M8Q and NEO-M8M](https://content.u-blox.com/sites/default/files/NEO-M8-FW3_DataSheet_UBX-15031086.pdf).
- The [NEO-M9M](https://content.u-blox.com/sites/default/files/NEO-M9N-00B_DataSheet_UBX-19014285.pdf) claims to support 25 Hz for all configurations, including 4 constellations.

High performance relates to when the M10 has been configured to use a higher clock speed:

- The default M10 clock speed is 128 MHz, whereas high performance is 192 MHz.
- Configuring the clock speed to 192 MHz is irreversible, and CANNOT be reverted back to 128 MHz.
- The configuration required to support the high performance rates is described in [Higher Logging Rates](../performance/high-rates.md).



#### 20 Hz and 25 Hz

20 Hz can only be achieved with 2 constellations.

- 2 constellations @ 20 Hz will potentially be worse than 3 or 4 systems @ 10 Hz

25 Hz can only be achieved with 1 constellation.

- 1 constellation @ 25 Hz will probably be worse than 3 or 4 systems @ 5 or 10 Hz

Both rates require the M10 to run in "high performance" mode, which requires more power, and more storage.



### Configuration

The [u-blox M10 SPG 5.30 Interface description](https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.30_InterfaceDescription_UBXDOC-304424225-20395.pdf) describes how to configure the navigation update rate.

- `CFG-RATE-MEAS` = Nominal time between GNSS measurements
- `CFG-RATE-NAV` = Ratio of number of measurements to number of navigation solutions
- `CFG-RATE-TIMEREF` = Time system to which measurements are aligned

The default time reference system is GPS, but those milliseconds should be identical to UTC.



#### Existing Devices

The table below lists some M10 devices, and the logging rates they support.

| Rate  | Motion | LISA GPS | ESP-GPS |
| :---: | :----: | :------: | :-----: |
| 1 Hz  |   ✅    |    ✅     |    ✅    |
| 2 Hz  |   ✅    |    ✅     |    ✅    |
| 4 Hz  |   ❌    |    ✅     |    ✅    |
| 5 Hz  |   ✅    |    ✅     |    ✅    |
| 8 Hz  |   ❌    |    ✅     |    ✅    |
| 10 Hz |   ✅    |    ✅     |    ✅    |
| 15 Hz |   ❌    |    ❌     |    ✅    |
| 20 Hz |   ❌    |    ❌     |    ✅    |

Notes:

- The LISA GPS is based on the ESP-GPS
- The SYRAC-GPS is an ESP-GPS and mentions 3 and 6 Hz in the user guide, perhaps inspired by u-blox data sheets?



#### Implications of Non-Divisors

When `CFG-RATE-MEAS` is not a divisor of 1000 the timestamps will not be consistent from one second to the next.

This chart shows 15 Hz data from an ESP-GPS. Intriguingly .995 and  .996 rarely occur, seemingly being logged at .000.

![15hz-distribution](img/15hz-distribution.png)

I am not really a fan of non-divisors, and prefer timestamps that are consistent from one second to the next.

- 0.000, 0.100, 0.200, etc.

Regular timestamps are easier to read, and non-divisors can cause complications for speed analysis software.



#### Popular Update Rates

Popular update rates include the following:

| Rate  | CFG-RATE-MEAS | CFG-RATE-NAV |
| :---: | :-----------: | :----------: |
| 1 Hz  |     1000      |      1       |
| 2 Hz  |      500      |      1       |
| 5 Hz  |      200      |      1       |
| 10 Hz |      100      |      1       |
| 20 Hz |      50       |      1       |

4 Hz, 8 Hz and 25 Hz also have a number of valid use cases, and they are all divisors of 1000.



#### Unusual Update Rates

It is worth mentioning the MAX M10 data sheet also refers to several update rates that are not divisors of 1000:

| Rate  | CFG-RATE-MEAS | CFG-RATE-NAV |
| :---: | :-----------: | :----------: |
| 3 Hz  |      334      |      1       |
| 6 Hz  |      167      |      1       |
| 12 Hz |      84       |      1       |
| 16 Hz |      63       |      1       |
| 18 Hz |      56       |      1       |

I suspect that these update rates we chosen to illustrate what the MAX M10 is capable of achieving 98% of the time.



### Observations

#### Accuracy

Previous testing has demonstrated that 3 systems @ 5 Hz can perform better than 2 systems @ 10 Hz. Not only did 10 Hz logging perform worse than 5 Hz, but +/- figures in analysis software suggests the complete opposite! The details have been documented on a separate page describing the [static testing](../testing/static-5hz-10hz.md) of 5 Hz and 10 Hz devices.



#### Aliasing

It should be noted that it is possible to request 1 Hz output in numerous ways, but it is not clear whether it impacts the u-blox Kalman filter.

| Rate | CFG-RATE-MEAS | CFG-RATE-NAV |
| :--: | :-----------: | :----------: |
| 1 Hz |      100      |      10      |
| 1 Hz |      200      |      5       |
| 1 Hz |      500      |      2       |
| 1 Hz |     1000      |      1       |

I wrote an article about the effects of [aliasing](https://logiqx.github.io/gps-details/general/aliasing/) and how it is evident in 1 Hz u-blox data. I wonder whether different combinations of `CFG-RATE-MEAS` and `CFG-RATE-NAV` might cause the M10 to implement a low-pass filter (LPF).

I was subsequently told that it may be possible to apply the u-blox LPF by computing the resultant vector of the North and East velocity fields, instead of using the ground speed field. I have not had an opportunity to investigate this any further.



### Troubleshooting

Setting `CFG-RATE-MEAS` to a value that is not a divisor of 1000 has already been discussed, and will result in irregular timestamps. This may be regarded as cosmetic, but it also has potential implications for speed analysis software.

The u-blox data sheets describe max update rates on the basis of a minimum 98% fix rate under typical conditions. Dropped points are still possible and will typically occur at the top of the epoch - between .000 and .200. The solution is using less satellites as [discussed](satellites.md) on another page, or reducing the logging rate.

The requirements for achieving the highest logging rates include the need for higher CPU speeds (M10 and / or ESP32), and higher baud rates. These topics are all described in detail on another page specific to [higher logging rates](../performance/high-rates.md).



### References

- [Another DIY GPS logger approach](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Another-DIY-GPS-logger-approach?page=54) - veton, 22 May 2025 10:14pm

