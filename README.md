# vasp_raman.py

Raman off-resonant activity calculator using VASP as a back-end.

## Theory

In order to calculate off-resonance Raman activity of a mode, one needs to compute the derivative of the polarizability (or macroscopic dielectric tensor) with respect to that normal mode coordinate: `dP/dQ` (or `de/dQ`).  
Thus, two ingredients are required:

 1. Phonons at Γ-point
 2. Macroscopic dielectric tensor

### Phonons at Γ-point
In VASP, phonons at Γ-point can be computed using either:

 * finite displacements: `IBRION=5` or `IBRION=6`; or
 * density functional perturbation theory (DFPT): `IBRION=7` or `IBRION=8`.

Only finite displacements are available when hybrid functional is employed.

### Macroscopic dielectric tensor
In VASP, macroscopic dielectric tensor can be computed using either:
 * DFPT: `LEPSILON=.TRUE.`
 * or from frequency dependent dielectric matrix calculation: `LOPTICS=.TRUE.`.

In the latter case, hybrids functionals could be employed.  
For a more formal description of the method see [D. Porezag, M.R. Pederson, PRB, 54, 7830 (1996)](http://dx.doi.org/10.1103/PhysRevB.54.7830).

## Installation

Python >= 2.6 is required. Just copy `vasp_raman.py` in the `$PATH` and run! No external dependencies.

## Global variables

`vasp_raman.py` **requires** two environmental variables to be set:

  - `VASP_RAMAN_PARAMS` is defined as `FIRST-MODE_LAST-MODE_NDERIV_STEPSIZE` where:
      - `FIRST_MODE` - integer, first mode for which derivative of the polarizability is computed
      - `LAST-MODE`  - integer, last mode for which derivative of the polarizability is computed
      - `NDERIV`     - integer, scheme for finite difference, **currently** only value `2` is supported
      - `STEPSIZE`   - float, step-size for finite difference, in Angstroms
        
    An example is `VASP_RAMAN_PARAMS=01_10_2_0.01`

  - `VASP_RAMAN_RUN` the command to execute VASP (can contain MPI call):  
Example: `VASP_RAMAN_RUN='aprun -B /u/afonari/vasp.5.3.2/vasp.5.3/vasp &> job.out'`

## Examples

* [Raman activity spectrum for Si using VASP](https://github.com/raman-sc/VASP/tree/master/Sibulk-VASP)
* [Raman activity spectrum for Si using VTST tools](https://github.com/raman-sc/VASP/tree/master/Sibulk-VTST)
* [Raman activity spectrum for cyclopentadiene using VASP](https://github.com/raman-sc/VASP/tree/master/Cyclopentadiene)
* [Raman activity spectrum for Si using VTST tools and PW91 functional](https://github.com/raman-sc/VASP/tree/master/Sibulk)

## Changelog

#### 0.6 (will be released soon)
* ADDED: ability to use phonons obtained from the [vtst tools](theory.cm.utexas.edu/vtsttools/dynmat/)
* FIX: cleaned `POSCAR` parsing code

#### [0.5.1](https://raw.github.com/raman-sc/VASP/3cb3cdf0682609365c4b966472ef6eb5be1defc5/vasp_raman.py)
* FIX: contributors and version are now in the output
* FIX: [Cyclopentadiene example](https://github.com/raman-sc/VASP/tree/master/Cyclopentadiene) is now fully consistent with the version

#### [0.5](https://raw.github.com/raman-sc/VASP/3004f2fd455b0f81c28a2e227542b328d5998bbd/vasp_raman.py)
* Basic working functionality

## Contributors

Alexandr Fonari (Georgia Tech, PIs: J.-L. Bredas/V. Coropceanu): [Email](mailto:alexandr.fonari[nospam]gatech.edu)  
Shannon Stauffer (UT Austin, PI: G. Henkelman): [Email](mailto:stauffers[nospam]utexas.edu).
