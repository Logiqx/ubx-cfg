## Static ESP Testing - ESP Enhancements

### Overview

Throughout the SYNAC testing, possible ESP GPS enhancements (and bug fixes) have become apparent.



### Configuration

Possible enhancements, and bug fixes

- Add "elevation mask" (i.e. minimum elevation), default to 10 degrees
  - Quick way to ignore some poor signals, and ease the M10 workload
  - See [elevation mask](../elevation-mask/README.md) for further details
- Add "power mode" - either "balanced" (default) and "full power"
  - Potential fix for devices which exhibit noise issues - e.g. SY2
  - See [power mode](../power-mode/README.md) for further details
- Tweaks to code relating to CPU speed, because 160 MHz is required for 5 Hz
  - The comment "For 5 Hz sample_rate, CPU freq of 80 MHz is sufficient" needs to be revised
  - "if(reset_boot==true) {setCpuFrequencyMhz(80);}"  needs to be revised
- Fix GNSS spellings
  - GLONASS, Galileo, BeiDou
- Perhaps hide all of the GNSS settings inside "expert" settings?
  - Constellations, log rate, ESP clock, max sats, elevation mask, power mode
  - Various other non-GNSS settings may also be regarded as "expert" settings



### ESP Screen

Possible enhancements

- Perhaps have some kind of status screen?
  - Constellations
  - Number of satellites
  - HDOP
  - Horizontal Accuracy (hAcc)
  - Speed Accuracy (sAcc)
  - ... perhaps latitude, longitude, height above MSL, SOG, and COG
- Rounding results to 2 decimal places, instead of truncation?
  - I have not confirmed what the ESP does, but results should be rounded



### File Types

#### TXT

Possible enhancements 

- Additional items describing the configuration, or performance
  - Max Satellites - e.g. 28
  - Elevation mask - e.g. 10 degrees
  - Power mode - e.g. "balanced" or "full power"
  - M10 clock speed - e.g. 128 MHz or 192 MHz
  - Count of non-contiguous frames (i.e. interval exceeds expected ms)
- Fix the total distance
  - Ideally it should match unfiltered distance in GPS Speedreader



#### SBP

Possible enhancements, and bug fixes
- vsdop should be zero, since it relates to climb rate (and it is not even a DOP)
- SV list should be all zeros, unless determined from NAV-SAT (unnecessary imho)
- SBP header could be populated with name, serial number, firmware version, etc.



#### GPX

Possible enhancements

- Implement a low-pass filter prior to down-sampling to 1 Hz
  - See [decimation](https://logiqx.github.io/gps-wizard/ideas/decimation/) for full details



### Performance

Asynchronous I/O, if not already implemented
- In an "ideal" world, multi-threading can be used to prevent blocking behaviours
  1. Thread to consume UBX messages
  2. Thread to write to the SD card, and perform the flush (when necessary)
  3. Thread (or threads) for calculating stats, updating the display, etc.
- This would reduce the chance of dropped frames, and improve support for multiple files
  - e.g. GPY + UBX + TXT
- However... writing multi-threaded code is not easy, so it is perhaps not viable right now
