## Static ESP Testing - Key Findings

### Data Collection

- The tests produced over 400 hours worth of data for analysis
- TXT files were useful for confirming the actual configuration (especially S3), and summary statistics
  - Distances in TXT files are incorrect, so calculating mean speeds from the TXT can be misleading
- GPY files were recorded instead of UBX, but GPY is not supported by the existing Python code
  - GPY files were converted to SBP using GPS Speedreader, but it does incur quantization errors




### Optimal Configuration

- Galileo is better than GLONASS
  - The latter test phases (4 onwards) ignored GLONASS entirely
- 5 Hz is better than 10 Hz
  - Max of 28 satellites is the optimal setting for 5 Hz (and 10 Hz)



### Sampling Rates

Quick summary:

- 20 Hz has limited usefulness in comparison to 10 Hz
  - Best 20 Hz mean SOG was 0.05656 (D2 in test 1) and 0.05806 (D2 in test 2)
  - 30 sats -> 20 sats means HDOP goes from ~0.4 to ~0.6 (50% increase)
  - The increase in HDOP cancels the sqrt(2) benefits relative to 10 Hz
- 15 Hz also may need to be limited to 20 sats
  - Best 15 Hz mean SOG was 0.05014 (D2 in test 3) and 0.05269 (D5 in test 2)
  - Unclear whether it is beneficial over 10 Hz
  - The 15 Hz timestamps are rather ugly
- 10 Hz may not be any more useful than it is on the Motion
  - Best 10 Hz mean SOG was 0.04277 (SY2 in test 1) and 0.04345 (D3 in test 6)
  - The latter phases of testing all demonstrated that 5 Hz was better than 10 Hz
- 5 Hz was confirmed to be the most accurate during these tests
  - Best 5 Hz mean speed was 0.02077 (D2 in test 5) and 0.02097 (D1 in test 6)
  - Gaussian error propagation suggests that to improve on 5 Hz performance...
    - 10 Hz would need to be <= 0.030, but was 0.043
    - 15 Hz would need to be <= 0.036, but was 0.050
    - 20 Hz would need to be <= 0.042, but was 0.057
  



### Speed Accuracy (sAcc)

Need to write up the sAcc issues apparent in test 7 and test 4

- The sAcc in 10 Hz data claims it to be more accurate than 5 Hz, which is untrue



### Previous Testing

Previous results for the Motion:

- 2 Hz was most "accurate", but only beat 5 Hz by a tiny margin
- 5 Hz does not suffer from nearly so much aliasing, so it is the better choice

