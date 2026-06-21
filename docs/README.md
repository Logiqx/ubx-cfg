## Introduction

These pages document various aspects of the u-blox M10 that are relevant to the speed sailing community.

Developers of devices such the the [ESP-GPS](https://github.com/RP6conrad/ESP-GPS-Logger) (or similar) may find some of this information useful.



### UBX Config

- Fundamentals
  - [Satellites](fundamentals/satellites.md) - constellations + filters
  - [Logging Rates](fundamentals/logging-rates.md) - max rates + accuracy
  - [Suggestions](fundamentals/suggestions.md) - constellations + filters + rates
- Performance
  - [High Logging Rates](performance/high-rates.md) - CPU / MPU + baud rates
  - [Signal Quality](performance/signal-quality.md) - power savings and LNA
  - [Solution Quality](performance/solution-quality.md) - models + filters
- Testing
  - [Power Mode](testing/power-mode.md) - "balanced" vs "full power"
  - [Static Testing](testing/static-5hz-10hz.md) - 5 Hz vs 10 Hz
  - [Fundamentals](testing/fundamentals.md) - optimal satellites + rates
  - [ESP-GPS](testing/esp-gps.md) - optimal ESP-GPS configuration
  
- Troubleshooting
  - [Noisy Data](troubleshooting/noisy-data.md) - power mode
  - [Dropped Points](troubleshooting/dropped-points.md) - CPU bandwidth
  - [Timestamp Variations](troubleshooting/timestamp-variations.md) - TBC
  - [Slow Acquisition](troubleshooting/slow-acquisition.md) - TBC




### UBX Outputs

- UBX-NAV-PVT - Essential
- UBX-NAV-SAT - C/N₀
- UBX-NAV-DOP - HDOP
- UBX-NAV-VELNED - 3D speed



### References

#### Technical Documentation

- [MAX-M10 Product summary](https://content.u-blox.com/sites/default/files/MAX-M10_ProductSummary_UBX-20017987.pdf)
- [MAX-M10M-00B Data sheet](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_DataSheet_UBX-22028884.pdf)
- [MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf)
- [u-blox M10 ROM 5.00 Release Notes](https://cdn.sparkfun.com/assets/2/0/d/7/4/u-blox_M10_ROM_5.00_ReleaseNotes_UBX-20050981.pdf)
- [u-blox M10 SPG 5.30 Interface description](https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.30_InterfaceDescription_UBXDOC-304424225-20395.pdf)
- [u-blox M9 SPG 4.04 Interface description](https://content.u-blox.com/sites/default/files/u-blox-M9-SPG-4.04_InterfaceDescription_UBX-21022436.pdf)
- [u-blox M8 Receiver description](https://www.u-blox.com/sites/default/files/products/documents/u-blox8-M8_ReceiverDescrProtSpec_UBX-13003221.pdf)



#### Articles

- [5 tips to enhance position accuracy in standard precision GNSS receivers](https://www.u-blox.com/en/blogs/tech/tips-to-improve-position-accuracy-of-standard-precision-GNSS-receiver) - u-blox, 30 Jan 2026



#### Tools

- [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951) by QZSS
