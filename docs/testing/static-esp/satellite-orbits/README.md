## Static ESP Testing - Satellite Orbits

The page describing the [test approach](../test-approach/README.md) described orbital periods, so that will not be repeated on this page.

Two additional topics may be worth considering:
- BeiDou has 3 x IGSO and 5 x GEO satellites in addition to the MEO satellites
  - This equates to an additional 8 visible satellites in the Asia region
  - The additional satellites WILL be tracked by the M10, and increase its workload
  - Tracking the signals is not costly, but the M10 must evaluate them for the NAV solution
  - Limiting "max sats" only limits how may signals are used for the actual NAV solution
- GLONASS inclination angle = 64.8° instead of 55° or 56°
  - It may be actually be good for high latitudes, perhaps above 50°

Propose also testing GLONASS at higher latitudes (e.g. Norway, Sweden, or Finland).



### Inclination Angles

A couple of links...

- [GEOG862 - Global Navigation Satellite Systems and the Future](https://courses.ems.psu.edu/geog862/l10.html)

  - Inclination of GPS = 55°, BeiDou = 55°, Galileo = 56°, GLONASS = 64.8°
    - See image at top of [Innovation: GPS, GLONASS and More](https://www.gpsworld.com/innovation-gps-glonass-and-more/)

  - Orbital planes of GPS = 6, BeiDou (MEO) = 3, Galileo = 3, GLONASS = 3
    - Additional orbital planes for BeiDou - 2 x IGSO and 1 x GEO


- [GPS vs GLONASS vs Galileo vs BeiDou](https://orbitalradar.com/navigation-constellations)
  - "GLONASS has the highest orbital inclination (64.8°) of any GNSS, giving it superior satellite visibility at latitudes above 55°N."
  - "This makes GLONASS particularly valuable in Scandinavia, Russia, Canada, and Alaska where GPS geometry alone can be weaker."

