## Static ESP Testing - ESP Suggestions

ESP GPS suggestions

- Configurable elevation mask, default to 10 degrees
  - Quick way to ignore some poor signals, and reduces the M10 workload
  - https://help.veripos.com/s/article/Elevation-Mask

- Additional items reported in .txt file
  - M10 performance mode 
  - Sats limit
  - Missing frames, which also needs to consider M10 clock drift
  - Report clock slips (e.g. 201 ms, but not the corrections such as 199 ms)

- Fix distance in TXT
  - Ideally it should match unfiltered speeds in GPS Speedreader

- CPU speed
  - The comment "For 5 Hz sample_rate, CPU freq of 80 MHz is sufficient" needs to be revised
  - "if(reset_boot==true) {setCpuFrequencyMhz(80);}"  needs to be revised

- Simplified config
  - Provide a simple 5 Hz / 10 Hz option and hide "expert" GNSS settings
  - "Expert" GNSS settings include constellations, log rate, ESP clock, max sats, and elevation mask
  - n.b. Various other non_GNSS settings may also be regarded as "expert" settings

- Fix GNSS spellings
  - GLONASS, Galileo, BeiDou

- Status screen
  - 3D fix does not tell us it is going to be accurate, also need low sAcc + hAcc
  - Suggest more info on the device - sats, HDOP, sAcc and hAcc

- Consider 12.5 Hz instead of 15 Hz?
  - 80 ms interval will repeat every 2000 ms
  - It is half of 25 Hz which is 40 ms

- SBP and GPY enhancements
  - Handling of clock drift... article to follow
  - n.b. This also makes the reporting of missing frames more straightforward

- SBP fixes
  - vsdop (vertical speed accuracy, related to climb rate) should be zero
  - SV list should be all zeros, unless determined from NAV-SAT (unnecessary)
  - SBP header

- GPX enhancement
  - Low-pass filter to ensure vmax is accurate in downstream apps

- Round results
  - I have not confirmed what it does but results should be rounded

- Asynchronous I/O, if not already implemented
  - Maybe worth considering threads with the sole aim of logging data
    - e.g. individual threads to consume UBX messages, write to SD card, and calculate stats
  - Vastly reduces the chance of dropped frames, and increases the number of file types
    - e.g. GPY + UBX