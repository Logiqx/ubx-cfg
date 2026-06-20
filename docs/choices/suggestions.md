## Suggestions

### Constellations

Use least 3

https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951 - mask angle 10 degrees

Consider QZSS + SBAS



### Rates

It might be worth limiting users to a smaller selection.

e.g. 1, 2, 5, and 10 Hz.

Static test - HDOP better at 5 Hz

Suggest systematic test *
Less systems = worse HDOP, translate into worse hAcc and sAcc

I do not like 15 Hz
C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Organised\ESP-GPS\Salvador, SYRAC-GPS\2026-04-26, SYRAC-GPS, 15 Hz



### Combinations

The following configurations are expected to produce the best performance from the M10:

| # Systems |     Systems     | Log Rate |   M10   |  ESP32  | Useful? |
| :-------: | :-------------: | :------: | :-----: | :-----: | :-----: |
|     4     | GPS+GAL+B1C+GLO |   4 Hz   | 128 MHz | 80 MHz  |    ❓    |
|     3     |   GPS+GAL+B1C   |   5 Hz   | 128 MHz | 80 MHz  |    ✅    |
|     4     | GPS+GAL+B1C+GLO |  10 Hz   | 192 MHz | 160 MHz |    ❓    |
|     3     |   GPS+GAL+B1C   |  10 Hz   | 192 MHz | 160 MHz |    ✅    |

Limiting the M10 to 2 constellations is not expected to perform as well as 3 constellations:

| # Systems | Systems | Log Rate |   M10   |  ESP32  | Useful? |
| :-------: | :-----: | :------: | :-----: | :-----: | :-----: |
|     2     | GPS+B1C |  10 Hz   | 128 MHz | 160 MHz |    -    |
|     2     | GPS+GAL |  10 Hz   | 128 MHz | 160 MHz |    -    |
|     2     | GPS+B1C |  20 Hz   | 192 MHz | 240 MHz |    -    |
|     2     | GPS+GAL |  20 Hz   | 192 MHz | 240 MHz |    -    |

IMPORTANT: Changing the M10 to 192 MHz is irreversible, and it CANNOT be changed back to 128 MHz. 



### Filters

Suggest implementing the following:

- Maximum number of satellites
- Elevation mask of 15 degrees

Not enough info on the following:

- C/N0 Thresholds
- Advanced Filtering



