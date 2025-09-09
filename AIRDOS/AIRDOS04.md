---
layout: page
title: "AIRDOS04: Airliner radiation dosimeter"
permalink: /airdos/AIRDOS04
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
_Note: Technical specifications are subject to change without prior notice as we continuously improve our devices. Any changes are made to enhance performance, usability, or compliance._

See [changelog](https://docs.dos.ust.cz/airdos/AIRDOS04/manual#product-changelog) for information about hardware revisions and version-specific features.

# Examples of data

AIRDOS04 has been extensively tested on multiple scientific missions including particle accelerators or experimental compagins. 

## Verification on artificial radiation sources

![Fragments in HIMAC beam detected by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_HIMAC_fragments.png)

![CERF mixed field radiation spectra by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_CERF_spectra.png)

## Flight-data

![Measured doserate during flight by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_doserate.png)

![Measured radiation spectra during flight by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_radiation_spectra.png)

![Environmental variables by AIRDOS04](https://raw.githubusercontent.com/UniversalScientificTechnologies/AIRDOS04/refs/heads/AIRDOS04C/doc/img/AIRDOS04_flight_environment.png)



