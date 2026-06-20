## Introduction

These pages document various aspects of the u-blox M10 that are relevant to the speed sailing community.

Developers of devices such the the [ESP-GPS](https://github.com/RP6conrad/ESP-GPS-Logger) (or similar) may find some of this information useful.



### UBX Config

- Fundamentals
  - [Satellites](fundamentals/satellites.md)
  - [Logging Rates](fundamentals/logging-rates.md)
  - [Suggestions](fundamentals/suggestions.md)
- Performance
  - [High Logging Rates](performance/high-rates.md)
  - [Signal Quality](performance/signal-quality.md)
  - [Solution Quality](performance/solution-quality.md)
- Testing
  - [Power Mode](testing/power-mode.md) - "balanced" vs "full power"
  - [Static Testing](testing/static-5hz-10hz.md) - 5 Hz vs 10 Hz
  
- Troubleshooting
  - [Noisy Data](troubleshooting/noisy-data.md)
  - [Dropped Points](troubleshooting/dropped-points.md)
  - [Timestamp Variations](troubleshooting/timestamp-variations.md)
  - [Slow Acquisition](troubleshooting/slow-acquisition.md)




### UBX Outputs

- UBX-NAV-PVT - Essential
- UBX-NAV-SAT - C/N₀
- UBX-NAV-DOP - HDOP
- UBX-NAV-VELNED - 3D speed



### References

#### Technical Documentation

- [MAX-M10 Product summary](https://content.u-blox.com/sites/default/files/MAX-M10_ProductSummary_UBX-20017987.pdf)
- [MAX-M10M-00B Data sheet](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_DataSheet_UBX-22028884.pdf) - 18 Jan 2026
- [MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf) - 5 May 2026
- [u-blox M10 ROM 5.00 Release Notes](https://cdn.sparkfun.com/assets/2/0/d/7/4/u-blox_M10_ROM_5.00_ReleaseNotes_UBX-20050981.pdf) - 5 May 2021
- [u-blox M10 SPG 5.30 Interface description](https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.30_InterfaceDescription_UBXDOC-304424225-20395.pdf) - 15 Oct 2025
- [u-blox M9 SPG 4.04 Interface description](https://content.u-blox.com/sites/default/files/u-blox-M9-SPG-4.04_InterfaceDescription_UBX-21022436.pdf) - 27 Jun 2023
- [u-blox M8 Receiver description](https://www.u-blox.com/sites/default/files/products/documents/u-blox8-M8_ReceiverDescrProtSpec_UBX-13003221.pdf) - 20 Mar 2023



#### Articles

- [5 tips to enhance position accuracy in standard precision GNSS receivers](https://www.u-blox.com/en/blogs/tech/tips-to-improve-position-accuracy-of-standard-precision-GNSS-receiver) - u-blox, 30 Jan 2026
