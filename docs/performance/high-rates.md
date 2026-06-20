## High Logging Rates

### M10 High Performance Mode

Dependent on log rate rate, constellations in use, number of satellites

High-Performance Mode - see integration manual

[MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf) - 5-May-2026

>  u-blox M10 devices are optimized for low power consumption and come with the default CPU clock rate that supports the default navigation update rate stated in the product datasheet. However, it is possible to achieve a higher navigation update rate by configuring the device for a higher clock rate. This supports the high performance navigation update rate with minor increase in power consumption.

"High CPU clock" is described in 2.1.7 of the integration manual - "High performance navigation update rate configuration"
- Changes made in the OTP configuration are permanent and cannot be reverted.
  - The high performance navigation update rate can be configured in the device's one-time programmable (OTP) memory.
  - The OTP configuration is only done once, and is subsequently applied automatically at every startup.
  - Changes made in the OTP configuration are permanent and cannot be reverted.  
  - Can be checked at run time as described in step 5
- Capping the number of sats makes sense for people with lots of sats visible (e.g. BeiDou in Asia)

https://portal.u-blox.com/s/question/0D52p0000Dgp2vpCQA/clarify-m10-max-navigation-update-rate
MCU running at 128 MHz by default, there are configurations to boost this to 192 MHz (High Performance)

https://portal.u-blox.com/s/question/0D5Oj00000dmmFwKAI/unstable-pvt-output-frequency-on-ublox-m10
On the M10 there's a method to boost the MCU clock (128 MHz to 192 MHz)

https://content.u-blox.com/sites/default/files/MAX-M10_ProductSummary_UBX-20017987.pdf
The extremely low power consumption of less than 25 mW* in continuous tracking mode ...

USE - case is avoiding dropped points, typically at the top of the epoch - between .000 and .200



### Baud Rate

Higher rate needed for higher frequency data

115,200



### ESP32 Maximum Performance

ESP32 CPU Speed

- 240 MHz (Maximum performance) - needed for 20 Hz
- 160 MHz (Default in many Arduino frameworks) - needed for 10 Hz
- 80 MHz (Lower power mode) - up to 8 Hz
