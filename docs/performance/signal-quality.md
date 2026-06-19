## Signal Quality

### Background

See Noisy Static Test - link



### Power Management

To achieve a high-performance output, you must ensure your receiver is not running in a power-save or low-power profile.

#### Operating Mode

Operating mode should be full, sometimes referred to as continuous.

https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf
- "Continuous mode" and CFG-PM-OPERATEMODE = 0 is mentioned in 3.11.3 Validity requirements

https://content.u-blox.com/sites/default/files/documents/u-blox-M10-SPG-5.20_InterfaceDescription_UBXDOC-304424225-20128.pdf

- CFG-PM-OPERATEMODE
  - Default is 2 - Power Saving Mode (PSM) cyclic tracking operation
  - Set to 0 - FULL - normal operation, no power save mode active

#### Power Mode

M8 https://content.u-blox.com/sites/default/files/products/documents/u-blox8-M8_ReceiverDescrProtSpec_UBX-13003221.pdf

- UBX-CFG-PMS (*full*, balanced [default], aggressive 1 / 2 / 4 Hz, interval)



### LNA Mode

See https://content.u-blox.com/sites/default/files/MAX-M10S_IntegrationManual_UBX-20053088.pdf for LNA info (*normal gain*, low gain [default], and bypass mode)

CFG-HW-RF_LNA_MODE

The internal LNA mode can be configured at run time in the BBR and RAM memory

DO NOT DO IT IN one-time-programmable memory (OTP)




### References

Julien:

> uBlox errata mentions issues with PMS Balanced and recommends Full. *But* on uBlox's own configuration software, PMS has disappeared and so I first thought it was removed or would have no impact. But by checking with their previous software (for M9 and earlier), it turned out that it was indeed set as PMS Balanced and still usable.

https://cdn.sparkfun.com/assets/2/0/d/7/4/u-blox_M10_ROM_5.00_ReleaseNotes_UBX-20050981.pdf

> Some devices may show poor performance with strong signals (40 dBm or better CN0) in the default “balanced” power mode. This degradation can be visible as loss of signals at the same time or reporting signals weaker than they really are.  Workaround: Change to “full power” mode (mode 0) in UBX-CFG-PMS.



