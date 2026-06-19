## Timestamp Variations

- Internal Processing and NCO Jitter: The timestamps are generated using a numerically controlled oscillator (NCO) running at an internal reference clock rate (64 MHz in the M10). Dividing this clock down to 10 Hz creates mathematical rounding, causing a natural jitter in the message timestamps.