## Static ESP Testing - Technical Details

### Procedure

After each phase the data was processed as follows:

1. Download GPY + TXT from the SYRAC
2. Review TXT using shell commands (see below), and copy into the [Google Sheet](https://docs.google.com/spreadsheets/d/1Uer4QUrVxRfGNcbAIAuh3Rk3f5fuU0N5Dms0RVw1vZA/edit?usp=sharing)
3. Load GPY into [GPS Speedreader](https://github.com/prichterich/GPS-Speedreader), record the time intervals, and export as SBP
4. Generate charts from the SBP using [static_test_charts.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_charts.ipynb)
6. Generate statistics from the SBP using [static_test_stats.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_stats.ipynb)
7. Copy statistics into Excel, and produce simple summary charts

Notes:

- SBP files were used because the existing Python code does not support GPY
  - Previous studies have used UBX or OAO, and this was the first study to use GPY
- The SBP format is not ideal because of the [quantization](https://en.wikipedia.org/wiki/Quantization_(signal_processing)) errors, but still adequate
  - The intention is to add a GPY loader to the Python code for future studies



### Shell Commands

Shell commands were used to review the TXT files from the ESP GPS devices.

```sh
grep "^V" txt/* | sort
grep "Dynamic" txt/* | sort
grep "Ublox .W" txt/* | sort

grep "Ublox M" txt/* | sort
grep "GNSS" txt/* | sort
grep "Hz" txt/* | sort

grep "First fix" txt/* | sort
grep "Total time" txt/* | sort
grep "Total distance" txt/* | sort
```



### Python Code

Python code was used to generate charts and statistics.

- [static_test_charts.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_charts.ipynb) - charts showing SOG, Sats, HDOP, and sAcc
- [static_test_stats.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_stats.ipynb) - calculate mean, median, stddev, etc.

The charts are relatively simple, but still provide a useful summary of individual SBP files.



### Data

The following links will provide access to all of the spreadsheets, but not the raw data.

- [Google Sheet](https://docs.google.com/spreadsheets/d/1Uer4QUrVxRfGNcbAIAuh3Rk3f5fuU0N5Dms0RVw1vZA/edit?usp=sharing) - summary statistics from TXT files and GPS Speedreader
- [Excel Spreadsheet](https://drive.google.com/drive/folders/1gRNQ0LvkSTy7sVIzL2fw2LlLyMm03tbF?usp=sharing) - summary statistics from Python

The pages describing all of the individual tests also have links to all of the charts and statistics.



### Note to Self

Data location, should it be needed in the future!

`C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Organised\ESP-GPS\Salvador, SYRAC-GPS\2026-07-xx, SYRAC-GPS, Static Testing`
