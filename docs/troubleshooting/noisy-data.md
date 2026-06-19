## Noisy Data

Noisy Static Test

- Spikes before PMS and LNA changes
  - C:\Users\mwgeo\OneDrive\Projects\GPS\Logs\Devices\Motion Mini (WSW)\test02-garden
- Fix
  - [Power Management](performance/power-management.md)
  - [LNA Mode](performance/lna-mode.md)

- By using PMS Full + LNA Normal, static results are similar to the M8. So far. It's still early testing.
  - It brings sacc/hdop to the values I would have expected on an M8. It's my wild guess that PMS Balanced pollutes their inner RF path with noise due to sleep/wake spikes. There's more power management systems available and they have a convenient "limit inrush current on wake" configuration field.
  - Later... maybe it's only PMS Full and we could revert to LNA Bypass to increase battery life by an hour or so BUT this will be a question for future us.