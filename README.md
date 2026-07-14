# M33 X-8 Spectral Analysis (Work in Progress)

> **Note:** This repository is currently under construction. Additional notebooks, scripts, figures, and documentation will be added as the analysis is finalized.

## Overview

This repository reproduces the broadband X-ray spectral analysis of the ultraluminous X-ray source (ULX) **M33 X-8** presented by **Krivonos et al. (2018)** using publicly available **NuSTAR** and **Swift/XRT** observations. The project focuses on high-energy astrophysics, black hole accretion physics, and spectral state modelling by reproducing both phenomenological and physically motivated XSPEC models to study the nature of the accretion flow and Comptonizing corona.


## Data Extraction

The NuSTAR data were manually reduced using **HEASoft** following the standard pipeline. Raw observations were downloaded from the HEASARC archive, cleaned using **`nupipeline`**, source and background regions were selected manually in **SAOImage DS9**, and spectra, light curves, response files (RMFs) and ARFs were generated using **`nuproducts`** for both FPMA and FPMB modules across the two observation epochs. The extracted spectra were then grouped to **30 counts per bin** using **`ftgrouppha`** for χ² fitting. Unlike the reference paper, the **Swift/XRT** spectrum was also reduced manually using **`xrtproducts`** rather than using the pre-generated spectrum from the **UK Swift Science Data Centre**.


## Models Studied

### Phenomenological Models
- Power Law
- Cutoff Power Law
- DISKPBB
- DISKBB + Power Law
- DISKBB + CutoffPL

For these models, **`ldata delchi`** plots were generated and the best-fit spectral parameters were compared with the published results.

### Physically Motivated Models
- SIMPL ⊗ DISKPBB
- SIMPL ⊗ DISKPBB × SPEXPCUT
- DISKPBB + NTHCOMP
- DISKBB + NTHCOMP

For these models, **`ldata delchi`**, **`ufspec`**, **`eeufspec`**, and confidence contours were generated to study the physical origin of the spectral components and parameter constraints.


## Results

The spectral fitting successfully reproduced the principal results of **Krivonos et al. (2018)**, with most best-fit parameters—including the disk temperature, photon index, temperature profile parameter (*p*), scattering fraction, and cutoff energy—remaining consistent with the published values. All phenomenological and physically motivated models were successfully implemented and their spectral properties compared with the reference work.


## Discussion

One notable discrepancy was found for the **DISKBB + NTHCOMP** model. While the best-fit parameters closely matched those reported by Krivonos et al. (2018), the electron temperature of the Comptonizing corona (**kTe**) remained only weakly constrained in the present analysis. Parameter-space exploration using XSPEC (`steppar`) showed that the fit statistic changed only marginally over a broad range of electron temperatures, unlike the tighter constraint reported in the reference paper. A likely reason is the independent manual reduction of the **Swift/XRT** spectrum, where pile-up correction becomes critical. The reference paper used the pile-up corrected spectrum provided directly by the **UK Swift Science Data Centre**, whereas this work performed the complete extraction manually using **HEASoft**. Since the Swift soft X-ray spectrum anchors the thermal disk component, even small differences in pile-up treatment can propagate into the Comptonization parameters and reduce the sensitivity to **kTe**.

Interestingly, this behaviour is more consistent with **West et al. (2018)**, who combined **NuSTAR** and **XMM-Newton** observations and argued that the **DISKBB + NTHCOMP** model, although statistically acceptable, does not uniquely describe the physical nature of M33 X-8. Their work instead favours a broadened disk associated with near- or super-Eddington accretion, highlighting that different physically motivated models can produce similar statistical fits while implying different accretion scenarios.


## Future Work

- Add complete XSPEC fitting scripts.
- Upload plotting notebooks and analysis workflow.
- Include comparison tables for all fitted models.
- Add parameter confidence analysis and contour plots.
- Extend the repository with timing analysis and additional ULX spectral models.
