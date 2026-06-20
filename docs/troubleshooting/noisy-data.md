## Noisy Data

### Issue

- Spikes before PMS and LNA changes
  - C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Devices\Motion Mini (WSW)\test02-garden



### Cause

The [u-blox_M10_ROM_5.00_Release Notes](https://cdn.sparkfun.com/assets/2/0/d/7/4/u-blox_M10_ROM_5.00_ReleaseNotes_UBX-20050981.pdf) report poor performance with strong signals.

> Some devices may show poor performance with strong signals (40 dBm or better CN0) in the default “balanced” power mode. This degradation can be visible as loss of signals at the same time or reporting signals weaker than they really are.  Workaround: Change to “full power” mode (mode 0) in UBX-CFG-PMS.

The different power modes on the M8 didn't make any difference in testing, so Motion originally went with the default of "balanced".

The official M10 documentation and software do not contain `UBX-CFG-PMS` , but it is still available.



### Solution

The "full power" mode and "normal gain" for the internal LNA produced static results similar to the M8. Aside from removing the low speed spikes, it also brought sAcc + HDOP to the values expected on an M8.

It was speculated that "balanced" power mode was polluting the inner RF path with noise, due to sleep / wake spikes. There are some other power management systems available, and they have a "limit inrush current on wake" configuration field.

Bypassing the internal LNA may increase the battery life of the Motion Mini by an hour or so, but this was never investigated. The "full power" mode and "normal gain" for the internal LNA have been standard in the Motion Mini since firmware 3168.

Further details about the different power modes and internal LNA can be found in the [signal quality](../performance/signal-quality.md) page.


