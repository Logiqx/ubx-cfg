## Motion GPS

### Background

The [Motion GPS](https://www.motion-gps.com/motion/) is one of the most popular devices within the speed sailing community, but no longer produced:

- The Motion LCD had a colourful screen and typically had 5 buttons
- The Motion Mini had one button and a light to show the status

Inside both devices there is a custom PCB, which includes a u-blox GNSS chip, filters, amplifier, and oscillator. This is different to the ESP-GPS design, which uses a Beitian GNSS module. GNSS modules are packages containing the GNSS chip, antenna, filters, amplifier, and oscillator.

It is worth mentioning that the GNSS oscillator can have a significant impact on accuracy, and it was upgraded when the Motion Mini was re-designed in 2024. The earlier Motion LCD and Motion Mini devices shipped with the u-blox M8, but were subsequently upgraded to the M10.



### M8 Devices

The [UBX-M8030-KT](https://www.u-blox.com/en/product/ubx-m8030-series) was used by the original Motions, and GNSS modules such as the u-blox MAX M8 + Beitian [BN250](https://www.youtube.com/watch?v=NGotetkXIZc).

The [NEO-M8](https://content.u-blox.com/sites/default/files/NEO-M8-FW3_DataSheet_UBX-15031086.pdf) datasheet shows the following max navigation update rates, specific to each module:

| Constellations / Services                   | NEO-M8N | NEO-M8Q |
| ------------------------------------------- | :-----: | :-----: |
| GPS / GLONASS / BDS B1I / Galileo / BDS B1C |  10 Hz  |  18 Hz  |
| GPS + GLONASS (default)                     |  5 Hz   |  10 Hz  |

These figures are all on the basis of a minimum 98% fix rate under typical conditions, not 100%.

The original Motions (M8) supported logging rates of 1, 2, 5, and 10 Hz:

- GPS + GLONASS + Galileo for up to 5 Hz, limited to 24 satellites
- GPS + GLONASS (perhaps Galileo) for 10 Hz, limited to 18 satellites

The M8 itself limited the Motion to just 2 systems when logging at 10Hz, just like the NEO-M8Q.

GPS + GLONASS was likely to used for 10 Hz, since that combination was the default for the M8.

The number of satellites was probably limited to avoid [Dropped Frames](../troubleshooting/dropped-frames.md), and maybe to conserve battery.



### M10 Devices

The [UBX-M10050-KB](https://www.u-blox.com/en/product/ubx-m10-series) was used by the newer Motions, and GNSS modules such as the u-blox MAX M10 + Beitian [BE250](https://www.beitian.com/en/sys-pd/520.html).

It is worth noting that the MAX-M10 performance looks very similar to the [MAX-M8](https://content.u-blox.com/sites/default/files/documents/MAX-M8-FW3_DataSheet_UBX-15031506.pdf), but it is nothing like the M9:

- Default performance of the MAX-M10 has the max navigation rates of the MAX-M8
- The MAX-M10 has identical Time-To-First-Fix (TTFF) specifications as the MAX-M8

The [MAX-M10](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_DataSheet_UBX-22028884.pdf) datasheet shows the following max navigation update rates:

| Constellations / Services                   | Default Performance | High Performance |
| ------------------------------------------- | :-----------------: | :--------------: |
| GPS / GLONASS / BDS B1I / Galileo / BDS B1C |        18 Hz        |      25 Hz       |
| GPS + Galileo (default)                     |        10 Hz        |      20 Hz       |
| GPS + Galileo + BeiDou B1C                  |        8 Hz         |      16 Hz       |
| GPS + Galileo + GLONASS                     |        6 Hz         |      16 Hz       |
| GPS + Galileo + BeiDou B1I                  |        3 Hz         |      12 Hz       |
| GPS + Galileo + BeiDou B1C + GLONASS        |        4 Hz         |      10 Hz       |

These figures are all on the basis of a minimum 98% fix rate under typical conditions, not 100%.

The newer Motions (M10) support logging rates of 1, 2, 5, and 10 Hz:

- GPS + GLONASS + Galileo for up to 5 Hz - limited to 24 satellites
- GPS + GLONASS (perhaps Galileo) for 10 Hz - limited to 18 satellites

These rates are the same as the M8 devices, but the M10 required some additional configuration:

- [Full power](signal-quality.md) mode instead of the default "balanced" power mode of the M10
- [High performance](high-rates.md) mode for 10 Hz logging, which CANNOT be reverted to the default

Final thoughts:

- It is interesting to note that 5 Hz logging is more accurate than 10 Hz logging on the M10 devices, demonstrated during [Static Testing](../testing/static-5hz-10hz.md)
- The accuracy of the M10 devices improved when the Motion Mini was [re-designed](https://www.motion-gps.com/motion/changelog.html#3231), possibly due to the upgraded GNSS oscillator
- High performance mode was enabled for 10 Hz logging in the last firmware release in late 2024



### Hardware Details

- Custom PCB
  - The Expressif logo is clearly visible on one of the chips, perhaps the MCU
  - The battery, charge coil, controller, and shielding are also visible
    - See [photo](https://www.seabreeze.com.au/img/photos/windsurfing/23053891.jpg) of PBC in Seabreeze [thread](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Mini-Motion-Battery-Replacement-Installed)
- GNSS chip, not a GNSS module
  -  [UBX-M8030-KT](https://www.u-blox.com/en/product/ubx-m8030-series) (40 pin QFN chip)
  - [UBX-M10050-KB](https://www.u-blox.com/en/product/ubx-m10-series) (28 pin QFN chip)
- GNSS filters
  - No details available

- Lower Noise Amplifier (LNA)
  - No details available

- GNSS oscillator
  - [NEO-M8](https://content.u-blox.com/sites/default/files/NEO-M8-FW3_DataSheet_UBX-15031086.pdf) and [MAX-M8](https://content.u-blox.com/sites/default/files/documents/MAX-M8-FW3_DataSheet_UBX-15031506.pdf) datasheets distinguish between crystal and [TCXO](https://www.microchip.com/en-us/products/clock-and-timing/components/oscillators/tcxo)
  - GNSS oscillator was upgraded when the Motion Mini hardware was [improved](https://www.motion-gps.com/motion/changelog.html#3231)
  - Devices with the upgraded oscillator benefit from improved performance
- Antenna
  - Cirocom [PA025KQ0002](https://www.cirocomm.com/en-global/products_ciro/detail/PA025KQ0002) 25\*25\*2 mm GPS + GLONASS patch antenna
    - See [photo](https://www.seabreeze.com.au/img/photos/windsurfing/21752270.jpg) of antenna in Seabreeze [thread](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Mini-Motion-repaired)
- Beitian GNSS modules - M8 and M10
  - Beitian [BN250](https://www.youtube.com/watch?v=NGotetkXIZc) contains UBX-M8030
  - Beitian [BE250](https://www.beitian.com/en/sys-pd/520.html) contains UBX-M10050
- LCDs and Minis both support Wi-Fi
  - Only the LCDs have support for longer range radio



### References

Julien in 2022:

> I use the flagship M8030 and add my own filters, amplifier, and oscillator because it's much better bang for the bucks. All M8 products derive from it or from its die. Achieving the specifications uBlox datasheets boast require better components than what their modules provide, except maybe for the timing series. I also give all these the energy they need.

Articles:

- [Patch Antenna PCB Design: Complete Guide with Calculations, Layout & Feeding Methods](https://pcbsync.com/patch-antenna-pcb/) - PCBSync
- [GNSS antennas - RF design considerations for u-blox GNSS receivers](https://content.u-blox.com/sites/default/files/products/documents/GNSS-Antennas_AppNote_%28UBX-15030289%29.pdf) - u-blox, 16 Oct 2019

