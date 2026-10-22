# CITEAM 2027 — Part D: Analyzing a CBED Pattern (Silicon [001])

HyperSpy/diffsims port of `1PM_Analyze_CBED_Pattern.ipynb` from the MLSTEM 2026
workshop (G. Duscher & S. Kalinin, UTK), following the same approach as the Part B
port `CITEAM_Basic_Diffraction_Al_HyperSpy`.

## Contents

| file | what it is |
|---|---|
| `CITEAM_Analyze_CBED_Si_HyperSpy_student.ipynb` | teaching version, outputs cleared |
| `CITEAM_Analyze_CBED_Si_HyperSpy_executed.ipynb` | same notebook, run end to end |
| `CITEAM_Analyze_CBED_Si_HyperSpy_executed.pdf`  | printable record of the run |
| `data/CBED_375mm_alpha-3.3_beta9.6_Condensor10um_Filter.dm3` | the MLSTEM data file |

## Data provenance

`CBED_375mm_alpha-3.3_beta9.6_Condensor10um_Filter.dm3` (17,382,840 bytes) lives in
`example_data/` of BOTH `gduscher/MLSTEM2026` and `gduscher/MLSTEM2025` — identical file.
It is the only file in the MLSTEM2026 `example_data/` folder.

    https://github.com/gduscher/MLSTEM2026/raw/main/example_data/CBED_375mm_alpha-3.3_beta9.6_Condensor10um_Filter.dm3

Recorded 2017-09-27 on a Zeiss Libra 200 MC, Gatan US1000XP camera, 200 kV, 2 s,
energy-filtered. The notebook downloads it automatically if `data/` is empty.

## Running

    pip install hyperspy diffsims ase orix
    jupyter lab CITEAM_Analyze_CBED_Si_HyperSpy_student.ipynb

Runs clean on hyperspy 2.5.0, diffsims 0.7.0, ase 3.29.0, orix 0.15.0.

## What the notebook establishes

* The DM3 carries **wrong** metadata, not missing metadata: a real-space (nm) axis
  calibration on a diffraction pattern, `Operation Mode = IMAGING`, and a stale
  `Specimen` field naming a block copolymer. The physics it does carry — 200 kV,
  378 mm nominal camera length, 14 um CCD pixels — is correct and sufficient to
  calibrate from first principles.
* Nominal camera length (378 mm) disagrees with the silicon by 17%; the refined
  value is 324 mm. The convergence angle in the *file name* (3.3 mrad) is wrong by a
  factor of two against the measured disk radius (6.7 mrad).
* Refined calibration: 0.017209 1/nm per pixel, centre (1164.4, 997.2) px,
  rotation 16.5 deg, convergence 6.69 mrad.
* Only the direct beam and the four {220} disks are above background; the allowed
  {400} and beyond are not detectable at this exposure.
* Inside a {220} disk, exact Bragg sits at 98% of the disk radius (the inner edge),
  not at the disk centre. Two-beam dynamical theory gets the fringe spacing roughly
  right and the peak position wrong — the pattern is many-beam.
