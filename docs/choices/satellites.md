## Satellites

### Constellations

Supported through `CFG-SIGNAL` keys

https://content.u-blox.com/sites/default/files/MAX-M10S_DataSheet_UBX-20035208.pdf

Parameter GPS+GAL GPS+GAL+GLO GPS+GAL+BDS B1I (default) GPS+GAL+BDS B1C GPS+GAL+BDS B1C+GLO
Default 10 Hz 6 Hz 3 Hz 8 Hz 4 Hz 
High performance  20 Hz 16 Hz 12 Hz 16 Hz 10 Hz

Sky view - https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951



Motion supported GPS + GLONASS + Galileo



#### BeiDou

The B1I and B1C are both civilian signals broadcast by the BeiDou Navigation Satellite System (BDS). B1I is the legacy signal designed for the older BeiDou-2 system, while B1C is a modernized, high-performance signal introduced with the global BeiDou-3 system.

Here are the key differences between the two signals:

1. Carrier Frequency
B1I: Transmits at 1561.098 MHz. This is a unique frequency used by BeiDou.
B1C: Transmits at 1575.42 MHz. This is the exact same frequency used by GPS L1 and Galileo E1, which allows receivers to process these signals together more easily.



#### QZSS

Asia / Oceania



### Satellite Based Augmentation Systems (SBAS)

- Primarily improves positional accuracy
- SBAS improves signal accuracy by mitigating some of the ionospheric errors
- `CFG-SIGNAL` to enable SBAS



### Filters

High numbers are good, but approaching the limit of 32 may not be ideal:

- Burden on the MCU
- Low elevation satellites have an increased risk of both multipath and increased ionospheric delay / distortion
- Poor C/N0
- Diminishing returns

Once weak signals are dropped, the engine dynamically balances the highest C/N₀ streams against those providing the lowest math residuals and the best spatial distribution (sky topology).

You can configure a u-blox chip to limit its navigation solution to a fixed maximum number of satellites, and the receiver will automatically select the best candidates based on internal metrics including C/N₀ and geometric geometry.

However, you cannot manually force the selection to exclusively rank by C/N₀ power alone, because the module must also prioritize Geometric Dilution of Precision (GDOP) and low residual errors to prevent accurate but tightly bunched satellites from degrading your position fix.



#### Number of Satellites

By default, modern multi-constellation modules (like M9 or F9) can use up to 32 (or more) satellites simultaneously. If you lower INFIL_MAXSVS to a specific number (e.g., 16), the chip will truncate its active tracking list. Combined with your C/N₀ filter and its internal mathematical selection, it limits the processing payload.

- `CFG-NAVSPG-INFIL_MAXSVS` - default is 32

Motion = 8 per constellation?



#### Elevation Mask

Minimum elevation for a GNSS satellite to be used in navigation.

A low elevation angle means there's an increased risk of both multipath and increased ionospheric delay/distortion.

Setting an elevation mask of 10° to 15° automatically strips out the weakest satellites before the internal selection engine even evaluates them, naturally leaving the receiver to focus on the stronger overhead signal.

  - `CFG-NAVSPG-INFIL_MINELEV` - defaults to 5 degrees
  - Try 15

References:

- https://docs.novatel.com/OEM7/Content/Commands/ELEVATIONCUTOFF.htm - considered low elevation if it is between 0 and 15 degrees
- https://help.fieldsystems.trimble.com/tbc/2359.htm - Trimble applies a default elevation mask of 13°
- https://help.veripos.com/s/article/Elevation-Mask - Veripos applies a default elevation mask of 10°

https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951 - mask angle 10 degrees



#### C/N0 Thresholds

Open Sky: Use 30 to 35 dB-Hz. If you have perfect signal conditions, raising the threshold filters out marginal multi-path and weak signals, saving processing power and potentially increasing position accuracy.

When you restrict maxSVs, the internal u-blox navigation engine evaluates all tracked satellites in view and dynamically trims the pool down to your cap using the following criteria:
Signal Quality Thresholds:

You can proactively filter out weak signals globally by adjusting `CFG-NAVSPG-INFIL_MINCNO` (defaults to 6 dBHz) to a floor value like 35 dB-Hz.

This stops the receiver from even considering low C/N₀ satellites.

Once weak signals are dropped, the engine dynamically balances the highest C/N₀ streams against those providing the lowest math residuals and the best spatial distribution (sky topology).



#### Advanced Filtering

If your application strictly requires an exact number of satellites sorted by C/N₀, you must handle this on your external microcontroller/host software: Enable the UBX-NAV-SAT binary message (or the standard NMEA GSV sentences) to stream data for all tracked satellites. Read the array of Satellites, extracting their C/N₀ and PRN codes. Run a quick sorting algorithm on your host microcontroller to pick your fixed number of top signals. Feed those specific satellite measurements into your custom navigation algorithm or localized filtering loop



### References

https://www.u-blox.com/en/blogs/tech/gps-accuracy-four-gnss-constellations
The number of tracked satellites from each constellation was limited to eight.

UBX + veton 2025-05-22 https://www.seabreeze.com.au/forums/Windsurfing/Gps/Another-DIY-GPS-logger-approach?page=54

