## Static ESP Testing - Key Findings

Over 400 hours of test data

- TXT files are useful
  - but the distances are incorrect and cannot use them to calculate mean speed (see 20 Hz files in test 1)

- Galileo is better than GLONASS
  - GPS + Galileo ~ 0.020 m/s
  - GPS + GLONASS ~ 0.025 m/s
  - Tests 4 onwards ignore GLONASS entirely

- 28 sats is the optimal setting for 5 Hz and 10 Hz
- 20 Hz has limited usefulness in comparison to 10 Hz
  - Best 20 Hz mean SOG was 0.05656 (D2 in test 1) and 0.05806 (D2 in test 2)
  - Maybe a 5% improvement in accuracy, but doubles the file size and uses more power
    - 30 sats -> 20 sats means HDOP goes from 0.4 to 0.6 (50% increase), cancelling most of the sqrt(2) benefits relative to 10 Hz
- 15 Hz may need to be limited to 20 sats
  - Best 15 Hz mean SOG was 0.05014 (D2 in test 3) and 0.05269 (D5 in test 2)
  - Unclear whether it is beneficial over 10 Hz
  - The 15 Hz timestamps are rather ugly
- 10 Hz may not be any more useful than it is on the Motion
  - Best 10 Hz mean SOG was 0.04277 (SY2 in test 1) and 0.04345 (D3 in test 6)
  - A single 10 Hz device amongst 5 Hz devices performed a lot worse in terms of accuracy
- 5 Hz is best
  - Best 5 Hz mean speed was 0.02077 (D2 in test 5) and 0.02097 (D1 in test 6)
  - To improve on 0.021 would need 0.030 (10 Hz was 0.043), 0.036 (15 Hz was .050), 0.042 (20 Hz was .057)
- Previous Motion tests
  - 2 Hz was most "accurate", but only beat 5 Hz by a tiny margin
  - 5 Hz does not suffer from nearly so much aliasing, so it is the better choice

- Need to write up the sAcc issues apparent in test 7 and test 4
  - 10 Hz claimed to be more accurate but it is not