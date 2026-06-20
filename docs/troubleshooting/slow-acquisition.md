## Slow Acquisition

If your module turns off and loses power completely, it performs a cold start every time. By connecting a battery or a supercapacitor to the \(V_{BCKP}\) pin, the M10 maintains last-known position, time, and almanac data. This drops subsequent fix times to just a few seconds (hot start).

It is very noticeable how much quicker the Motion acquires its satellites in comparison to the Motion, especially after a hard reset. This makes me wonder which Beitian module is inside the LISA and whether it has onboard flash memory like the BE-182.