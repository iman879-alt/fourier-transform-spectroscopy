# Fourier-Transform Spectroscopy of a Mercury Lamp

**Second-year experimental physics project — Imperial College London | Report mark: 86%**

## Overview

In this project, I used a Michelson interferometer as a Fourier-transform spectrometer to measure the visible emission spectrum of a low-pressure mercury lamp.

A 632.8 nm HeNe laser was used as an external reference to calibrate the optical path difference (OPD). The mercury interferogram was then processed in Python and Fourier transformed to recover the emission spectrum.

The main aim was to answer:

> **How accurately can a simple Michelson Fourier-transform spectrometer, calibrated with a HeNe laser, recover the wavelengths and line profiles of the main visible emission lines of a low-pressure mercury lamp?**

The analysis focused on three main questions:

- How accurately could the known mercury emission wavelengths be recovered?
- Which line-profile model best described the measured peaks?
- How did the interferometer scan length affect spectral resolution?

## Experimental Approach

Light from a mercury lamp and a HeNe laser was passed through a Michelson interferometer.

One detector recorded the HeNe reference interferogram while a second detector simultaneously recorded the mercury signal. As one interferometer mirror moved, the changing optical path difference produced the interference signals used for the analysis.

The full measurement consisted of a 60-minute scan, corresponding to a maximum calibrated OPD of approximately **4.4 mm**. This gave a nominal instrumental resolution of approximately **0.04 nm** around the yellow mercury lines. 

<!-- Add experimental setup diagram here -->

## Data Analysis

The raw detector signals required several processing steps before a reliable spectrum could be obtained.

### 1. Signal Pre-processing

Both detector signals were high-pass filtered using a second-order Butterworth filter to remove DC offsets and slow instrumental drift.

The ends of the signals were removed to reduce filtering transients.

### 2. Optical Path Difference Calibration

The HeNe interferogram provided a stable wavelength reference.

Zero crossings of the filtered HeNe signal were identified and used to construct a locally calibrated OPD axis. Because this calibration was not perfectly uniformly spaced, the mercury interferogram was then resampled onto a uniform OPD grid using cubic-spline interpolation. 

<!-- Add OPD calibration figure here -->

### 3. Fourier Transform

A Hamming window was applied to reduce spectral sidelobes caused by the finite scan range.

The processed interferogram was then Fourier transformed to convert the signal from optical path difference into spatial frequency and finally wavelength.

The measured spectrum was also corrected for the wavelength-dependent responsivity of the photodiode.

<!-- Add full mercury spectrum here -->

### 4. Spectral-Line Fitting

The main mercury features analysed were:

- the green line near **546 nm**
- the yellow doublet near **577 nm and 579 nm**

Gaussian, Lorentzian and Voigt profiles were fitted to the measured peaks and compared using reduced chi-squared.

The Voigt profile produced the lowest reduced chi-squared for both the green line and yellow doublet, so it was used to extract the final peak positions and widths.

<!-- Add Voigt fit figure here -->

## Results

### Wavelength Accuracy

The fitted mercury wavelengths were:

| Emission line | Reference / nm | Measured / nm | Difference / nm |
| --- | ---: | ---: | ---: |
| Green | 546.0750 | 546.0770 | +0.0020 |
| Yellow 1 | 576.9610 | 576.9631 | +0.0021 |
| Yellow 2 | 579.0670 | 579.0702 | +0.0032 |

All three measured line centres therefore agreed with the reference values to within approximately **0.002–0.003 nm**.

This was much smaller than the overall estimated wavelength uncertainty of approximately **0.02 nm**, meaning that the measured wavelengths were fully consistent with the reference values.

### Uncertainty Budget

I separated the wavelength uncertainty into three contributions:

- instrumental resolution
- statistical uncertainty from fitting
- residual calibration uncertainty

The total uncertainty was approximately **0.02 nm for all three lines**.

The fitting uncertainties were only of order `10^-4 nm`, while calibration offsets were around `0.002–0.003 nm`. The dominant limitation was therefore the finite instrumental resolution rather than statistical fitting noise. 

This was an important result because it showed that improving the fitting procedure alone would not substantially improve the final measurement precision.

### Spectral Resolution

I then investigated how spectral resolution changed with interferometer scan length.

The original 60-minute interferogram was repeatedly truncated to shorter OPD ranges and the complete analysis pipeline was rerun for each scan length.

For shorter scans, the measured green-line width decreased approximately as:

`1 / Lmax`

