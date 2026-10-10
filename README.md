# M33 X-8 Spectral Analysis (Work in Progress)

Status: Work in progress. This project independently reproduces and investigates the broadband X-ray spectral analysis of the ultraluminous X-ray source (ULX) M33 X-8 using NuSTAR and Swift/XRT observations. The analysis is being extended to XMM-Newton data.

## Overview

This repository reproduces the broadband X-ray spectral analysis of the ultraluminous X-ray source (ULX) **M33 X-8** presented by **Krivonos et al. (2018)** using publicly available **NuSTAR** and **Swift/XRT** observations. 

M33 X-8 is a nearby, borderline ultraluminous X-ray source that provides an important opportunity to study accretion near the Eddington limit and investigate the nature of compact objects. The analysis uses HEASoft for data reduction and XSPEC for spectral fitting, exploring phenomenological and physically motivated models to characterise the source's X-ray emission and accretion properties. The resulting fits and parameter constraints are compared with those reported in the reference study, with particular attention to differences in spectral parameters and the coronal electron temperature inferred from NTHCOMP-based models. 

The project is ongoing, with the analysis extending to XMM-Newton observations.

## Data Extraction

NuSTAR observations were reduced using **HEASoft**, following the standard processing pipeline. Raw observations were obtained from the HEASARC archive and processed using `nupipeline`. Source and background regions were selected using **SAOImage DS9**, and spectra, light curves, response matrix files (RMFs), and ancillary response files (ARFs) were generated using `nuproducts` for both FPMA and FPMB across the two observation epochs. The spectra were grouped to **30 counts per bin** using `ftgrouppha` for chi-squared fitting.

The **Swift/XRT** spectrum was reduced manually using `xrtproducts`, rather than using the pre-extracted spectrum from the UK Swift Science Data Centre adopted in the reference study.


## Spectral Modelling

Spectral fitting was performed in **XSPEC**, using the **3–20 keV** band for NuSTAR and the **0.3–5 keV** band for Swift/XRT. Single-component and multi-component models were fitted to characterise the source spectrum and investigate thermal disc emission and Comptonisation. Best-fit parameters and fit statistics were compared with those reported by Krivonos et al. (2018).

## Models Studied

### Phenomenological Models
- Power Law (POWERLAW)
- Cutoff Power Law (CUTOFFPL)
- DISKPBB
- DISKBB + Power Law
- DISKBB + CutoffPL

These models were used to characterise the continuum emission and assess improvements in fit quality with additional spectral components. Best-fit parameters and fit statistics were compared with the published results. Data and residuals were examined using ldata delchi plots.

### Physically Motivated Models
- SIMPL ⊗ DISKPBB
- (SIMPL ⊗ DISKPBB) × SPEXPCUT
- DISKPBB + NTHCOMP
- DISKBB + NTHCOMP

For these models, **`ldata delchi`**, **`ufspec`**, **`eeufspec`**, and confidence contours were generated to study the physical origin of the spectral components and parameter constraints.

## Results

- Single-component models fit poorly (χ²/d.o.f. of 1.42–2.47). Models combining a thermal disc with a curved or Comptonised high-energy component reach χ²/d.o.f. ≈ 1.1.
- The overall spectral shape and most parameters agree with Krivonos et al. (2018): inner disc temperature of about 1 keV, temperature-profile index p ≈ 0.75–0.76, and cutoff energy of about 7 keV.
- In the DISKPBB fit, p reaches the lower limit of the model (0.5), as also found by Krivonos et al.
- The fit statistics are systematically higher than those of Krivonos et al. for the same models.
- The electron temperature is only weakly constrained in the NTHCOMP models.

**Fit statistics (χ²/d.o.f.)**

| Model | This work | Krivonos et al. (2018) |
|---|---|---|
| Power law | 1991/930 | 1690/903 |
| Cutoff power law | 1315/929 | 1207/902 |
| DISKPBB | 1629/929 | 1584/902 |
| DISKBB | 2299/930 | not applicable |
| DISKBB + power law | 1079/928 | 951/901 |
| DISKBB + cutoff power law | 1009/927 | 891/900 |
| SIMPL ⊗ DISKPBB | 1021/928 | 901/901 |
| (SIMPL ⊗ DISKPBB) × SPEXPCUT | 1012/927 | 891/900 |
| DISKPBB + NTHCOMP | 1005/927 | 886/900 |
| DISKBB + NTHCOMP | 1005/928 | 887/901 |

**Physically motivated models: key parameters**

| Model | kT_in (keV) | p | Γ | Other | χ²/d.o.f. |
|---|---|---|---|---|---|
| SIMPL ⊗ DISKPBB | 0.909 ± 0.053 | 0.763 ± 0.024 | 3.459 ± 0.089 | f_scat = 0.506 ± 0.076 | 1021/928 |
| (SIMPL ⊗ DISKPBB) × SPEXPCUT | 1.172 ± 0.067 | 0.749 ± 0.018 | 1.738 ± 0.304 | f_scat = 0.412 ± 0.045, E_cut = 7.15 ± 1.31 keV | 1012/927 |
| DISKPBB + NTHCOMP | 0.971 ± 0.069 | 0.760 ± 0.080 | 3.240 ± 0.682 | kTe = 17.53 ± 57.31 keV | 1005/927 |
| DISKBB + NTHCOMP | 0.980 ± 0.031 | n/a | 3.170 ± 0.485 | kTe = 13.02 ± 26.10 keV | 1005/928 |

## Discussion

**Model comparison.** The four physically motivated models (χ² of 1005–1021) fit equally well, and also match the best two-component phenomenological fit (DISKBB + cutoff power law, 1009/927), so the data do not statistically favour one prescription over another. Allowing p to vary gives no improvement once NTHCOMP is included (χ² = 1005 for both models). DISKBB + NTHCOMP is adopted as the reference model because it gives one of the best fits with physically interpretable disc and Comptonisation parameters; the other models are kept to check how robust the results are.

**Electron temperature.** The main difference from Krivonos et al. is the constraint on kTe. For DISKBB + NTHCOMP, the best-fit value (13.02 ± 26.10 keV) is close to the published 17.7 (+1.3/−2.4) keV, but the uncertainty is far larger. For DISKPBB + NTHCOMP, Krivonos et al. report only a lower limit (kTe > 100 keV). Scans with `steppar` show that the fit statistic changes only marginally over a broad range of kTe, so it is weakly constrained rather than measured here.

**Possible contributor.** The Swift/XRT spectrum was extracted manually here, whereas the reference study used the online tools of the UK Swift Science Data Centre, including their pile-up treatment. Since the soft spectrum constrains the thermal disc component, this difference may affect the kTe constraint. It is a plausible contributor but has not been tested; the XMM-Newton extension is intended to help examine it.

**West et al. (2018).** Using NuSTAR and XMM-Newton data, West et al. found that an additional Comptonised component above 10 keV is required, ruling out a single advection-dominated disc and classical sub-Eddington models. This agrees with the poor fits of the single-component models here.

## Technical Report

A full technical report of this analysis is included in this repository: report/M33_Analysis_report.pdf
