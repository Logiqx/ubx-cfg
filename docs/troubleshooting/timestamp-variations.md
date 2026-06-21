## Timestamp Variations

Sometimes timestamps are wrong by .001 seconds.

According to Google:

> Internal Processing and NCO Jitter:
>
> The timestamps are generated using a numerically controlled oscillator (NCO) running at an internal reference clock rate (64 MHz in the M10). Dividing this clock down to 10 Hz creates mathematical rounding, causing a natural jitter in the message timestamps.

This does not happen on the Motion, but it is not known whether it rounds the timestamps, or found a solution.

Perhaps it is another consequence of exceeding the CPU bandwidth in the M10, along with dropped points?