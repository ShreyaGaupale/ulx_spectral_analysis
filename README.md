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

The spectral fitting successfully reproduced the principal results of **Krivonos et al. (2018)**, with most best-fit parameters—including the disk temperature, photon index, temperature profile parameter (*p*), scattering fraction, and cutoff energy remaining consistent with the published values. All phenomenological and physically motivated models were successfully implemented and their spectral properties compared with the reference work.


## Discussion

One notable discrepancy was found for the **DISKBB + NTHCOMP** model. While the best-fit parameters closely matched those reported by Krivonos et al. (2018), the electron temperature of the Comptonizing corona (**kTe**) remained only weakly constrained in the present analysis. Parameter-space exploration using XSPEC (`steppar`) showed that the fit statistic changed only marginally over a broad range of electron temperatures, unlike the tighter constraint reported in the reference paper. A likely reason is the independent manual reduction of the **Swift/XRT** spectrum, where pile-up correction becomes critical. The reference paper used the pile-up corrected spectrum provided directly by the **UK Swift Science Data Centre**, whereas this work performed the complete extraction manually using **HEASoft**. Since the Swift soft X-ray spectrum anchors the thermal disk component, even small differences in pile-up treatment can propagate into the Comptonization parameters and reduce the sensitivity to **kTe**.

Interestingly, this behaviour is more consistent with **West et al. (2018)**, who combined **NuSTAR** and **XMM-Newton** observations and argued that the **DISKBB + NTHCOMP** model, although statistically acceptable, does not uniquely describe the physical nature of M33 X-8. Their work instead favours a broadened disk associated with near- or super-Eddington accretion, highlighting that different physically motivated models can produce similar statistical fits while implying different accretion scenarios.


## Future Work

- Add complete XSPEC fitting scripts.
- Upload plotting notebooks and analysis workflow.
- Include comparison tables for all fitted models.
- Add parameter confidence analysis and contour plots.
- Extend the repository with timing analysis and additional ULX spectral models.
