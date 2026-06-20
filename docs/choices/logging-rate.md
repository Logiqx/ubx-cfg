## Logging Rate

- 10 Hz is twice as accurate as 5 Hz, right?
  - Not necessarily... 10 Hz may be worse than 5 Hz
  - C:\Users\mwgeo\OneDrive\Documents\GPS Files\Testing\2024\2024-06-18, Frequency Test - Garden 1
    - 10 Hz worse than 5 due to 2 systems and lower HDOP
    - sAcc is lying and so is +/-
- 20 Hz may not offer any benefits
  - Only 2 systems, so comparable to 5 Hz vs 10 Hz observations
    - 20 Hz with 2 systems may be no better than 5 Hz with 3 or 4 systems
    - Just requiring more compute power and 4 times the storage
- Supported through `CFG-RATE-*` keys
- Dependencies
  - [High-Performance Mode](performance/high-performance.md)
  - Baud rate
  - ESP32 CPU speed
- Troubleshooting - dropped points



### 1 Hz

Possibilities

•	CFG-RATE-MEAS = 100 and CFG-RATE-NAV = 10
•	CFG-RATE-MEAS = 200 and CFG-RATE-NAV = 5
•	CFG-RATE-MEAS = 500 and CFG-RATE-NAV = 2
•	CFG-RATE-MEAS = 1000 and CFG-RATE-NAV = 1

n.b. CFG-RATE-TIMEREF probably irrelevant (defaults to GPS) because GPS and UTC share milliseconds

Julien

CFG-RATE-MEAS = 1000

I always assumed that people interested in lower output rates than 5/10Hz would need it for the extended battery life so never tried a (5Hz update rate with 1Hz output rate) or similar.

IIRC to use uBlox's own LPF, you need to compute the resultant vector of the North and East velocity fields instead of using the ground speed field.



### Odd Rates

6 Hz - 1000 / 150

15 Hz = 1000 / 66



### Dependencies

Possible dependencies:

MCU speed



### Considerations

If you increase the update rate, you must also increase the baud rate (data transmission speed) of your serial connection to the chip (e.g., from 9600 to 115200) to avoid data bottlenecks

