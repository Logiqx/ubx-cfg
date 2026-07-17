## Static ESP Testing - Test Approach

The duration of the tests is because the number of visible satellites changes quite over time. This image shows S3 during test 6 (GPS + Galileo) and it varied between 12 and 20. When comparing different configurations (especially different constellations) the ideal is to use 12 or 24 hours to get results for one complete orbit (12 hours) or two orbits (night and day). I chose 6 hours for these tests as we don't have time to do the full 12 hours. 6 hours is also enough to pick up issues such as dropped frames, which may be missed if the test was just a couple of hours. Having identified the required CPU speed (160 MHz, even for 5 Hz), I think we now have settings which almost eliminate dropped frames. The optimal performance for GGB at 5 Hz and 10 Hz was 28 sats, confirmed during the last 3 tests.



### Missing Points

Dropped frames... BLAH
