---
layout: page
title: "DOSVIEW: Calibration"
permalink: /dosview/calibration
parent: DOSVIEW
nav_order: "2"
---


# Energy Calibration

The energy calibration tool in DOSVIEW provides an interactive and reproducible workflow for converting detector channel numbers into physical energy values using measured spectra of known reference sources. This calibration step is essential for any further spectral analysis, as it allows detector histograms to be interpreted in real energy units such as keV or MeV instead of arbitrary channel numbers.

The calibration tool is implemented as a dedicated tab within DOSVIEW and integrates directly with the existing workflow. It combines structured tables, interactive graphics, and automatic numerical fitting while keeping the calibration process transparent and easy to reproduce.

The tool can be launched in two ways:

* from the graphical interface via **Tools → Calibration**
* directly from the command line using `dosview --calibration`

![Dosview main window](img/dosview_calibration.png)

## Typical Calibration Workflow

A typical energy calibration session in DOSVIEW follows these steps:

1. Load one or more spectral CSV files containing histogram data.
2. Identify known spectral peaks corresponding to reference energies.
3. Create channel-to-energy calibration points for these peaks.
4. Precisely align calibration markers with the peaks in the spectrum.
5. Calculate calibration coefficients using the defined points.
6. Verify the calibration using the energy axis and reference markers.
7. Save the calibration project or export plots for further use.

This workflow is designed to be iterative; calibration points can be adjusted at any time, with all changes immediately reflected in the spectrum plot.

---

## User Interface Overview

After opening the calibration tab, the interface is divided into two main areas:

* **Left panel** – contains tables and controls for managing loaded spectra, defining calibration points, working with reference energies, and displaying calculated calibration constants.
* **Right panel** – shows an interactive plot of the loaded spectra, which updates immediately when calibration parameters are changed.

This layout allows calibration points to be adjusted while directly observing their effect on the spectrum.


## Loading Spectral Data

Spectral data are loaded using the **Add CSV** button. Each CSV file represents a single histogram and must contain:

* channel number (numeric)
* count value (numeric)

No header row is required. Multiple spectra can be loaded simultaneously, making it possible to compare different measurements or reference sources within one calibration session. Each loaded spectrum can be:

* shown or hidden independently
* assigned a custom label used in the plot legend


## Channel-to-Energy Calibration

The actual energy calibration is performed by defining channel-to-energy calibration points. These points represent known spectral features, most commonly characteristic peaks from calibration sources.

Calibration points can be created manually or imported from the list of known reference energies located in the lower part of the left panel. When a reference energy is added to the channel-to-energy table, a thick vertical marker line appears in the spectrum plot above the graph.

This vertical line represents the expected position of the selected energy and must be aligned with the corresponding spectral peak. The alignment can be performed in two equivalent ways:

* by entering the channel number directly in the channel field in the left panel, or
* by dragging the vertical marker line with the mouse along the channel axis in the spectrum plot.

The marker should be positioned at the center of the peak corresponding to the given element or energy. This procedure must be repeated for all selected reference energies.

For a valid calibration, at least **two calibration points** are required. However, using more points is strongly recommended, as it improves the robustness of the fit and helps to identify possible non-linearities or outliers.

Once the desired calibration points are defined and aligned, the calibration constants can be calculated using the **Calculate calibration** (or **Estimate calibration constants**) button. This operation determines the calibration coefficients based on the current positions of all defined marker lines.



## Calibration Model and Constants

DOSVIEW currently uses a linear calibration model:

```
E [keV] = a × channel + b
```

where:

* `a` is the energy-per-channel slope
* `b` is the offset corresponding to the energy at channel zero

After defining a sufficient number of calibration points, clicking **Estimate calibration constants** performs a linear regression using all defined points. The calculated parameters are applied immediately, and the resulting calibration formula is displayed in the plot legend.



## Reference Energies

The calibration tool includes a table of reference energies that can be used as a lightweight database of known spectral lines. Each entry contains:

* energy value
* optional element or isotope label
* visibility flag

Reference energies can be displayed directly in the plot to assist with peak identification. Selected entries can also be imported into the channel-to-energy calibration table, where they can be matched to observed peaks and used for calibration.



## Visualization and Export

Several visualization options are available to support both quick inspection and detailed calibration work:

* linear or logarithmic Y-axis scaling
* switching the X-axis between channel number and calibrated energy
* exporting the current plot as PNG or JPG
* opening the plot in a separate matplotlib window

The matplotlib view provides additional features such as dual X-axes (channel and energy), grid lines, and standard zoom and pan controls.



## Project Files and Reproducibility

The complete calibration setup can be saved into a `.dosview_calib` project file. This file stores:

* loaded spectra and their visibility states
* channel-to-energy calibration points
* reference energies
* calculated calibration constants
* plot scaling settings

Saved project files can be loaded later to continue work or to reproduce the calibration exactly. A typical workflow consists of loading spectra, defining calibration points, estimating calibration constants, verifying the result using the energy axis, and finally saving the project or exporting plots for documentation or publication.
