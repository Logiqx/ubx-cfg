## Motion GPS

### Background

The [Motion GPS](https://www.motion-gps.com/motion/) has been one of the most popular devices within the speed sailing community:

- The Motion LCD had either 4 or 5 buttons
- The Motion Mini had one button and a light

Inside both devices there is a custom PCB, which includes a u-blox GNSS chip, filters, amplifier, and oscillator. This is somewhat different to the ESP-GPS design, which uses an all-in-1 GPS module from Beitian. GPS modules are a self-contained package including the GNSS chip, antenna, filters, amplifier, and oscillator. The GNSS oscillator was upgraded when the Motion Mini was re-designed (double-strap), and mentioned in the release notes of [firmware](https://www.motion-gps.com/motion/changelog.html#3231) 3231. The earlier Motion LCD and Motion Mini devices shipped with the u-blox M8, but were subsequently upgraded to the M10.



### M8 Devices

The [UBX-M8030-KT](https://www.u-blox.com/en/product/ubx-m8030-series) was used by the original Motions, u-blox GNSS modules such as the MAX M8, and Beitian [BN250](https://www.youtube.com/watch?v=NGotetkXIZc).

The [NEO-M8](https://content.u-blox.com/sites/default/files/NEO-M8-FW3_DataSheet_UBX-15031086.pdf) datasheet shows the different levels of performance for the M8:

| Constellations / Services                   | NEO-M8N | NEO-M8Q |
| ------------------------------------------- | :-----: | :-----: |
| GPS / GLONASS / BDS B1I / Galileo / BDS B1C |  10 Hz  |  18 Hz  |
| GPS + GLONASS (default)                     |  5 Hz   |  10 Hz  |

These figures are all on the basis of a minimum 98% fix rate under typical conditions, not 100%.

The original Motions (M8) supported logging rates of 1, 2, 5, and 10 Hz:

- GPS + GLONASS + Galileo - up to 5 Hz, limited to 24 satellites
- GPS + GLONASS (perhaps Galileo) - up to 10 Hz, limited to 18 satellites



### M10 Devices

The [UBX-M10050-KB](https://www.u-blox.com/en/product/ubx-m10-series) was used by the newer Motions, u-blox GNSS modules such as the MAX M10, and Beitian [BE250](https://www.beitian.com/en/sys-pd/520.html).

It is worth noting that the MAX-M10 performance closely matches the [MAX-M8](https://content.u-blox.com/sites/default/files/documents/MAX-M8-FW3_DataSheet_UBX-15031506.pdf):

- High performance mode of the MAX-M10 has the same max navigation rates of the MAX-M8
- The MAX-M10 has the identical Time-To-First-Fix (TTFF) to the MAX-M8 for the various constellations

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

The newer Motions (M10) support the same logging rates as the earlier models - 1, 2, 5, and 10 Hz:

- GPS + GLONASS + Galileo up to 5 Hz - limited to 24 satellites
- GPS + GLONASS (perhaps Galileo) up to 10 Hz - limited to 18 satellites

The M10 configuration:

- [Full power](signal-quality.md) mode is used instead of the default "balanced" power mode
- [High performance](high-rates.md) mode is only enabled when 10 Hz logging is configured, and CANNOT be reverted

It is interesting to note that 5 Hz logging is more accurate than 10 Hz logging, demonstrated during [Static Testing](../testing/static-5hz-10hz.md).



### Hardware Details

- Custom PCB
  - The Expressif logo is clearly visible on one of the chips
  - The battery, charge coil, controller, and shielding are visible
    - See [photo](https://www.seabreeze.com.au/img/photos/windsurfing/23053891.jpg) of PBC in Seabreeze [thread](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Mini-Motion-Battery-Replacement-Installed)
- GNSS chip
  -  [UBX-M8030-KT](https://www.u-blox.com/en/product/ubx-m8030-series) (40 pin QFN chip)
  - [UBX-M10050-KB](https://www.u-blox.com/en/product/ubx-m10-series) (28 pin QFN chip)

- GNSS oscillator clearly has an impact on performance
  - See [NEO-M8](https://content.u-blox.com/sites/default/files/NEO-M8-FW3_DataSheet_UBX-15031086.pdf) datasheet and [MAX-M8](https://content.u-blox.com/sites/default/files/documents/MAX-M8-FW3_DataSheet_UBX-15031506.pdf) datasheets
- Antenna
  - Cirocom [PA025KQ0002](https://www.cirocomm.com/en-global/products_ciro/detail/PA025KQ0002) 25\*25\*2 mm GPS + GLONASS patch antenna
    - See [photo](https://www.seabreeze.com.au/img/photos/windsurfing/21752270.jpg) of antenna in Seabreeze [thread](https://www.seabreeze.com.au/forums/Windsurfing/Gps/Mini-Motion-repaired)
- Comparable Beitian GNSS modules
  - UBX-M8030 - Beitian [BN250](https://www.youtube.com/watch?v=NGotetkXIZc)
  - UBX-M10050 - Beitian [BE250](https://www.beitian.com/en/sys-pd/520.html)

- LCDs and Minis have Wi-Fi
  - Only the LCDs have longer range radio



### References

Julien in 2022:

> I use the flagship M8030 and add my own filters, amplifier, and oscillator because it's much better bang for the bucks. All M8 products derive from it or from its die. Achieving the specifications uBlox datasheets boast require better components than what their modules provide, except maybe for the timing series. I also give all these the energy they need.

Articles:

- [Patch Antenna PCB Design: Complete Guide with Calculations, Layout & Feeding Methods](https://pcbsync.com/patch-antenna-pcb/) - PCBSync
- [GNSS antennas - RF design considerations for u-blox GNSS receivers](https://content.u-blox.com/sites/default/files/products/documents/GNSS-Antennas_AppNote_%28UBX-15030289%29.pdf) - u-blox, 16 Oct 2019

