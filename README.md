# Fourier-Transform Spectroscopy of a Mercury Lamp

**Second-year experimental physics project — Imperial College London | Report mark: 86%**

## Overview

In this project, I used a Michelson interferometer as a Fourier-transform spectrometer to measure the visible emission spectrum of a low-pressure mercury lamp.

A 632.8 nm HeNe laser provided an external reference for calibrating the optical path difference (OPD). I then processed the mercury interferogram in Python and applied a Fourier transform to recover the emission spectrum.

The project focused on three main questions:

- How accurately could the known mercury emission wavelengths be recovered?
- Which spectral line-profile model best described the measured peaks?
- How did interferometer scan length affect spectral resolution?

## Experimental Setup

The mercury lamp and HeNe reference laser were passed through a Michelson interferometer.

One detector recorded the HeNe reference interferogram while a second detector simultaneously recorded the mercury signal. As one mirror moved, the changing optical path difference generated the interference signals used for wavelength calibration and spectral reconstruction.

The full measurement used a 60-minute scan, corresponding to a maximum calibrated OPD of approximately **4.4 mm**.

<img width="400" alt="inteferometer drawio (1)" src="https://github.com/user-attachments/assets/da8d6d95-3e97-4c97-93e3-331642636451" />

*Michelson interferometer setup showing the mercury lamp, HeNe calibration laser, beam splitters, mirrors and detectors.*

## Analysis

The raw interferograms were converted into a calibrated spectrum through several processing stages:

1. **Signal filtering** — high-pass filtering removed DC offsets and slow instrumental drift.
2. **OPD calibration** — zero crossings of the HeNe reference interferogram were used to construct a locally calibrated optical-path-difference axis.
3. **Resampling and apodisation** — the mercury interferogram was interpolated onto a uniform OPD grid and a Hamming window was applied to reduce finite-scan sidelobes.
4. **Fourier transformation** — the processed interferogram was transformed from optical-path-difference space into wavelength space.
5. **Spectral fitting** — Gaussian, Lorentzian and Voigt profiles were compared using reduced chi-squared to determine which model best described the measured mercury lines.

## Results

### Recovered Mercury Spectrum

The reconstructed spectrum clearly recovered the strong green mercury emission line near **546 nm** and the yellow doublet near **577 nm and 579 nm**.

<img width="700" alt="fig_DA2_Hg_spectrum_notch_band_and_zoom_coloured (6)" src="https://github.com/user-attachments/assets/7911de76-8734-4e9f-bde9-e9ed4b266974" />


*Recovered visible mercury spectrum. The main green line and yellow doublet are clearly resolved, while smaller features around the green peak were investigated as possible instrumental sidelobes.*

### Wavelength Accuracy and Line-Profile Fitting

To determine the line centres accurately, I compared Gaussian, Lorentzian and Voigt models rather than selecting a profile based only on visual agreement.

The **Voigt profile produced the lowest reduced chi-squared** for both the green line and yellow doublet and was therefore used for the final wavelength and linewidth measurements.

<img width="700" alt="fig_DA4_Voigt_fits_green_yellow (6)" src="https://github.com/user-attachments/assets/87f3f2fc-0d1d-4b92-ad0b-6637d350f551" />

*Voigt-profile fits to the green mercury line and yellow doublet used to determine the final line centres and widths.*

The measured wavelengths were:

| Emission line | Reference / nm | Measured / nm | Difference / nm |
| --- | ---: | ---: | ---: |
| Green | 546.0750 | 546.0770 | +0.0020 |
| Yellow 1 | 576.9610 | 576.9631 | +0.0021 |
| Yellow 2 | 579.0670 | 579.0702 | +0.0032 |

All three measured line centres agreed with their reference wavelengths to within approximately **0.002–0.003 nm**.

The total estimated wavelength uncertainty was approximately **0.02 nm**, meaning that all three measurements were comfortably consistent with the reference values.

### Understanding the Uncertainty

I separated the wavelength uncertainty into contributions from:

- instrumental resolution
- statistical fitting uncertainty
- residual calibration uncertainty

The fitting uncertainties were only of order **10⁻⁴ nm**, while the calibration differences were around **0.002–0.003 nm**.

The dominant limitation was therefore the **finite instrumental resolution rather than statistical fitting noise**.

