---
layout: page
title: "AIRDOS06: Pocket airliner dosimeter"
permalink: /airdos/AIRDOS06/
parent: "AIRDOS - Atmospheric Radiation sensors"
nav_order: 0
---

# AIRDOS06 - Pocket cosmic radiation spectrometer and dosimeter with neutron detection

AIRDOS06 is a pocket-sized personal cosmic radiation dosimeter and spectrometer for aircrew. It measures the ionizing radiation dose received at flight altitudes using a silicon PIN diode detector and, unlike the other AIRDOS models, detects neutrons as a standard part of its design.

![AIRDOS06](/AIRDOS/img/AIRDOS06.jpg)

The instrument is constructed directly for pilots and cabin crew working at high altitudes, who often change between aircraft. It weighs only 148 g, so it is carried by the person rather than installed in an aircraft. The same unit follows its wearer from one flight to the next, and the dose is recorded for the individual instead of for a particular airframe.

## Applications

* Personal dosimetry of pilots and cabin crew
* Dose tracking across flights on different aircraft
* Cosmic radiation field research at flight altitudes
* Benchmarking and validation of radiation models

## Neutron detection

Neutrons are a significant component of cosmic radiation inside an aircraft. They are produced when primary cosmic rays interact with the atmosphere and the aircraft structure, and a conventional dosimeter cannot easily distinguish them from the much stronger background of directly ionizing charged particles.

AIRDOS06 detects neutrons in its standard configuration, with no accessory required. A thin neutron-conversion layer of lithium-6 (LiF or Li2CO3) is placed on top of the silicon PIN diode. A thermal neutron captured in Li-6 produces a triton and an alpha particle with a well-defined energy (Li-6 + n &rarr; H-3 + He-4). This appears at a characteristic position in the deposited-energy spectrum, where it can be separated from the continuous charged-particle background. The neutron contribution is therefore measured during the flight, not estimated afterwards.

{: .warning }
Neutron detection works reliably only when AIRDOS06 is worn on the body, for example in a chest or leg pocket. The neutron measurement relies on the wearer's body to moderate (slow down) the neutrons so that the conversion layer can register them. When the instrument is placed away from the body, for example in a bag or on a seat or shelf, the neutron signal is not reliable. The measurement of charged particles is not affected by the placement.

This is the main difference from [AIRDOS05](/airdos/AIRDOS05/), where neutron detection is an optional extension that needs a separate carry case with a polyethylene moderator.

## External Dosimeter Display Unit

AIRDOS06 can be used together with the external Dosimeter Display Unit (DDU), which shows the current dose rate and accumulated dose. The DDU is described in the [AIRDOS05](/airdos/AIRDOS05/#external-dosimeter-display-unit) documentation and connects to AIRDOS06 over Bluetooth LE.

### DDU Specification

  * Dimensions: 46 x 35.5 x 9.5 mm
  * Display:
    * Resolution: 200(H) × 200(V)
    * Active Area: 27 × 27 mm
  * Power supply:
    * Battery LiPo Battery 3.7V 200mAh
    * USB charging
    * 24-hour endurance after charging
  * Data interface:  Bluetooth LE 5.0
  * Mass: 13g

## Technical parameters

 * Detection element: silicon PIN diode, volume 44 mm³, with a Li-6 (LiF/Li2CO3) neutron converter layer
 * Deposited energy range: 40 keV to 80 MeV
 * Data storage device: SD card (~1 GiB), FAT filesystem, human-readable log format
 * Charging: USB-C
 * Battery endurance: at least 5 days
 * DDU interface: Bluetooth LE 5.0
 * Dimensions: approx. 80 x 70 x 20 mm (± 5 x 3 x 2 mm)
 * Mass: 148 g

---
_Note: Technical specifications are subject to change without prior notice as we continuously improve our devices. Any changes are made to enhance performance, usability, or compliance._
