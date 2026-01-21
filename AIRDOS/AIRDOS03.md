---
layout: page
title: "AIRDOS03: The Drone-Compatible Detector"
permalink: /airdos/AIRDOS03
parent: AIRDOS
nav_order: "9"
---


# AIRDOS03 - Lightweight airborne dosimeter and spectrometer

[AIRDOS03](https://docs.thunderfly.cz/avionics/AIRDOS03/), also called “UAVDOS”, is a semiconductor ionizing radiation sensor developed in cooperation with [ThunderFly s.r.o.](https://www.thunderfly.cz/) as a measuring device for the [TF-ATMON](https://docs.thunderfly.cz/instruments/TF-ATMON) measuring toolchain. The detector is designed to be lightweight and capable of connecting to a wide range of unmanned drone flight controllers. 
Design meet requirements for TF-ATMON’s sensors and therefore can share a power supply, data storage, or telemetry link with common drone avionics. This eliminates excess weight that would otherwise have to be carried by the drone, thereby decreasing the flight range or duration and lowering flight parameters. The particle detector is, at the same time, compatible with the [Pixhawk](https://www.pixhawk.org/) standard for connecting devices to drones.

![AIRDOS03 sensor electronics](https://raw.githubusercontent.com/ust-modules/USTSIPIN03/refs/heads/USTSIPIN03C/doc/img/AIRDOS04_sensor_top.png)

The [TF-ATMON](https://www.thunderfly.cz/tf-atmon.html) system, in combination with the sensor, enables the search for areas with increased radiation intensity and optimally utilizes flight time to collect high-quality data. Refer to [ThunderFly's AIRDOS03 documentation](https://docs.thunderfly.cz/avionics/AIRDOS03/) for more details. 

## Key Features

* Fully compatible with [TF-ATMON](https://docs.thunderfly.cz/instruments/TF-ATMON) and Pixhawk ecosystem
* Lightweight and extremely low-power (5 V / 3 mA)
* Spectral data output for scientific analysis
* Can operate in real-time streaming mode or store data onboard
* Modular open-source firmware for custom scientific missions

## Applications

* Unmanned atmospheric radiation surveys
* Detection of increased ionizing radiation in convective storm regions
* Mapping radiation gradients near ground-based or airborne sources
* Scientific support for space weather and high-altitude dosimetry research

## Technical parameters

* Measurement of the deposited energy of ionizing radiation in the 40 keV to 80 MeV
* Energy resolution 15 ±2 keV per channel (firmware-dependent)
* Effective number of energy channels: ~65000
* 44 mm³ detection volume
* Radiation spectra integration time: 10 s (configurable by firmware)
* Environmental sensors
  * Relative Humidity 0 to 100 %RH (accuracy 2	%RH)
  * Temperature -40 to 125 °C (accuracy 0.5 °C)
* Lightweight, compact electronics
  * 71 × 51 × 25 mm
  * 40 grams
* Interface options: UART (JST-GH - Pixhawk-compatible)
  * UART could be converted to USB-C by [TFUSBSERIAL01](https://docs.thunderfly.cz/avionics/TFUSBSERIAL01/)
  * Device suitable for real-time spectrum measurement and in-flight data logging.

AIRDOS03 provides TELEM/UART connectivity. The UART interface is compatible with the [Pixhawk connector standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf) and enables integration with onboard telemetry systems or flight controllers.

### UART Pinout

| Signal | Pixhawk Color                            | ThunderFly Color                                              |
| ------ | ------------------------------------------------- | ---------------------------------------------- |
| +5V    | ![Red](https://user-images.githubusercontent.com/5196729/102204855-ab1c3300-3eca-11eb-8083-646d633e3aef.png) Red     | ![Red](https://user-images.githubusercontent.com/5196729/102204855-ab1c3300-3eca-11eb-8083-646d633e3aef.png) Red       |
| RX     | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![White](https://user-images.githubusercontent.com/5196729/102204632-5e385c80-3eca-11eb-985d-a881acfae26a.png) White   |
| TX     | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Green](https://user-images.githubusercontent.com/5196729/102205114-04846200-3ecb-11eb-8eb8-251c7e564707.png) Green   |
| CTS    | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Blue](https://user-images.githubusercontent.com/5196729/102205102-ffbfae00-3eca-11eb-9372-8406f7a4aa9d.png) Blue     |
| RTS    | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Yellow](https://user-images.githubusercontent.com/5196729/102204908-bc653f80-3eca-11eb-9a1d-a02ea5481c03.png) Yellow |
| GND    | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black   |

### TF Payload connector

These signals provide additional functions, including synchronization or inter-device communication. This connector is primarily intended for time synchronization with the [TFGPS01 GNSS module](https://docs.thunderfly.cz/avionics/TFGPS01/), which provides PPS and time pulse signals on "Payload Connector".

| Signal    | Pixhawk Color                | ThunderFly Color                                  |
| --------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| TIMEPULSE | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Blue](https://user-images.githubusercontent.com/5196729/102205102-ffbfae00-3eca-11eb-9372-8406f7a4aa9d.png) Blue     |
| EXTINT    | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Yellow](https://user-images.githubusercontent.com/5196729/102204908-bc653f80-3eca-11eb-9a1d-a02ea5481c03.png) Yellow |
| GPIO | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![White](https://user-images.githubusercontent.com/5196729/102204632-5e385c80-3eca-11eb-985d-a881acfae26a.png) White   |
| SDA       | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Green](https://user-images.githubusercontent.com/5196729/102205114-04846200-3ecb-11eb-8eb8-251c7e564707.png) Green   |
| SCL       | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Yellow](https://user-images.githubusercontent.com/5196729/102204908-bc653f80-3eca-11eb-9a1d-a02ea5481c03.png) Yellow |
| TX        | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![White](https://user-images.githubusercontent.com/5196729/102204632-5e385c80-3eca-11eb-985d-a881acfae26a.png) White   |
| RX        | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Green](https://user-images.githubusercontent.com/5196729/102205114-04846200-3ecb-11eb-8eb8-251c7e564707.png) Green   |
| GND       | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black | ![Black](https://user-images.githubusercontent.com/5196729/102205213-28e03e80-3ecb-11eb-95bb-7ba207360541.png) Black   |

## Mechanical design

The instrument consists two PCBs connected by standard 2.54 mm pitch 15x2 pin-header. The pin-header could be the both straight or angled, depending of the desired "L" or parallel "II" PCB configuration. In case of parallel mounting the PCBs are separated by a screw collumns. 

![AIRDOS03 data processing board dimensions](https://raw.githubusercontent.com/ThunderFly-aerospace/TFUNIPAYLOAD01/refs/heads/TFUNIPAYLOAD01B/doc/img/TFUNIPAYLOAD01_dimensions.png)

![AIRDOS03 sensor board dimensions](https://raw.githubusercontent.com/ust-modules/USTSIPIN03/refs/heads/USTSIPIN03C/doc/img/AIRDOS04_dimensions.png)

## Output data format

The data are produced as continuous data stream on the UART port. The default firmware generates [MAVLink Tunnel packets](https://mavlink.io/en/services/tunnel.html), eliminating the need to modify autopilot firmware. This solution is suited for rapid deployment and testing of new environmental or scientific sensors connected autopilot without firmware development. It provides a plug-and-play bridge between your sensor and [TF-ATMON ecosystem](/instruments/TF-ATMON/).

Alternatively the device could output [Particle Detector Output File Format](/xdos_format) common for SPACEDOS, AIRDOS and GEODOS instruments. 



