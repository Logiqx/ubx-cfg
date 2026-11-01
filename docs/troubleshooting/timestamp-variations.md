## Timestamp Variations

The ESP GPS logging at 5 Hz includes timestamp intervals of 199 or 201 milliseconds. This is most evident in the GPY + SBP files where the timestamps are in milliseconds, and is not seen in UBX files.

After detailed investigations it transpires that this is due to clock drift within the GNSS receiver, and two articles have been written:

- [Navigation Epochs](../fundamentals/navigation-epochs)
- [GNSS Timestamps](https://logiqx.github.io/gps-details/general/timestamps/)

The first article (Navigation Epochs) recommends that timestamps are rounded to the nearest 5 ms.

This simple recommendation resolves the issues related to variable timestamp intervals; 1, 2, 4, 5, 8, 10, 20, 25 Hz.