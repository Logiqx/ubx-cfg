## Dropped Points

When the M10 is using multiple active satellite constellations, the CPU can experience temporary processing bottlenecks. During heavy workloads the receiver might drop a PVT solution immediately after the top-of-second epoch.

Dropped points may be be resolved by configuration changes, generally relating to the clock rate(s), and maybe the baud rate. If the clock rates of the M10 and ESP32 have already been increased sufficiently, then too many satellites are being tracked and need to be limited.

Full details about increasing the clock rates of the M10 and ESP32 are available on the page that talks about [High Logging Rates](../performance/high-rates.md).


