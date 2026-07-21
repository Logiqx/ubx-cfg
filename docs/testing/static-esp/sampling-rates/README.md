## Static ESP Testing - Sampling Rates

### Theory

See what Google says if you enter the following search term:

- "gaussian error propagation reduction in error with twice as many measurements"

You will probably be given results that touch on the following points:

- Doubling the number of measurements (N) reduces the error of the mean by a factor of sqrt(2).
- Error scales inversely with sqrt(N), taking twice as many measurements decreases your uncertainty to about 70.7%.

That is the theory, but does it really apply to GNSS measurements?

- Gaussian error propagation relies upon two assumptions
  - The errors are random and normally distributed
  - The measurements are independent of one another
- It is somewhat questionable whether these are sound assumptions u-blox output
  - u-blox receivers make use of a Kalman filter to minimise noise in the NAV solution
  - The Kalman filter directly impacts future positions and speeds... that is how they work

Anyway, putting the theory aside, Gaussian error propagation is still useful when debating the benefits of 5 Hz and 10 Hz.



### Practice

The static testing of the SYNAC GPS concluded with [Phase 7](../test-phases/phase-7/README.md) which clearly demonstrated that 5 Hz performs better than 10 Hz.

The mean values for Speed Over Ground (SOG) were as follows:

- 10 Hz = 0.042 kt
- 5 Hz = 0.024 kt

Since 10 Hz has twice as many samples as 5 Hz, 70% of 0.042 kt can be directly compared to 0.024 kt.

i.e. +/- 0.030 kt vs +/- 0.024 kt

Thus, if these magnitudes of error were to be applied to kinematic data, 5 Hz would still be better than 10 Hz.

The differences are small, but there is no reason to double file sizes (and increase processing) for zero benefit.



### Links

Some relevant statistical concepts:

- [Law of large numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers)
- [Central limit theorem](https://en.wikipedia.org/wiki/Central_limit_theorem)
- [Propagation of uncertainty](https://en.wikipedia.org/wiki/Propagation_of_uncertainty)