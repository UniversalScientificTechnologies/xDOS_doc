---
layout: page
title: "AIRDOS04: Airliner radiation dosimeter"
permalink: /airdos/AIRDOS04/
parent: AIRDOS
nav_order: "1"
has_children: true
---


# AIRDOS04 - Airborne radiation dosimeter and spectrometer

AIRDOS is a state-of-the-art cosmic radiation dosimeter and spectrometer unit. It is intended for long-term airborne measurement of cosmic radiation and dosimetry in mixed ionizing radiation fields on board aircraft.

![AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/AIRDOS04A/doc/img/AIRDOS04.jpg)

The instrument is designed primarily for the dosimetry of cabin crew and commercial flight attendants. Thanks to its design of detachable data storage and power source from accumulators, the required maintenance time is minimal. The calibrated AIRDOS04 detector can be placed on board continuously, and it is only necessary to  replace the accumulator/storage module according to the set maintenance interval.

[Get started now]({{site.baseurl}}/airdos/AIRDOS04/quickstart){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

**Vendor Information**: The AIRDOS04 detectors are procured by [Universal Scientific Technologies s.r.o.](https://www.ust.cz/) (UST) company. A company specializing in advanced dosimetry and spectrometry equipment. UST is known for its cutting-edge technology and reliable radiation detection and measurement products. For more details about the company and its officers, please visit their website at [www.ust.cz](https://www.ust.cz/). For any further information or support, you can contact us [via email](https://www.ust.cz/about/#email).

# Technical parameters

 * Detection element: Silicon PIN diode, volume 44 mm³
 * Effective number of energy channels: ~65000
 * Deposited energy range: 40 keV to 80 MeV
 * Energy measurement resolution: 15 ±2 keV
 * Service interface and charging source: USB-C connector
 * Energy source: Up to five 18650 Li-ion cells with 64 Wh in total. That conforms [≤ 100 Wh / 2g IATA restrictions](https://www.iata.org/contentassets/6fea26dd84d24b26a7a1fd5788561d6e/passenger-lithium-battery.pdf)
   * Can also be operated without accumulators completely with the use of an aircraft's on-board USB power source. 
 * Radiation spectra integration time: 10 s
 * Environmental sensors
   * Relative Humidity 0 to 100 %RH (accuracy 2	%RH)
   * Temperature -40 to 125 °C (accuracy 0.5 °C)
   * Barometric pressure 1 to 120 kPa (accuracy 150 Pa)
 * Maintenance interval: ~1 month (data download, accu pack change)
 * Maintenance duration: under 5 minutes
 * Size: 166 x 107 x 57 mm (two  of these should fit into the Aircraft printed manual bay)
 * Weight is 0.88 kg (With five Li-ion accumulator cells in [BATDATUNIT01](https://docs.dos.ust.cz/airdos/BATDATUNIT01))
   * 0.62 kg without Li-ion accumulators  
 * Environmental operational conditions
   * Device protection: IP30 rating (fully assembled)
   * Operational and storage temperature range: 0°C to 50°C (32°F to 122°F)
   * Operational humidity conditions: non-condensing, 20% to 80% RH

---
_Note: Technical specifications are subject to change without prior notice as we continuously improve our devices. Any changes are made to enhance performance, usability, or compliance. See [changelog](https://docs.dos.ust.cz/airdos/AIRDOS04/manual#product-changelog) for information about hardware revisions and version-specific features._

# Examples of data

AIRDOS04 has been verified in well‑characterized reference radiation fields, during operational airline flights, and on stratospheric balloon campaigns. The following sections demonstrate the instrument’s capabilities in mixed fields dominated by charged particles.

## Verification on artificial radiation sources

AIRDOS04 has undergone beam/field exposures at the following facilities :

* **HIMAC (Heavy‑Ion Medical Accelerator in Chiba, Japan)** — a clinical/research synchrotron complex delivering high‑energy heavy‑ion beams with precise energy and intensity control. It is widely used to study fragmentation and dosimetry in well‑defined mono‑species beams.
* **CERF at CERN (CERN‑EU High‑Energy Reference Field)** — a *mixed* high‑energy hadron field created from secondary particles in a controlled geometry, routinely used to benchmark dosimeters and spectrometers in conditions representative of aviation altitudes.

These facilities let us test AIRDOS04 in both mono‑energetic/mono‑species and mixed‑field scenarios.

![Fragments in HIMAC beam detected by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_HIMAC_fragments.png)
*HIMAC exposure: heavy‑ion interactions and nuclear fragmentation features are visible at high deposited energies, confirming the spectrometric response and dynamic range.*

![CERF mixed field radiation spectra by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_CERF_spectra.png)
*CERF exposure: spectrum measured in a standardized mixed high‑energy field; spectral shape and rates are consistent with the reference field characterization.*

### Energy calibration (Am‑241 & Pu‑239)

The each produced AIRDOS04 unit is individually energy‑calibrated using two reference sources, Am‑241 and Pu‑239. A calibration protocol is supplied with every delivered instrument.

![Energy calibration with Am‑241 and Pu‑239](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_Am-241_Pu-239.png)
*Energy‑calibration spectrum from a typical unit. Labeled lines correspond to distinct radiation types and serve as fixed points for the channel‑to‑energy conversion.*

Identified energies and radiation types:

* **59.5 keV (γ from Am‑241):** Low‑energy gamma line used as the lowest-energy calibration anchor; in silicon it produces a well‑defined full‑energy peak (dominated by photoelectric absorption), validating the low‑noise of spectrometer.
* **5.486 MeV (α from Am‑241):** High‑energy alpha‑particle line; alphas of this energy stop within tens of micrometres in Si and deposit essentially their full energy, providing a sharp peak for the MeV‑range anchor and resolution check.
* **5.15 MeV (α from Pu‑239):** Second alpha line near the Am‑241 peak; the ≈0.336 MeV separation between the two alpha lines is a sensitive cross‑check of the energy scale and spectral resolution.

These three lines jointly establish the keV‑per‑channel calibration and verify the detector’s linearity from tens of keV up to several MeV.

## Flight-data

During routine operations, AIRDOS04 records the typical evolution of the cabin radiation environment. The figures below show a representative flight where the dose rate rises with climb, levels at cruise, and decreases on descent; the spectral content and environmental variables (pressure, temperature) evolve accordingly.


![Measured doserate during flight by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_doserate.png)

*Dose‑rate vs. time along the flight profile.*

> * Flight duration: 11 h, number of spectral measurements: 3854.
> * Dose in silicon over the flight: 14.444 μGy ± 1.132 μGy.


![Measured radiation spectra during flight by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_radiation_spectra.png)
*In‑flight deposited‑energy spectra.*


![Environmental variables by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_flight_environment.png)
*Concurrent pressure and temperature records provide context for ascent/cruise/descent phases and help correlate aircraft flight-phases with radiation trends.*



