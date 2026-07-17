## Static ESP Testing

**\* THIS PAGE IS WORK IN PROGRESS AND NOT FOR SHARING OR REVIEW \***



### Overview

The [ESP GPS](https://github.com/RP6conrad/ESP-GPS-Logger) provides a number of configuration options which directly impact GNSS performance:

- GNSS - GPS, GLONASS, Galileo, BeiDou
- Max satellites
- Sample rate
- CPU frequency (ESP32)

The objective of this study was to identify the optimal ESP GPS configuration(s), and provide clarity to the ESP GPS community.

It was anticipated that 3 constellations with a sample rate of 10 Hz would be optimal, and that 20 Hz would not be so useful.



### Recommendations

This study identified optimal settings for all ESP GPS users, including derivatives such as the LISA GPS.

- GNSS = GPS + Galileo + BeiDou B1C
- Max satellites = 28
- Sample rate = 5 Hz
- CPU Freq = 160 MHz
- Logging = GPY + TXT

It was slightly surprising to discover that 10 Hz is NOT optimal, but it actually degrades the accuracy of the device. Should anyone be interested in how all of these settings were identified, further details can be found throughout these pages.

It is also highly recommended that ESP GPS devices are switched on some time before being used on the water. It can sometimes take between 15 and 30 minutes for an ESP GPS to establish the best possible fix, and utilise the maximum number of available satellites.

The majority of ESP GPS users do not need to know how the optimal settings were identified. The majority of ESP GPS users can simply use the optimal settings as recommended, but anyone wanting further details can read the remainder of this content.



### Approach

The SYRAC GPS is based on the ESP GPS, and 7 identical units were made available for static testing. The static testing was conducted from a rooftop in Tarifa (Spain) and are precursors to any kinematic testing on the water.

Static testing is extremely effective because in reality the devices have a constant velocity, exactly matching the rotation of the earth. The satellites are in [Medium Earth Orbit](https://en.wikipedia.org/wiki/Medium_Earth_orbit) (MEO) and the earth is rotating, but Speed Over Ground ([SOG](https://en.wikipedia.org/wiki/Ground_speed)) is zero within the [ECEF coordinate system](https://en.wikipedia.org/wiki/Earth-centered,_Earth-fixed_coordinate_system).

Previous tests for devices such as the Locosys GT-11, GT-31, GW-60, Motion GPS, and Garmin watches have all shown that performance during static testing is highly indicative of kinematic performance. The best devices during static testing will typically perform best on the water.

Each of the tests lasted for a period of at least 6 hours, which is roughly half of the time time that it takes for a full orbit of the various GNSS constellations. Comparisons are only made between devices during the same test period, never across different test periods.

The primary focus of this investigation was the accuracy of Speed Over Ground (SOG). The first 30 minutes is always discarded to allow for cold starts, and so is the last 5 minutes to allow for any disruption during shutdown. The statistics were produced using Python code.



### Phases

This study consisted of 7 individual test phases, each containing a number of different configurations run in parallel.

|                                          |                  Constellations                   |         Summary          |
| ---------------------------------------- | :-----------------------------------------------: | :----------------------: |
| [Phase 1](test-phases/phase-1/README.md) |          GPS + GLONASS vs GPS + Galileo           |    GLONASS vs Galileo    |
| [Phase 2](test-phases/phase-2/README.md) | GPS + Galileo + GLONASS vs GPS + Galileo + BeiDou |    GLONASS vs BeiDou     |
| [Phase 3](test-phases/phase-3/README.md) | GPS + Galileo + GLONASS vs GPS + Galileo + BeiDou | Satellite limits @ 15 Hz |
| [Phase 4](test-phases/phase-4/README.md) |              GPS + Galileo + BeiDou               | Satellite limits @ 5 Hz  |
| [Phase 5](test-phases/phase-5/README.md) |              GPS + Galileo + BeiDou               | Satellite limits @ 5 Hz  |
| [Phase 6](test-phases/phase-6/README.md) |              GPS + Galileo + BeiDou               | Satellite limits @ 10 Hz |
| [Phase 7](test-phases/phase-7/README.md) |              GPS + Galileo + BeiDou               |      5 Hz vs 10 Hz       |

Separate pages describe the individual test phases, accessible via the links in the table.



### Findings

The initial tests showed that GPS + Galileo performs better than GPS + GLONASS. The tests were performed in Tarifa (Spain), and should apply to most popular windsurfing regions, but further testing may also be worthwhile at higher latitudes (e.g. Norway, Sweden, or Finland).

Latitude is potentially relevant because GLONASS satellites use an orbital inclination of 64.8° as opposed to 55° (GPS + BeiDou) or 56° (Galileo). This ensures that GLONASS satellites appear higher above the horizon when the latitude of the receiver is above 55° (e.g. north of Moscow).

Introducing a third GNSS demonstrated how GPS + Galileo + BeiDou B1C is better than GPS + Galileo + GLONASS. The use of GLONASS as a third system sometimes degraded the overall solution quality, but this may be different at higher latitudes.

The earliest tests focused on sample rates between 5 Hz and 20 Hz, but the final tests focused on 5 Hz and 10 Hz. Just like the Motion GPS it was determined that sample rates of 10 Hz and higher actually degrade the solution quality, offering no obvious benefit over 5 Hz.



### Further Details

To reduce the length of this page, further details are provided on separate pages.

#### Methodology

- [Test approach](test-approach/README.md)
- [Technical details](tech-details/README.md)
- [SYRAC devices](syrac-devices/README.md)
- [Key findings](key-findings/README.md)

#### Next Steps

- [Elevation mask](elevation-mask/README.md)
- [ESP enhancements](esp-enhancements/README.md)
- [Kinematic testing](kinematic-testing/README.md)

#### Theory

- [Satellite orbits](satellite-orbits/README.md)
- [Accuracy and HDOP](accuracy-hdop/README.md)
- [Sampling rates](sampling-rates/README.md)
- [GPY vs SBP](gpy-sbp/README.md)
