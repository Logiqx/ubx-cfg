## Static ESP Testing - Elevation Mask

### Background

Satellites at a low elevation angle have an increased risk of both multipath, and ionospheric delay / distortion. The default elevation mask for u-blox SPG products is 5°,  including M8 / M9 / M10 chipsets.

Specifying an elevation mask of 10° to 15° is relatively common in marine environments. Eliminating these low elevation signals before the internal selection engine even evaluates them leaves it to focus on the more reliable signals.

- `CFG-NAVSPG-INFIL_MINELEV` - default is 5°

Specifying 10° or 15° is likely to be beneficial when speed sailing, especially in environments with cliffs, buildings, or ships.

References:

- [Veripos](https://help.veripos.com/s/article/Elevation-Mask) apply a default elevation mask of 10°
- [NovAtel](https://docs.novatel.com/OEM7/Content/Commands/ELEVATIONCUTOFF.htm) state that a satellite is considered low elevation if it is between 0 and 15° above the horizon

The online [GNSS View](https://app.qzss.go.jp/GNSSView/gnssview.html) can be used to see the effects of different mask angles.



### Proposal

Suggest the ESP GPS adds support for an elevation mask (i.e. minimum elevation), so that it can be be set to 10°.

My expectation is that it will give the M10 a helping hand, quickly discarding the lowest quality signals.