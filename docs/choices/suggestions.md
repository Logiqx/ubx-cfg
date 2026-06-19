## Suggestions

### Constellations

Use least 3

https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951 - mask angle 10 degrees

QZSS + SBAS



### Rates

Max navigation update rate - Minimum 98% fix rate under typical conditions - default / high performance
4 systems = 4 / 10
3 systems = 8 / 16
2 systems (GPS + GAL) = 10 / 20
1 system = 18 / 25

Static test - HDOP better at 5 Hz

Suggest systematic test *
Less systems = worse HDOP, translate into worse hAcc and sAcc

I do not like 15 Hz
C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Organised\ESP-GPS\Salvador, SYRAC-GPS\2026-04-26, SYRAC-GPS, 15 Hz



### Combinations

Do as tables (ignore B1I):

4 systems - limited / no benefit

- GPS+GAL+B1C+GLO @ 4 Hz = 128 MHz u-blox (default) + 80 MHz ESP32
- GPS+GAL+B1C+GLO @ 10 Hz = 192 MHz u-blox (high performance) + 160 MHz ESP32

3 systems

* GPS+GAL+B1C @ 5 Hz = 128 MHz u-blox (default) + 80 MHz ESP32 				* recommended setting, but 8 Hz is also possible

- GPS+GAL+B1C @ 10 Hz = 192 MHz u-blox (high performance) + 160 MHz ESP32

2 systems - 16 sats (Manfred) or 27 sats (Paul)

- GPS+B1C @ 20 Hz = 192 MHz u-blox (high performance) + 240 MHz ESP32
- GPS+GAL @ 20 Hz = 192 MHz u-blox (high performance) + 240 MHz ESP32
  n.b. GPS+B1C or GPS+GAL @ 10 Hz = 128 MHz u-blox (default) + 160 MHz ESP32 BUT UNLIKELY TO BE USEFUL



### Filters

Suggest implementing the following:

- Maximum number of satellites
- Elevation mask of 15 degrees

Not enough info on the following:

- C/N0 Thresholds
- Advanced Filtering



### Existing Devices

#### Motion

Motion supported GPS + GLONASS + Galileo

- 3 systems @ 5 Hz can be better than 2 systems @ 10 Hz



#### ESP-GPS

Rates in https://github.com/RP6conrad/ESP-GPS-Logger/blob/master/Ublox.h
M10 - ESP-GPS supports 1 2 4 5 8 10 15 [eurgh] 20 but excludes 3 + 6 + 12 + 16 + 18 [all eurgh] + 25
	SYRAC user guide mentions 3 and 6 [eurgh]



