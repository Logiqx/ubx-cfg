## Dropped Points

- Processor Workload and Saturation: When the u-blox M10 is running at 10 Hz with multiple active satellite constellations, the MCU can experience temporary processing bottlenecks. During heavy workloads (e.g., tracking many satellites), the receiver might drop a solution immediately after the top-of-second epoch, pushing the timestamp to the next measurement cycle.
- Due to number of satellites being tracked, perhaps too many constellations
- Typically at top of epoch between .000 and 0.200
- May need [High-Performance Mode](performance/high-performance.md) - see UBX specs
- May also need increased baud rate and / or higher ESP32 CPU speed