## Timestamp Variations

The ESP GPS logging at 5 Hz includes timestamp intervals of 199 or 201 milliseconds. This is most evident in the GPY + SBP files where the timestamps are in milliseconds, and rarely seen as an issue in UBX files.

After detailed investigations it transpires that this is due to clock drift within the GNSS receiver. I have lots of interesting examples to show for different chipsets but have not gotten around to documenting this phenomena properly.

In the meantime, I have shared a very simple summary within my [gps-details](https://logiqx.github.io/gps-details/general/timestamps/) repository.