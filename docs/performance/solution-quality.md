## Solution Quality

Several configurations and filters might be considered to refine the M10 output.



### 2D / 3D Fix

There is no particular reason to allow a 2D fix, so might be worth mandating a 3D fix.

  - `CFG-NAVSPG-FIXMODE` = 2 (3D only)
    - Default is 3 (auto)

  - `CFG-NAVSPG-INIFIX3D` = 1
    - Default is 0 (false)




### Dynamic Model

The dynamic model affects how the navigation filter captures and smooths speed peaks.

- `CFG-NAVSPG-DYNMODEL` - default may be 0 (portable), or 9 (wrist)

|      | Name         | Description                                                  |
| ---- | ------------ | ------------------------------------------------------------ |
| 1    | Portable     | Applications with low acceleration, e.g., portable devices. Suitable for most situations.<br />Max speed (<310 m/s), low acceleration |
| 2    | Stationary   | Velocity restricted to 0 m/s. Zero dynamics assumed.<br />No motion expected |
| 3    | Pedestrian   | Applications with low acceleration and speed, e.g., how a pedestrian would move.<br />Speeds <30 m/s (~58.3 knots is too low), low acceleration |
| 4    | Automotive   | Used for applications with equivalent dynamics to those of a passenger car. Low vertical acceleration assumed.<br />Typical road speeds (<100 m/s), higher accelerations than pedestrian |
| 5    | Sea          | Recommended for applications at sea, with zero vertical velocity. Sea level assumed.<br />Speeds <25 m/s (~ 48.6 knots is too low), no altitude change |
| 6    | Airborne <1g | Used for applications with a higher dynamic range and greater vertical acceleration than a passenger car.<br />Up to 1g acceleration (3 times a speed sailor), max speed 100 m/s |
| 7    | Airborne <2g | Recommended for typical airborne environments. <br />Up to 2g acceleration, max speed 250 m/s |
| 8    | Airborne <4g | Only recommended for extremely dynamic environments.<br />Up to 4g acceleration, max speed 500 m/s |
| 9    | Wrist        | Only recommended for wrist-worn applications. The receiver will filter out arm motion.<br />Frequent signal loss (body shadowing), low speed |

Aside from "portable" the only dynamic model that may be useful when speed sailing is "automotive", which may be worth testing.

Would need to keep an eye out for any additional dead-reckoning (DR) behaviours!

Further details - [How to Choose a Suitable u-blox Dynamic GNSS Platform](https://base.xsens.com/s/article/How-to-Choose-a-Suitable-u-blox-Dynamic-GNSS-Platform?language=en_US) - Xsense, 4 Dec 2025



### Static Hold

For speed sailing, static hold thresholds should left at zero.

- `CFG-MOT-GNSSSPEED_THRS` - default is 0
- `CFG-MOT-GNSSDIST_THRS` - default is 0



### Navigation Input Filters

Navigation input filters may potentially prevent poor quality PVT solutions from a few satellites / signals.

#### Satellites

- `CFG-NAVSPG-INFIL_MINSVS` - default is 3
  - This corresponds a minimal 2D fix


#### C/N₀ Threshold

- `CFG-NAVSPG-INFIL_NCNOTHRS` - default is 0
  - Number of signals required above this threshold
- `CFG-NAVSPG-INFIL_CNOTHRS` - default is 0
  - Thresholds to consider might be 30 to 35 dB-Hz



### Navigation Output Filters

Navigation output filters can potentially prevent poor quality solutions (e.g. spikes) being output.

#### DOP / Accuracy

- `CFG-NAVSPG-OUTFIL_PDOP` - default is 250
- `CFG-NAVSPG-OUTFIL_TDOP` - default is 250
- `CFG-NAVSPG-OUTFIL_PACC` - default is 100 m
- `CFG-NAVSPG-OUTFIL_TACC` - default is 350 m
- `CFG-NAVSPG-OUTFIL_FACC` -  default is 150 m/s