which is the expected behaviour for an interferometer whose resolution is limited by finite optical path difference.

However, for longer scans the improvement became progressively smaller and the measured FWHM approached a limiting value of approximately **0.1–0.12 nm**. 

<!-- Add FWHM vs OPD scan range figure here -->

This showed that increasing scan length improves resolution only until other effects become important, including:

- the intrinsic mercury line width
- Hamming apodisation
- slow instrumental drift
- noise

### Instrumental Artefacts

Small features appeared around the strong 546 nm green line.

Rather than interpreting them immediately as additional mercury transitions, I compared their behaviour with what would be expected from the finite-OPD instrumental response.

Their approximate symmetry around the main peak, sinc-like appearance and dependence on scan length and apodisation indicated that they were primarily **instrumental sidelobes rather than real spectral lines**. 

This was an important part of the analysis because it demonstrated the need to distinguish genuine physical features from artefacts introduced by the measurement and processing pipeline.

## Conclusion

The Michelson interferometer successfully operated as a Fourier-transform spectrometer for a low-pressure mercury lamp.

Using local calibration from the HeNe reference, the main mercury emission lines were recovered to within approximately **0.002–0.003 nm of reference values**, comfortably inside the total estimated wavelength uncertainty of approximately **0.02 nm**.

The experiment also demonstrated the trade-off between scan length and spectral resolution. Increasing the maximum optical path difference initially improved the measured resolution approximately as expected from the theoretical `1 / Lmax` relationship, but the improvement eventually approached a floor of approximately **0.1 nm** as other broadening mechanisms became dominant.

Overall, the experiment showed that a relatively simple Michelson Fourier-transform spectrometer can recover the main mercury emission wavelengths with approximately **0.02 nm accuracy and sub-0.2 nm spectral resolution**, provided that the optical path difference is carefully calibrated. 

## Why This Project Is Useful

Fourier-transform spectroscopy is widely used wherever precise spectral information is required.

Similar methods are used in areas including:

- astronomy
- atomic and molecular spectroscopy
- chemical identification
- remote sensing
- optical instrumentation

More generally, this project demonstrates an important feature of experimental data analysis: the final result depends not only on collecting data, but also on calibration, signal processing, model selection, uncertainty analysis and understanding the limitations of the measurement system.

## What I Learned

This project significantly developed my approach to experimental data analysis.

I learned that obtaining a physically meaningful result often requires building a complete processing pipeline rather than applying a single calculation to raw data. In this experiment, filtering, calibration, interpolation, Fourier transformation, detector-response correction and peak fitting all affected the final spectrum.

I also developed a better understanding of **model comparison**. Rather than choosing a Gaussian, Lorentzian or Voigt profile because one appeared visually convincing, I compared the fits quantitatively using reduced chi-squared before selecting the Voigt model.

The uncertainty analysis was particularly useful. Separating instrumental, calibration and fitting contributions showed me that the largest source of uncertainty is not always the most obvious one. In this case, statistical fitting errors were very small, while the finite instrumental resolution dominated the final wavelength uncertainty.

Finally, investigating the apparent sidelobes reinforced the importance of questioning unexpected features in data. A feature in a plot is not automatically a physical effect; it may instead result from the instrument, processing method or assumptions used in the analysis.

## What I Would Improve

If I repeated the experiment, I would focus primarily on reducing systematic rather than statistical uncertainty.

Possible improvements would include:

- improving the absolute OPD calibration and reducing differences between the optical paths followed by the HeNe and mercury beams
- improving long-term thermal and mechanical stability during the 60-minute scan
- investigating alternative apodisation windows and their effect on spectral resolution and sidelobes
- explicitly modelling the measured line profile as a convolution of the source spectrum with the finite-OPD instrumental response
- accounting more carefully for correlations in the noise introduced by filtering and Fourier transformation

These improvements would provide a more physically complete model of the measured spectrum and could help reduce the remaining difference between the measured line width and the ideal instrumental resolution.

## Technologies & Skills

- Python
- NumPy
- SciPy
- Matplotlib
- Fourier transforms
- Signal processing
- Non-linear curve fitting
- Statistical model comparison
- Uncertainty analysis
- Data visualisation
- Experimental physics

## Academic Integrity

This repository is a portfolio summary of an assessed university laboratory project.

The full submitted report, raw data and assessed analysis code are not publicly provided. The purpose of this repository is to summarise the experimental approach, analysis, results and skills developed during the project.
