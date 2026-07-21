## High Logging Rates

The higher logging rates of the M10 will typically require configuration relating to the clock rate(s) and baud rate.



### M10 Clock Rate

Increasing the clock rate from 128 MHz (default) to 192 MHz (higher) is described in the [MAX-M10M-00B Integration manual](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf).

>  u-blox M10 devices are optimized for low power consumption and come with the default CPU clock rate that supports the default navigation update rate stated in the product datasheet. However, it is possible to achieve a higher navigation update rate by configuring the device for a higher clock rate. This supports the high performance navigation update rate with minor increase in power consumption.

- The higher clock rate can be configured in the device's one-time programmable (OTP) memory.
- The OTP configuration is only done once, and is subsequently applied automatically at every startup.
- Changes made in the OTP configuration are permanent and CANNOT be reverted. 
- The high performance navigation update rate can be checked at run time.

The M10 may require the higher clock rate when using lots of satellites or high logging rates, otherwise dropped frames may become an issue.

The latest firmware for the Motion LCD and Motion Mini devices will automatically configure the higher clock rate for 10 Hz logging.



### Baud Rate

Higher logging rates will result in more data being sent to the UART, so it is essential the baud rate is sufficient.

The default baud rate will often be 9,600 or 38,400 baud, but use 115,200 baud should be ample for most use cases.

The exact requirements can be calculated from the UBX message sizes.



### ESP32 Clock Rate

It may also be necessary to increase the clock rate of the MCU in the ESP32:

| Clock Rate | Description                        | Suitability |
| :--------: | ---------------------------------- | :---------: |
| 80 MHz     | Lower power mode                   | up to 8 Hz  |
| 160 MHz    | Default in many Arduino frameworks | up to 16 Hz |
| 240 MHz    | Maximum performance                | 20 Hz       |



### References

#### Discussions

- [Clarify M10 max navigation update rate](https://portal.u-blox.com/s/question/0D52p0000Dgp2vpCQA/clarify-m10-max-navigation-update-rate)
  - "MCU running at 128 MHz by default, there are configurations to boost this to 192 MHz (High Performance)"
- [Unstable PVT Output Frequency on Ublox M10](https://portal.u-blox.com/s/question/0D5Oj00000dmmFwKAI/unstable-pvt-output-frequency-on-ublox-m10)
  - "On the M10 there's a method to boost the MCU clock (128 MHz to 192 MHz)"
- [Another DIY GPS logger approach](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Another-DIY-GPS-logger-approach?page=54) - veton, 22 May 2025 10:14pm
  - Tables highlight the need for M10 "high performance" mode and the ESP32 requirements

