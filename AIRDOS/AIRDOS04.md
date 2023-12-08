---
layout: page
title: AIRDOS04
permalink: /airdos/AIRDOS04
parent: AIRDOS
---


# AIRDOS04

AIRDOS04 is a state-of-art cosmic radiation dosimeter and spectrometer unit. It is intended for long-term airborne measurement of cosmic radiation and dosimetry in mixed ionization fields on board aircraft.

![AIRDOS04_render_001](https://github.com/roman-dvorak/xDOS_doc/assets/5196729/2687c5f5-7647-4756-b735-521b06e7acf6)


The instrument is designed primarily for the dosimetry of cabin crew and flight attendants of commercial flights. Thanks to its design of detachable data-storage and power-source/accumulators, required maintenance time is minimalized. AIRDOS04 detectors can be placed on-board continuously and it is necessary to replace the accumulator/storage module according to the set maintenance interval.

# Technical parameters
 * Detection element: Silicon PIN diode, volume 44 mm3
 * Effective number of energy channels: 470 ±3 or more
 * Deposited energy range: 60 keV to 7 MeV
 * Energy measurement resolution: 15 ±2 keV or better
 * Service interface and energy source: USB-C PD 2.0 connector
 * Radiation spectra integration time: 10 s
 * Maintenance interval: ~1 month 
 * Maintenance duration: under 5 minutes
 * Size: 166 x 107 x 57 mm
 * Device protection: IP30 (in fully assembled state)
 * Weight:
   * Detector unit:   xxx g
   * Battery module:  xxx g
   * Direct-power module:  xxx g
   * Complete solution with accumulator module:
   * Complete solution with external power module:

# Components and Their Functions

## AIRDOS04 - Detection part
The detection part of the AIRDOS04B represents the core of its abilities, designed to provide high sensitivity and precision in cosmic radiation detection. This part of the whole assembly is permanently embedded within an aluminum box, which ensures mechanical durability and protects the sensitive components within.

The detection part consists of the following key components:

**Analog Part**: This segment contains the high sensitive analog electronics necessary for processing signals from the sensing element. It's optimized to minimize noise and maximize sensitivity, crucial for accurate radiation measurement.

**Sensing Element - PIN Diode**: Sensing element of the detection part is a semiconductor PIN diode. Selected for its ability to effectively detect ionizing radiation with high accuracy by absorbing particle energy, the diode is positioned under the top side of the box. Its precise location is clearly marked on the top print of the casing, guiding proper orientation during installation.

**Digitization Section**: Analog signals are converted into digital data. This process ensures that the captured data is accurate and detailed enough for quality measurements and real-time signal processing.

The design and structural features of the AIRDOS04B's detection part are meticulously crafted to ensure both durability and high performance in cosmic radiation detection. Detection components are permanently in-build within a robust aluminum casing. This casing provides exceptional mechanical resistance, protecting the sensitive internal components from external impacts and environmental stressors, thereby ensuring the longevity and reliability of the detector.

In this design, the detection part is fixed and non-removable, contrasting with the easily insertable data storage and power modules. This fixed installation is critical as it maintains the integrity and calibration of the sensitive components, ensuring consistent performance over the operational life of the detector. On the top side of the box is clearly marked the precise location of the sensing element underneath, guiding proper orientation and installation.

The detector is designed to allow for easy insertion of data storage and power modules. This feature is particularly beneficial for quick maintenance, data module replacement, enabling these maintenance tasks to be completed efficiently without disturbing the detector's core components.

## AIRDOS04 Digital, Data Storage and Power Module
The AIRDOS04B, designed with efficiency and modularity in mind, separates its detection capabilities from its data storage and power supply functions. These functions are executed through interchangeable modules, which also act as processor units with firmware, data storage with high capacity and power source. 
The separation of the data storage and power supply from the detection part results from a desire to enhance the flexibility and ease of maintenance of the AIRDOS04B detector. By compartmentalizing these functions, the detector allows for easier upgrades, maintenance, and customization based on specific user needs or changing technological advancements. 

The concept of an interchangeable digital part significantly reduces the maintenance time required to keep the detector operational. Maintenance on-site (such as on-board aircraft) involves swapping the digital part with another unit that is pre-prepared with a cleared data storage and properly charged batteries.
All the firmware for the detector is also located in this digital part. This is to ensure that firmware updates can be conducted out of the detection site, off the aircraft, so that the time required for regular maintenance is not extended by firmware updates.

# Available variants of digital part:

## BATDATUNIT01-EXT - External power source type 

The digital/data module without an accumulator in the AIRDOS04B detector represents a streamlined and efficient approach to data management and power supply. Designed for environments where a continuous external power source is readily available, this module prioritizes data handling and processing capabilities while relying on external power, through a USB-C connection.

This module contains the critical digital components and firmware of the AIRDOS04B. Its design facilitates efficient data management, allowing for quick data transfer and analysis when connected to a computer or other devices. The absence of an accumulator is useful in cases where you need to put a detector in places where lithium cells are permitted.

The integrated data storage of the detector is accessible as a mass-storage device via the USB-C interface. This feature provides fast and user-friendly access to the internal storage, without requiring any external memory readers. More information about initialization of mass-storage mode is written in “Device operations” part of this manual. 

## BATDATUNIT01-BAT - With integrated battery power source

The accumulator module of the AIRDOS04 detector, above the non-accumulator version (BATDATUNIT01-EXT), offers an integrated energy storage solution. This module is equipped with five lithium-ion cells housed in 18650 battery cases, providing a significant power capacity that can sustain the detector's operation for approximately one month. 
It can be continuously connected to a USB-C power supply, functioning similarly to an Uninterruptible Power Supply (UPS). In scenarios where external power supply experiences fluctuations or outages, the accumulator module ensures that the AIRDOS04B continues to operate without interruption, maintaining consistent data collection and detector functionality.



