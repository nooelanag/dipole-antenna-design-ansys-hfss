# Dipole Antenna Design with ANSYS HFSS

Lab project of *Radio Frequency and Antenna Subsystems*
(Master's in Telecommunication Engineering, UC3M).

Design and electromagnetic characterisation of a **half-wavelength dipole
antenna** at 2.3 GHz in ANSYS HFSS (Ansys Electronics Desktop), analysed through
its reflection coefficient, input impedance, gain and efficiency versus
frequency, 3D directivity, 2D radiation patterns and the fields on the antenna
itself.

## Model

| Parameter | Value |
|---|---|
| Design frequency | 2.3 GHz |
| Wavelength | 0.130 m |
| Initial antenna length | half a wavelength, as a parametric variable |
| Antenna radius | 0.01 wavelengths |
| Feed | 2D rectangular lumped port in the XZ plane, 50 ohm, across the gap |

The dipole is built as a cylinder centred on the origin, and the feed gap is
created by duplicating that solid, shortening the copy and subtracting it from
the dipole. Every dimension is defined through variables, so the geometry
rebuilds automatically when a parameter changes.

## Length optimisation

With a length of exactly half a wavelength the resonance does not fall at the
target frequency, so the multiplier applied to the wavelength is turned into a
variable, `L_tune`, and swept with an Optimetrics parametric analysis from 0.4 to
0.5 in steps of 0.001. Narrowing the family of traces around the 2.3 GHz marker
gives the optimum:

    L_tune = 0.441 wavelengths

## Results

| Quantity | Value |
|---|---|
| S11 at resonance | -17.19 dB |
| -10 dB band | 2.160 to 2.468 GHz |
| Fractional impedance bandwidth | 13.39 % |
| Input impedance Z11 at resonance | 63.81 - j7.59 ohm |
| Z11 before tuning the length | 110.87 + j45.94 ohm |
| Peak directivity | 2.51 dB |
| Half-power beamwidth | about 74 degrees |
| Radiation and total efficiency | close to 100 % |

Observations:

- Tuning the length moves the real part of the input impedance from 110.87 ohm
  towards 50 ohm and brings the imaginary part close to zero, which is what the
  improvement in S11 reflects.
- The 2D patterns are plotted in the elevation plane against theta and in the
  azimuth plane against phi, where the dipole pattern is a circle.
- Gain and directivity are related by G = D * efficiency, so gain should never
  exceed directivity. Here the two coincide, because the simulated radiation and
  total efficiencies come out marginally above 100 %, a small numerical artefact
  that is otherwise negligible.
- The surface current `ComplexMag_Jsurf` matches the theoretical distribution: a
  maximum at the centre of the half-wavelength dipole and minima at the arm ends.
  Re-evaluating the same structure at other frequencies, so that its electrical
  length becomes a quarter wavelength or a full wavelength, reproduces the
  expected behaviour: the full-wavelength case develops two lobes with a minimum
  at the centre, while the quarter-wavelength case keeps the maximum at the centre
  with a lower value. Total efficiency drops in both cases.

## Repository contents

- `PRACTICA_3_final.aedt` - HFSS project with the geometry, setup, parametric
  sweep and reports
- `REPORT.pdf` - lab report with all results, in Spanish

## How to run

Open the `.aedt` file in Ansys Electronics Desktop and run the analysis. Solution
data is not included in the repository, since HFSS regenerates the mesh and the
field solution locally. The parametric sweep over `L_tune` is disabled, with the
optimum value set as nominal; re-enable it from Optimetrics to reproduce the
length study.

## Notes

The lab guide and the base material were provided by the course instructors and
are not included in this repository.

## Authors

[Noel Andolz Aguado](https://github.com/nooelanag) and
[Daniel Lozano Uceda](https://github.com/dalouc)
