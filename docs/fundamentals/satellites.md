## Satellites

### Constellations

The table below highlights a few key aspects of the signals supported by the M10. It omits details such as modulation, code frequency / chipping rate, primary PRN / code length, etc. Nevertheless, GLONASS and B1I are clearly the odd ones because of their differing frequencies and use of FDMA. The other signals have all been designed to co-exist on the same central frequency, simplifying receiver design and improving performance. The BeiDou B1C and Galileo E1 signals also benefit from modern signal designs, including individual data and pilot components.

| Constellation | Signal |        Frequency         | Technique |  Components  |      |
| ------------- | :----: | :----------------------: | :-------: | :----------: | :--: |
| GPS           | L1 C/A |       1575.42 MHz        |   CDMA    |     Data     |      |
| GLONASS       |  L1OF  | 1598.0625 - 1605.375 MHz |   FDMA    |     Data     |      |
| BeiDou        |  B1I   |       1561.098 MHz       |   CDMA    |     Data     |      |
| BeiDou        |  B1C   |       1575.42 MHz        |   CDMA    | Data + Pilot |      |
| Galileo       |   E1   |       1575.42 MHz        |   CDMA    | Data + Pilot |      |
| SBAS          | L1 C/A |       1575.42 MHz        |   CDMA    |     Data     |      |
| QZSS          | L1 C/A |       1575.42 MHz        |   CDMA    |     Data     |      |
| QZSS          |  L1S   |       1575.42 MHz        |   CDMA    |     Data     |      |

There is a useful online tool called [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html?t=1781765528951) which can be used to determine the visible GNSS satellites at any given time.



#### GLONASS

GLONASS currently uses FDMA, instead of CDMA like the other systems. The system is recognised as being less accurate than its rivals; GPS, BeiDou, and Galileo.

M10 configurations should probably use GPS + Galileo + BeiDou B1C, instead of GPS + Galileo + GLONASS. The processing burden is lower for the M10, and the results are likely to be more accurate.



#### BeiDou

The [MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf) claims that tracking and reacquisition sensitivity for acquired signals is approximately at the same level for BeiDou B1I and B1C.

<u>BeiDou B1I</u>

- Faster TTFF and higher start-up sensitivity. BeiDou B1I signals are acquired significantly faster and at a lower signal level than BeiDou B1C signals.
- Better availability. Higher start-up sensitivity results in a larger number of BeiDou satellites tracked and used in navigation solution especially at low signal level.

<u>BeiDou B1C</u>

- Concurrent reception of 4 GNSSs with GPS L1 C/A, Galileo E1, BeiDou B1C, and GLONASS L1OF.
- Lower power consumption. No additional frequency band required for BeiDou B1C in multiGNSS constellations, resulting in a lower power consumption during acquisition and tracking phases.

Notes

- BeiDou B1I and BeiDou B1C are sometimes referred to as BDS B1I and BDS B1C.
- The BeiDou B1I signal cannot be used simultaneously with the BeiDou B1C or GLONASS L1OF signals.



#### Galileo

Galileo is one of the most accurate GNSS systems, and should always be one of the constellations used in addition to GPS.

Suggest GNSS configurations including GPS + Galileo + BeiDou B1C.



### Augmentation Systems

#### Satellite Based Augmentation Systems (SBAS)

