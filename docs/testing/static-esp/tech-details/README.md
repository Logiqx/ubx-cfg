## Static ESP Testing - Technical Details

### Procedure

After each phase the data was consumed using the following process:

1. Download GPY + TXT files
2. Review TXT files using shell commands, and update the [Google Sheet](https://docs.google.com/spreadsheets/d/1Uer4QUrVxRfGNcbAIAuh3Rk3f5fuU0N5Dms0RVw1vZA/edit?usp=sharing)
3. Load GPY files into [GPS Speedreader](https://github.com/prichterich/GPS-Speedreader), record time intervals in the Google Sheet, and export as SBP
4. Convert SBP files to CSV using [batch_convert.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/batch_convert.ipynb)
5. Generate + review charts using [static_test_charts.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_charts.ipynb)
6. Generate + review stats using [static_test_stats.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_stats.ipynb)
7. Copy stats into Excel and produce summary charts



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

- [batch_convert.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/batch_convert.ipynb)
- [static_test_charts.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_charts.ipynb)
- [static_test_stats.ipynb](https://github.com/Logiqx/gps-wizard/blob/main/python/adhoc/static_test_stats.ipynb)

The charts are relatively crude but provided a useful summary of each session. Possible improvements:

- Standard y-axis
- Summarise configurations in the titles (i.e. via lookup)



### Data

The following links will provide access to all of the outputs (e.g. statistics and charts), but not the raw data.

- [Google Sheets](https://docs.google.com/spreadsheets/d/1Uer4QUrVxRfGNcbAIAuh3Rk3f5fuU0N5Dms0RVw1vZA/edit?usp=sharing)
- [Google Drive](https://drive.google.com/drive/folders/1gRNQ0LvkSTy7sVIzL2fw2LlLyMm03tbF?usp=sharing)



### Note to Self

Data location, should it be needed in the future!

`C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Organised\ESP-GPS\Salvador, SYRAC-GPS\2026-07-xx, SYRAC-GPS, Static Testing`
