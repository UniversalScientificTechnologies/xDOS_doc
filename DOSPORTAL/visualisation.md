---
layout: page
title: "Visualization methodology"
parent: "DOSPORTAL - Cloud-based Dosimetry Data Platform"
permalink: /dosportal/visualisation
nav_order: 2
sitemap: false
math: true
---

# Visualization Methodology

This text describe the methodology that DOSPORTAL uses to visualize data.


## Evolution Charts

Vizualize dosimetric data in time.

![Dosage in silicon evolution chart in DOSPORTAL](/DOSPORTAL/img/DSi_evolution.png)

*Dose rate in silicon over the course of a measurement.*

### Dosage in Silicon

Radiation dosage in silicon measures the energy absorbed from ionizing or particle radiation per unit mass.

$$DS_i = \frac{E_i \, q}{m} \cdot \frac{10^{6} \cdot 3600}{\Delta t} \quad [\mathrm{\mu Gy/h}]$$

Three step process described below:

**1. Energy per channel.**

$$E_j = \mathrm{coef_0} + (j - j_{\min})\,\mathrm{coef_1} \quad [\mathrm{MeV}]$$

**2. Energy deposited per exposure.**

$$E_i = \sum_j C_{i,j}\,E_j \quad [\mathrm{MeV}]$$

**3. Dose rate in silicon.** The energy is converted to joules, divided by the mass of the silicon chip and expressed per hour:

$$DS_i = \frac{E_i \, q}{m} \cdot \frac{10^{6} \cdot 3600}{\Delta t} \quad [\mathrm{\mu Gy/h}]$$

$$q = 1.602176634 \times 10^{-13}$$: MeV to Joules constant.

$m$: the silicon mass (obtained from the detector type).

$C_{i,j}$: Raw files are processed into a table format that has cells: $C_{i,j}$. Meaning $C_{i,j}$ events registered in channel $j$ during exposure $i$.

$n_i$: Table also contain particle counter $n_i$ (the `events_count` column): $$n_i = \sum_{j_{\min}} C_{i,j}$$

$j_{\min}=4$: The first four noise channels. Not included in $n_i$.

$\Delta t$: One exposure block $\Delta t$ is about 10 s.

$S$: the sensitive area of the silicon chip is read from the detector type.

$10^6$: Gy to µGy (constant value in equation).

$3600$: seconds to hours (constant value in equation).

coef0, coef1: obtained from selected calibration.

**Red line**

The red line is a centered moving average over 50 exposures.

---

### Flux Evolution

The particle counter $n_i$ is divided by the sensitive area of the silicon chip $S$ times the length of the exposure $$\Delta t$$.

$$y_i = \frac{n_i}{S \cdot \Delta t} \quad [\mathrm{cm^{-2}\,s^{-1}}]$$

$C_{i,j}$: Raw files are processed into a table format that has cells: $C_{i,j}$. Meaning $C_{i,j}$ events registered in channel $j$ during exposure $i$.

$n_i$: Table also contain particle counter $n_i$ (the `events_count` column): $$n_i = \sum_{j_{\min}} C_{i,j}$$

$j_{\min}=4$: The first four noise channels. Not included in $n_i$.

$\Delta t$: One exposure block $\Delta t$ is about 10 s.

$S$: the sensitive area of the silicon chip is read from the detector type.

**Red line**

The red line is a centered moving average over 50 exposures.

---

### Count Evolution

Particle count per exposure.

$$y_i = n_i$$

$C_{i,j}$: Raw files are processed into a table format that has cells: $C_{i,j}$. Meaning $C_{i,j}$ events registered in channel $j$ during exposure $i$.

$n_i$: Table also contain particle counter $n_i$ (the `events_count` column): $$n_i = \sum_{j_{\min}} C_{i,j}$$

$j_{\min}=4$: The first four noise channels. Not included in $n_i$.

$\Delta t$: One exposure block $\Delta t$ is about 10 s.

**Red line**

The red line is a centered moving average over 50 exposures.



---




## Spectrum Charts

Spectrum charts organize data by energy levels.

![Energy spectrum chart in DOSPORTAL](/DOSPORTAL/img/energy_spectrum.png)

*Energy Spectrum.*

### Energy Spectrum

Energy spectrum organize data by energy levels.

$$x = E_j \quad [\mathrm{MeV}], \qquad y_j = \sum_i C_{i,j} \quad [\text{counts}]$$ (for channel $$j \geq j_{\min}$$)