This was important because it showed that improving the fitting algorithm alone would not substantially improve the overall measurement precision.

### Spectral Resolution and Scan Length

I also investigated how the maximum optical path difference affected spectral resolution.

The original interferogram was repeatedly truncated to shorter OPD ranges and the analysis was rerun for each scan length.


For shorter scans, the measured width of the green mercury line decreased approximately according to the expected $1/L_{\max}$ relationship for a Fourier-transform spectrometer limited by finite optical path difference.


<img width="500" alt="Green_line_FWHM_vs_scan_range (5)" src="https://github.com/user-attachments/assets/ab847111-07c0-46b3-bba7-ac848624277b" />

*Measured green-line FWHM as the maximum OPD scan range increases, compared with the expected instrumental width.*

At larger scan ranges, however, the improvement became progressively smaller. The measured FWHM approached approximately **0.1–0.12 nm**, despite the theoretical instrumental width continuing to decrease.

This showed that increasing scan length improves spectral resolution only until other effects become significant, including:

- intrinsic mercury line width
- Hamming apodisation
- slow instrumental drift
- measurement noise

### Distinguishing Physical Features from Artefacts

Small features were visible around the strong 546 nm green line.

Rather than assuming that these represented additional mercury transitions, I investigated whether they could instead result from the finite-OPD response of the interferometer.

Their approximate symmetry around the main peak, sinc-like appearance and sensitivity to scan length and apodisation indicated that they were primarily **instrumental sidelobes rather than genuine spectral lines**.

This was an important part of the analysis because it demonstrated that features appearing in experimental data should not automatically be interpreted as physical effects.

## Conclusion

The Michelson interferometer successfully operated as a Fourier-transform spectrometer for a low-pressure mercury lamp.

Using the HeNe reference for local OPD calibration, the main mercury emission lines were recovered to within approximately **0.002–0.003 nm of their reference wavelengths**, comfortably inside the total estimated uncertainty of approximately **0.02 nm**.

The experiment also demonstrated the trade-off between scan length and spectral resolution. Increasing the maximum OPD initially improved resolution in line with the expected **1 / Lmax** behaviour, but the improvement eventually approached a floor of approximately **0.1 nm** as other broadening mechanisms became dominant.

Overall, the experiment showed that a relatively simple Michelson Fourier-transform spectrometer can recover the main mercury emission wavelengths with approximately **0.02 nm wavelength uncertainty and sub-0.2 nm spectral resolution**, provided that the optical path difference is carefully calibrated.

## Why This Project Is Useful

Fourier-transform spectroscopy is used wherever precise spectral information is required, including:

- astronomy
- atomic and molecular spectroscopy
- chemical identification
- remote sensing
- optical instrumentation

More broadly, this project demonstrated how a reliable experimental result depends on the entire analysis chain rather than only the quality of the raw data.

Calibration, signal processing, model selection, uncertainty analysis and understanding the limitations of the instrument all influenced the final measurement.

## What I Learned

This project taught me not to underestimate instrumental effects. It is easy to assume that unexpected features or limitations come from the underlying physics, when in reality the instrument or analysis method may be responsible for much of what is being observed.

I also learned the importance of testing assumptions quantitatively rather than relying only on visual judgement. A model or result can look convincing, but that is not enough evidence on its own.

Finally, I learned that improving data quality is not always as simple as collecting more data. I initially assumed that increasing the scan length would continue to improve the spectral resolution, but later found that other limitations had become more important. This reinforced the importance of testing different possible limitations before deciding what actually needs to be improved.

## Applying What I Learned

In future projects, I would try to support my assumptions and judgements with quantitative evidence before relying on them.

I would also avoid over-optimising one part of a project at the expense of everything else. In this experiment, I focused too heavily on increasing the scan length because I assumed that more data would keep improving the result. That made it easier to overlook other limitations that were becoming more important.

A useful lesson for me was that the best solution is often a trade-off rather than making one part of a project as perfect as possible. A balanced analysis, where each important component is developed to a strong and consistent standard, can be more useful than maximising one part while neglecting the rest.

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

This repository is a portfolio summary of assessed university laboratory work.

The full submitted report, raw data and assessed analysis code are not publicly provided. The purpose of this repository is to summarise the experimental approach, analysis, results and skills developed during the project.
