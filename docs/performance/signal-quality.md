## Signal Quality

### Background

Power saving and low-noise amplifier (LNA) modes were central to an investigation into [noisy data](../troubleshooting/noisy-data.md) from M10 devices.

Some M10 devices will benefit from the "full power" mode, instead of the default "balanced" mode.



### Power Saving

#### Power Mode

The [u-blox_M10_ROM_5.00_Release Notes](https://cdn.sparkfun.com/assets/2/0/d/7/4/u-blox_M10_ROM_5.00_ReleaseNotes_UBX-20050981.pdf) report poor performance with strong signals.

> Some devices may show poor performance with strong signals (40 dBm or better CN0) in the default “balanced” power mode. This degradation can be visible as loss of signals at the same time or reporting signals weaker than they really are.  Workaround: Change to “full power” mode (mode 0) in UBX-CFG-PMS.

The different power modes on the M8 didn't make any difference in testing, so the Motion went with the default.

M10 devices may need to use `UBX-CFG-PMS` to select "full power", instead of the default "balanced" power mode.

n.b. The official M10 documentation and software do not contain `UBX-CFG-PMS` , but it is still available.

See section 13.7 in the [u-blox M8 Receiver Description](https://content.u-blox.com/sites/default/files/products/documents/u-blox8-M8_ReceiverDescrProtSpec_UBX-13003221.pdf) for more details.



#### Operating Mode

Power management in the M10 supports three operating modes / power save modes:

- 0 = Full (normal operation, no power save mode active)
- 1 = PSMOO (PSM ON/OFF operation)
- 2 = PSMCT (PSM cyclic tracking operation)

The operating mode can be changed using `CFG-PM-OPERATEMODE`, but the default is already "full".

n.b. The "full" operating mode is referred to as "continuous mode" in MAX-M10 integration manual.

See [u-blox M10 SPG 5.30 Interface description](https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.30_InterfaceDescription_UBXDOC-304424225-20395.pdf) and [MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf) for more details.

#### 

### LNA Mode

M10 receivers feature an internal low-noise amplifier (LNA) with three operational modes:

- 0 = Normal gain
- 1 = Low gain
- 2 = Bypass

This can be changed using `CFG-HW-RF_LNA_MODE`, but the default is already "normal gain".

Early prototypes of the Motion Mini using UBX-M10050-KB experimented with the "bypass" mode, but reverted to "normal gain".

The internal LNA can't be configured on the M8 or M9, because `CFG-HW-RF_LNA_MODE` was introduced in the M10.

See [u-blox M10 SPG 5.30 Interface description](https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.30_InterfaceDescription_UBXDOC-304424225-20395.pdf) and [MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf) for more details.



### History

Julien during the PMS investigation:

> uBlox errata mentions issues with PMS Balanced and recommends Full. *But* on uBlox's own configuration software, PMS has disappeared and so I first thought it was removed or would have no impact. But by checking with their previous software (for M9 and earlier), it turned out that it was indeed set as PMS Balanced and still usable.

The "full power" mode and "normal gain" internal LNA mode produced static results similar to the M8. Aside from removing the low speed spikes, it also brought sAcc + HDOP to the values expected on an M8.

It was speculated that "balanced" power mode was polluting the inner RF path with noise, due to sleep / wake spikes. There are more power management systems available and they have a "limit inrush current on wake" configuration field.