Two step process described below:

**1. Sum over exposures.** The counts of each channel are summed over every exposure in the window:

$$y_j = \sum_i C_{i,j} \quad [\text{counts}]$$ (for channel $$j \geq j_{\min}$$)

**2. Channel to energy.** The channel number is converted to the energy a single event in that channel deposits:

$$E_j = \mathrm{coef_0} + (j - j_{\min})\,\mathrm{coef_1} \quad [\mathrm{MeV}]$$ (for channel $$j \geq j_{\min}$$)

The point (x-axis) is then plotted at $E_j$ (energy in MeV).


$C_{i,j}$: Raw files are processed into a table format that has cells: $C_{i,j}$. Meaning $C_{i,j}$ events registered in channel $j$ during exposure $i$.

$j_{\min}=4$: The first four noise channels. These channels are excluded from the computation.

**coef0, coef1**: obtained from selected calibration. $\mathrm{coef_0}$ is the energy of the first counted channel and $\mathrm{coef_1}$ the width of one channel.



### Channel Spectrum

See spectrum accross channels.

$$x = j, \qquad y_j = \sum_i C_{i,j} \quad [\text{counts}]$$ (for channel $$j \geq j_{\min}$$)

$C_{i,j}$: Raw files are processed into a table format that has cells: $C_{i,j}$. Meaning $C_{i,j}$ events registered in channel $j$ during exposure $i$.

$j_{\min}=4$: The first four noise channels. These channels are excluded from the computation.

---

## Time window

Selected time segments of the data can be analyzed further.

![Energy spectrum chart in DOSPORTAL](/DOSPORTAL/img/spectrum_time_window.png)

*Time window selected by the user.*

**Blue**: spectrum of full measurement window (default view).

**Yellow**: When a time window is selected, its spectrum is drawn in the accent colour and the full-measurement spectrum is hidden.

### Accumulated Dose

The dose obtained over the selected time window is the mean dose rate of the window multiplied by the length of the window.

The computation reports the following values for the selected window:

- $\overline{DS}$ — mean dose rate $[\mathrm{\mu Gy/h}]$
- $\sigma$ — standard deviation of the dose rate $[\mathrm{\mu Gy/h}]$
- $D$ — dose obtained over the window $[\mathrm{\mu Gy}]$
- $\sigma_D$ — uncertainty of the dose $[\mathrm{\mu Gy}]$
- $T$ — length of the window $[\mathrm{h}]$
- $N$ — number of exposures in the window

$$D = \overline{DS} \cdot T \quad [\mathrm{\mu Gy}]$$

Three step process described below:

**1. Mean dose rate.** The dose rates of all exposures that fall into the window are averaged:

$$\overline{DS} = \frac{1}{N} \sum_{i \in W} DS_i \quad [\mathrm{\mu Gy/h}]$$

**2. Spread of the dose rate.** The sample standard deviation over the same exposures:

$$\sigma = \sqrt{\frac{1}{N-1} \sum_{i \in W} \left(DS_i - \overline{DS}\right)^2} \quad [\mathrm{\mu Gy/h}]$$

For a window that contains a single exposure ($N = 1$) the standard deviation is reported as $0$.

**3. Window length and dose.** The window boundaries are given in milliseconds and converted to hours, the mean dose rate is then integrated over that duration:

$$T = \frac{t_{\mathrm{to}} - t_{\mathrm{from}}}{3.6 \times 10^{6}} \quad [\mathrm{h}]$$

$$D = \overline{DS} \cdot T \quad [\mathrm{\mu Gy}], \qquad \sigma_D = \sigma \cdot T \quad [\mathrm{\mu Gy}]$$

$DS_i$: dose rate in silicon of exposure $i$, computed as described in [Dosage in Silicon](#dosage-in-silicon).

$W$: the set of exposures that fall into the selected time window. The window is taken as given — the selection decides which exposures belong to it.

$N$: number of exposures in the window.

$t_{\mathrm{from}}$, $t_{\mathrm{to}}$: boundaries of the selected window in milliseconds.

$3.6 \times 10^{6}$: milliseconds to hours (constant value in equation).

$\sigma_D$: uncertainty of the dose, the standard deviation of the dose rate scaled by the same duration.

**Note**: $T$ is the length of the window, not the sum of the exposure blocks $\Delta t$ inside it.