SBAS performs two roles, firstly for [Differential GPS (DGPS)](https://en.wikipedia.org/wiki/Differential_GNSS):

- Potentially improves signal accuracy by mitigating some of the ionospheric errors.
- Primarily improves positional accuracy by providing range corrections.

Secondly, SBAS satellites (geostationary, not MEO) can also be used to calculate positions.

- This is generally regarded as a bad thing to do, and can reduce accuracy.

By all means use SBAS for corrections, but don't use it as supplementary satellites for position fixes.



#### Quasi-Zenith Satellite System (QZSS)

Quasi-Zenith Satellite System (QZSS) is a regional navigation satellite system that transmits additional GPS L1 C/A signals for the Pacific region covering Japan and Australia.

The M10 is able to receive and track these signals concurrently with GPS signals, resulting in better availability, especially under challenging signal conditions. It is akin to a few extra GPS satellites in Japan and Australia.



### Configuration

#### Enabling Signals

Individual signals are enabled using `CFG-SIGNAL` keys which are described in the [u-blox M10 SPG 5.30 Interface description](https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.30_InterfaceDescription_UBXDOC-304424225-20395.pdf).

You need to be sure that your selection will not overwhelm the M10 with too many signals, which also relates to update rates.



#### Existing Devices

Popular devices within the speed sailing community:

| Constellations / Signals             | Motion | ESP-GPS |
| ------------------------------------ | :----: | :-----: |
| GPS + Galileo                        |   ❓    |    ✅    |
| GPS + GLONASS                        |   ❓    |    ✅    |
| GPS + GLONASS + Galileo              |   ✅    |    ✅    |
| GPS + Galileo + BeiDou B1C           |   ❌    |    ✅    |
| GPS + GLONASS + Galileo + BeiDou B1C |   ❌    |    ✅    |

n.b. It is not known whether the Motion with M10 uses GPS + Galileo, or GPS + GLONASS when running at 10 Hz.



### Filters

High numbers of satellites are good, but approaching the limit of 32 may not be ideal:

- Burden on the M10
- Low elevation satellites have an increased risk of both multipath and increased ionospheric delay / distortion
- Poor C/N₀ from some satellites

It is sometimes worth limiting the number of satellites used for the fix:

- Once weak signals are dropped, the engine dynamically balances the highest C/N₀ streams against those providing the lowest math residuals and the best spatial distribution (sky topology).
- You can configure a u-blox chip to limit its navigation solution to a fixed maximum number of satellites, and the receiver will automatically select the best candidates based on internal metrics including C/N₀ and geometric geometry.
- However, you cannot manually force the selection to exclusively rank by C/N₀ power alone, because the module must also prioritize Geometric Dilution of Precision (GDOP) and low residual errors to prevent accurate but tightly bunched satellites from degrading your position fix.



#### Number of Satellites

By default the M10 can track up to 32 satellites simultaneously and use them for PVT. If you lower `INFIL_MAXSVS` to a specific number the chip will truncate its active tracking list. Combined with any C/N₀ filter(s) and its internal mathematical selection, it limits the processing payload.

- `CFG-NAVSPG-INFIL_MAXSVS` - default is 32

Limiting the number of satellites often makes sense for people with lots of satellites visible (e.g. BeiDou in Asia).

n.b. The Motion GPS limits the number of satellites to 24 when logging at 5 Hz, and 16 when logging at 10 Hz. It appears to be placing a limit of 8 satellites per constellation, presumably deciding for itself which signals are being used at any one time.



#### Elevation Mask

Satellites at a low elevation angle have an increased risk of both multipath, and increased ionospheric delay/distortion.

Setting an elevation mask of 10° to 15° is common in marine environments. Eliminating these low elevation signals before the internal selection engine even evaluates them leaves it to focus on the more reliable signals.

The M10 elevation mask defaults to 5° but can be changed using `CFG-NAVSPG-INFIL_MINELEV`.

Changing it to 15° is likely to be beneficial when speed sailing, especially in environments with nearby cliffs, buildings, or ships.

References:

- [NovAtel](https://docs.novatel.com/OEM7/Content/Commands/ELEVATIONCUTOFF.htm) state that a satellite is considered low elevation if it is between 0 and 15° above the horizon
- [Trimble](https://help.fieldsystems.trimble.com/tbc/2359.htm) say the elevation mask is usually set to 13° by default to avoid interference problems
- [Veripos](https://help.veripos.com/s/article/Elevation-Mask) apply a default elevation mask of 10°

The online [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html) can also apply a mask angle.



#### C/N₀ Thresholds

Open Sky: Use 30 to 35 dB-Hz. If you have perfect signal conditions, raising the threshold filters out marginal multi-path and weak signals, saving processing power and potentially increasing position accuracy.

When you restrict maxSVs, the internal u-blox navigation engine evaluates all tracked satellites in view and dynamically trims the pool down to your cap. You can proactively filter out weak signals globally by adjusting `CFG-NAVSPG-INFIL_MINCNO` (defaults to 6 dBHz) to a floor value like 35 dB-Hz. This stops the receiver from even considering low C/N₀ satellites.

Once weak signals are dropped, the engine dynamically balances the highest C/N₀ streams against those providing the lowest math residuals and the best spatial distribution (sky topology).



#### Advanced Filtering

If your application strictly requires an exact number of satellites sorted by C/N₀, you must handle this on your external microcontroller/host software.

Enable the `UBX-NAV-SAT` binary message to stream data for all tracked satellites. Read the array of Satellites, extracting their C/N₀ and PRN codes. Run a quick sorting algorithm on your host microcontroller to pick your fixed number of top signals. Feed those specific satellite measurements into your custom navigation algorithm or localized filtering loop.

It is possible that the Motion does something along these lines to limit the number of satellites to 24, perhaps allowing 8 per constellation.



### References

- [GPS accuracy: The benefits of tracking all four global GNSS constellations](https://www.u-blox.com/en/blogs/tech/gps-accuracy-four-gnss-constellations) - u-blox, 5 Nov 2020

- [Another DIY GPS logger approach](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Another-DIY-GPS-logger-approach?page=54) - veton, 22 May 2025 10:14pm

