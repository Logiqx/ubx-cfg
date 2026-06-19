## Solution Quality

### 2D / 3D Fix
  - `CFG-NAVSPG-FIXMODE` = 2 (3D only), default = 3 (auto)
  - `CFG-NAVSPG-INIFIX3D` - default is 0 (false)



### Dynamic Model

- Affects how the navigation filter captures and smooths speed peaks
- `CFG-NAVSPG-DYNMODEL` - default may be 9 (wrist)
  - 0 = Portable
  - 3 = Pedestrian
  - 4 = Automotive
  - 5 = Sea is UNSUITABLE

https://base.xsens.com/s/article/How-to-Choose-a-Suitable-u-blox-Dynamic-GNSS-Platform?language=en_US



### Static Hold

Static hold / stationary thresholds

For speedsurfing, static hold should be OFF — it clamps low speeds to zero and should not affect a moving board.
- Do not assume the same "off" value across generations; confirm by logging low-speed behaviour.
- Supported through motion / navigation filter keys such as `CFG-MOT-*`



### Filters

If you want to filter very poor quality positions and speeds...

#### Satellites

- `CFG-NAVSPG-INFIL_MINSVS` - default is 3
  - Julien said the default used to be 5
  - Maybe need it to match the 2D / 3D


#### C/No

- `CFG-NAVSPG-INFIL_NCNOTHRS` - defaults to 0
  - Number above threshold
- `CFG-NAVSPG-INFIL_CNOTHRS` - defaults to 0
  - Might consider 30 to 35 dB-Hz

#### DOP / Accuracy

- `CFG-NAVSPG-OUTFIL_PDOP` - defaults to 250
- `CFG-NAVSPG-OUTFIL_TDOP` - defaults to 250
- `CFG-NAVSPG-OUTFIL_PACC` - defaults to 100 m
- `CFG-NAVSPG-OUTFIL_TACC` - defaults to 350 m
- `CFG-NAVSPG-OUTFIL_FACC` -  defaults to 150 m/s