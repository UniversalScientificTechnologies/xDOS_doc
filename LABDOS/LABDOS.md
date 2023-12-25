---
layout: page
title: "LABDOS01: Full manual"
parent: LABDOS
permalink: /labdos/LABDOS01
---

# LABDOS01 Operational Manual

## Introduction

LABDOS01 is a lightweight portable ionizing radiation spectrometer-dosimeter intended as an experimental device for laboratory measurements or as a personal dosimeter for frequent flyers. The dosimeter is connected via a USB bus, through which it is powered and read-out. This minimizes the demand for skills required to operate the dosimeter.

![LABDOS01 front and back side](https://raw.githubusercontent.com/UniversalScientificTechnologies/LABDOS01/LABDOS01B/doc/LABDOS01A_merge.jpg)

This device should be used for experimental verification and planning before using our more sophisticated and application-specific devices like SPACEDOS, AIRDOS, or GEODOS.

## Vendor Information 
The LABDOS01 detectors are procured by Universal Scientific Technologies s.r.o. (UST) company. A company specializing in advanced dosimetry and spectrometry equipment. UST is known for its cutting-edge technology and reliable products in the field of radiation detection and measurement. For any further information or support you can contact us via email at support@ust.cz

## Technical Parameters
- Detection element: Silicon PIN diode volume 44 mm³
- Effective number of energy channels: 470 ±3
- Deposited energy ranges: 60 keV to 7 MeV
- Energy measurement resolution: 15 ±2 keV (varies with calibration method and particle type)
- Power supply: 5V via USB-C port or JST-GH connectors
- Radiation spectra integration time: 10 s
- Deadtime: 
  - Up to 1 second for SD card writing
  - 100 ms for data output to USB
- Interface:
  - USB 2.0 USB-C connector (Virtual Com Port baud rate 115200)
  - 3.3V UART link on JST-GH
- Size: 96x56x19mm
- Weight: 80 grams
- Environmental operational conditions:
  - Device protection: IP30 rating
  - Operating temperature range: 0°C to 35°C
  - Operating humidity conditions: non-condensing 20% to 80% RH

## Usage of LABDOS01
### Standalone Detector for Unattended Data Logging
In this type of use, LABDOS01 functions as an autonomous unit, recording data directly to its internal storage in the form of an industrial-grade SLC/SLC mode SD card. This setup is ideal for mid-term environmental monitoring or experiments where continuous human oversight is not feasible. The data is stored on the SD card, which can later be retrieved and analyzed. This application is particularly suitable for fixed installations in labs or for monitoring in remote locations.
This mode is perfect for validating local conditions for future experiments. After initial data collection and analysis, it is recommended to replace LABDOS01 with one of the UST detectors optimized for long-term standalone use, such as GEODOS, AIRDOS, or SPACEDOS detectors. These specialized detectors are tailored for sustained, unattended operations, providing enhanced reliability and data accuracy in various environmental conditions.
Frequent flyers can utilize LABDOS01 in conjunction with a power bank when access to real-time measurements is not available. The device can be connected to a power bank, serving as an energy source, while LABDOS01 continuously logs data to the SD card. This setup is particularly useful for travelers who wish to monitor radiation exposure during flights without the need for immediate data access. Users can upload the data from the SD card to the online platforms, where advanced analysis can be performed to interpret the radiation levels and other relevant metrics. This feature is particularly useful for users who may not have access to sophisticated data analysis software, providing a user-friendly and efficient means of understanding the data captured by LABDOS01.

### Use with Mobile Device or Computer for Data Processing

When connected to a compatible mobile phone or a computer, LABDOS01 serves as a real-time detector and spectrometer. The detector sends data, after each exposition interval, directly to the connected device. This usage is highly beneficial for interactive experiments, educational purposes, or situations where immediate data analysis and visualization are required. The accompanying software on the device can be used for in-depth analysis and graphical representation of the detected particle data, enhancing the understanding and interpretation of the results.

## Basic Usage
### Data Stream Capturing
Reading the data stream from LABDOS01 via USB involves capturing and analyzing the data transmitted from the device to a connected computer or mobile device. The USB data streaming approach is particularly beneficial for mid-term monitoring scenarios where real-time data publication is desired, such as displaying radiation measurements on a website or generating live data feeds for other applications. This method requires dedicated software to handle the data streaming and publishing processes. The software interprets the data stream from LABDOS01 and converts it into a suitable format for online publishing or other forms of output, enabling continuous and dynamic sharing of radiation data in real time. This feature is especially useful in scientific research, public monitoring projects, or educational demonstrations.

### Steps to Read Data Stream
1. Connect LABDOS01 using a USB-C cable.
2. Ensure device recognition and enumeration as a virtual serial line.
3. Launch data logging software (e.g., picocom, minicom, or Putty).
4. Adjust settings in your logging software according to the data format and baud rate (default baud rate is 115200) used by LABDOS01.
5. Start capturing the data stream.

### Important Considerations
- Use the correct data format for specific experiments.
- Use of a high-quality connection cable.

### Recording on SD card
Data in the LABDOS01 are always logged when an SD card is present and functional. The recording of the card is indicated by the illumination of LED2. If the card is inserted and LED2 does not blink between exposures, there might be an issue with the SD card. It's advisable to check the card on a computer. The problem could be due to using an incorrect type of SD card, improper formatting, or damage to the card media.

Note: SD cards in environments with elevated radiation levels may degrade more quickly. Therefore, it's recommended to proactively replace the SD card annually with a suitable and supported type. For information on availability and the correct type of card, contact technical support.

Note 2: The presence and recording of an SD card in LABDOS01 can cause variable deadtime, depending on the condition of the SD card and filesystem. This deadtime can be as long as one second. To minimize deadtime, remove the SD card and log data externally via data stream (USB/UART). This method ensures more continuous data capture with reduced interruptions, making it more suitable for applications where minimizing of deadtime is critical.

## Maintenance
### Basic Maintenance
The LABDOS01 is a low-maintenance device, requiring minimal upkeep when operated within its specified conditions. Adhering to its operational guidelines ensures reliable performance without the need for special maintenance routines.

SD Card: The only consumable component in the detector is the SD card, which is used for data storage. Described in the section above. Regular replacements of the SD card are essential for maintaining the detector's efficiency and reliability.

### Advanced Maintenance

#### Firmware Update

**Updating Process**

  1. Download the Latest Firmware: Access the latest firmware as a release on GitHub or request it directly from the manufacturer.
  1. Connect LABDOS01 to a Computer: Use a USB-C cable for connection.
  1. Initiate Firmware Update: Follow the specific instructions available on the documentation page. Always refer to the online guide for the latest instructions as they may evolve.
  1. Complete the Update: Avoid disconnecting during the update process.


**Additional requirements**

  1. Power Stability: Ensure a quality USB-C cable is used.
  1. Compatibility Check: Verify firmware compatibility with your LABDOS01 model.
  1. Post-Update Testing: After updating, it's important to test the detector to ensure it functions correctly as expected. This step verifies that the update has been successful and the device operates as intended. It can be done by 
  1. connecting a detector to any device, where you can open the serial line terminal.
  1. Remember, the steps outlined here are general guidelines. Always follow the latest online instructions (https://docs.dos.ust.cz/) for accurate and up-to-date procedures.

## Recycling and Disposal
The device constitutes customer electronic waste without additional batteries or another harmful substance.  Dispose of it according to the regulations of your country. The device is RoHS-compliant. 

## Safety Instructions and Warranty
Universal Scientific Technologies s.r.o. shall not be liable for any damages, injuries, or regulatory non-compliance arising from improper use, maintenance, or unauthorized device alterations. Unauthorized interventions in the device or handling that contradict the instructions provided in the manual and detector online documentation will result in the loss of warranty.



