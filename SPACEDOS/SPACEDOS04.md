---
layout: page
title: "SPACEDOS04: Personal Active Dosimeter"
parent: "SPACEDOS - Space radiation detectors"
permalink: /spacedos/SPACEDOS04
nav_exclude: true
---

# SPACEDOS04 - Personal Active Dosimeter for manned deep space missions

{: .warning }
SPACEDOS04 is currently under development. Parameters listed below are design targets and may change before the flight model is finalized.

SPACEDOS04 is a wearable radiation dosimeter for manned deep space and ISS missions, measuring ionizing radiation dose received by an astronaut using a silicon PIN diode detector combined with passive detectors (TLD and nuclear track detectors). It forms a Space Dosimeter Unit (SDU) together with a wristwatch-style Display and Data Unit (DDU) that provides real-time dose readout.

The device is being developed and flight-tested as part of the [CZPAD experiment](https://ceskacestadovesmiru.cz/czpad/) onboard the International Space Station (ISS), which serves as the qualification path towards a flight-proven, deployable instrument.

## System overview

Each SDU consists of a SPACEDOS04 electronic dosimeter, a set of passive detectors (TLD and nuclear track detectors), and a Nomex pouch for mechanical protection and flame retardancy. The SDU can be attached to the cosmonaut's body (waist strap, chest strap, thigh strap) or to the ISS structure (hook & loop adhesive pads).

## Hardware

The SPACEDOS04 electronics consists of three PCBs:

* **Baseboard** - MCU, Battery Management System (BMS), and a Bluetooth Low Energy RF interface to the DDU wristwatch display
* **Sensor board** - silicon PIN diode detector and the analogue signal processing chain
* **Flex PCB** - mechanical and electrical interconnect between the baseboard, sensor board, and the Li-ion battery cell

## Parameters (design targets)

* Silicon PIN diode detector, at least 28 x 28 x 0.5 mm³, with a full-area LiF neutron converter layer
* Deposited energy range: 50 keV to 100 MeV (the 50 keV lower bound is set by the ²⁴¹Am 59.5 keV calibration line)
* Aluminium shielding of the diode: 6 mm on the sides
* Data storage device: SD card (~1 GiB), FAT filesystem, human-readable log format
* Charging: USB-C
* Battery endurance: at least 5 days
* Dimensions (without pouch): approx. 80 x 70 x 20 mm (± 5 x 3 x 2 mm)
* Mass: estimated 148 - 184 g (SDU including battery cell and shielding, excluding pouch)
* Maximum temperature while charging: 45 °C
* Vibration resistance per Crew Dragon / ISS JSC-20793 requirements

