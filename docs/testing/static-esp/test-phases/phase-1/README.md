## Static ESP Testing - Phase 1

### Overview

GLONASS vs Galileo



### Conclusions



### Configuration

| ID   | Constellations          | Rate  | Max Sats | ESP     | Baud    |
| :--: | ----------------------- | :---: | :------: | :-----: | ------: |
| SY1  | GPS + GLONASS           | 10 Hz | 32       | 160 MHz | 38,400  |
| SY2  | GPS + Galileo           | 10 Hz | 32       | 160 MHz | 38,400  |
| D3   | GPS + GLONASS           | 15 Hz | 32       | 240 MHz | 115,200 |
| D1   | GPS + Galileo           | 15 Hz | 32       | 240 MHz | 115,200 |
| D5   | GPS + GLONASS           | 20 Hz | 32       | 240 MHz | 115,200 |
| D2   | GPS + Galileo           | 20 Hz | 32       | 240 MHz | 115,200 |
| S3   | GPS + Galileo + GLONASS | 10 Hz | 32       | 160 MHz | 38,400  |



### Charts

BLAH

![sog-mean-1.png](img/sog-mean-1.png)

BLAH

![sog-mean-2.png](img/sog-mean-2.png)

BLAH

![sog-mean-3.png](img/sog-mean-3.png)

BLAH

![sog-median.png](img/sog-median.png)

BLAH

![sog-stddev.png](img/sog-stddev.png)



### Results

- TTFF was quite variable... will assume some devices were a cold start
- Warm up periods need deleting... remove 30 mins and show the effects in GPS Speedreader
- No evidence of M10 "balanced" power mode issues in SOG
- Overall GLONASS performed worst, Galileo performed best
  - GPS + Galileo > GPS + Galileo + GLONASS > GPS + GLONASS @ 10 Hz
  - GPS + Galileo > GPS + GLONASS @ 15 Hz
  - GPS + Galileo > GPS + GLONASS @ 20 Hz
  - GPS + Galileo ~ 0.020 m/s
  - GPS + GLONASS ~ 0.025 m/s
- HDOP doesn't really improve much after 20 sats
  - S3 has scatter plot
- Oddly 10 Hz tests slightly outperformed the 15 Hz and 20 Hz ones
  - S3 might be misleading though as it shows a lot of clock adjustments
  - Phase 2 testing to confirm!
- Odd time intervals due to clock drift, except 15 Hz which is just weird
- Dropped frames @ 20 Hz... slightly more for GLONASS (11) vs Galileo (4)
- Thought... multiply actual sats by log rate for sats / sec
