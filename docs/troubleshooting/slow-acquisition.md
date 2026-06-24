## Slow Acquisition

It is very noticeable how much quicker the Motion acquires its satellites in comparison to the LISA, especially after a hard reset. This makes me wonder which Beitian module is inside the LISA and whether it has onboard flash memory like the BE-182.

Possibly related...

>  If your module turns off and loses power completely, it performs a cold start every time. By connecting a battery or a supercapacitor to the \(V_{BCKP}\) pin, the M10 maintains last-known position, time, and almanac data. This drops subsequent fix times to just a few seconds (hot start).

Something else that may be relevant is AssistNow Autonomous. The AssistNow Autonomous feature runs locally on the receiver and generates mid and long term predicted orbits without an internet connection. The orbit prediction is based on broadcast ephemerides.

The AssistNow Autonomous feature provides a functionality similar to AssistNow Predictive Orbits without the need for a host and a connection. Based on a broadcast ephemeris downloaded from the satellite (or obtained by AssistNow Live Orbits), the receiver can autonomously (i.e. without any host interaction or online connection) generate an accurate satellite orbit representation ("AssistNow Autonomous data") that is usable for navigation much longer than the underlying broadcast ephemeris was intended for. This makes downloading new ephemeris or aiding data for the first fix unnecessary for subsequent startups of the receiver.

Related commands:

- `CFG-ANA-USE_ANA` where the default is 1 (true)
- `UBX-MGA-FLASH-DATA` can be used to transfer MGA-ANO ( AssistNow Offline) data block to flash
- `UBX-MGA-FLASH-STOP` is used to finish flashing MGA-ANO data
- `UBX-MGA-FLASH-ACK` will acknowledge the last FLASH-DATA or -STOP

See the MAX-M10M [integration guide](https://content.u-blox.com/sites/default/files/documents/MAX-M10M-00B_IntegrationManual_UBX-22038241.pdf) for further details about AssistNow Autonomous.
