## Static ESP Testing - Power Mode

### Background

The [u-blox_M10_ROM_5.00_Release Notes](https://cdn.sparkfun.com/assets/2/0/d/7/4/u-blox_M10_ROM_5.00_ReleaseNotes_UBX-20050981.pdf) report poor performance with strong signals.

> Some devices may show poor performance with strong signals (40 dBm or better CN0) in the default "balanced" power mode. This degradation can be visible as loss of signals at the same time or reporting signals weaker than they really are.  Workaround: Change to "full power" mode (mode 0) in UBX-CFG-PMS.

The different power modes on the M8 didn't make any difference in testing, so the Motion went with the default.

M10 devices may need to use `UBX-CFG-PMS` to select "full power", instead of the default "balanced" power mode.

n.b. The official M10 documentation and software do not contain `UBX-CFG-PMS` , but it is still available.

See section 13.7 in the [u-blox M8 Receiver Description](https://content.u-blox.com/sites/default/files/products/documents/u-blox8-M8_ReceiverDescrProtSpec_UBX-13003221.pdf) for more details.



### SY2

Throughout these tests, SY2 exhibited problems reminiscent of an issue that affected some early Motion Mini using the M10. This was resolved by selecting "full power", instead of the default "balanced" power mode.

Suggest the ESP GPS has a "power mode" option added so that "full power" or "balanced" (default) can be selected. It will then be possible to test "full power" mode on SY2, and any other devices that have a similar afflication.