---
layout: page
title: UST Dosimeters file format
permalink: /xdos_format
---

# Particle Detector Output File Format - Version 1

## Introduction

This document describes the output file format for the AIRDOS and LABDOS series of particle detectors. The file is formatted in plain text, which not only facilitates easy readability by humans but also allows for quick and efficient machine parsing. This format is particularly designed to accommodate multiple logs (detector cycles) within a single file, enabling these logs to be segmented into individual logs for detailed analysis. The current version of this file format is actively in use.

## File Structure

The output file is composed of various data messages, each representing different types of data captured by the detector. The structure of these lines is as follows:


### Data format Identifier
Not implemented yet

### Detector Identifier

- **Format**: `$DOS, [DetectorModel], [FirmwareVersion], [Bulid number], [SerialNumber], [BuildUniqueId], [Build origin], [SN]`
- **Example**: `$DOS,AIRDOS04A,1.0.1-0-User,0,1905b9179096e859818e6010ad4eb126c2f0222c,User,1290c00806a20091c449a000a0000038`
- **Description**: Identifies the detector model, firmware version, a unique identifier for the device, user information, and session ID.

### Digital part identifier

- **Format**: `$DIG, [ModuleType], [SerialNumber], [Reserved]`
- **Example**: `$DIG,BATDATUNIT01B,1290c00806a200926049a000a00000c9,ffff`
- **Description**: 

### Analog-to-Digital Conversion (ADC) Readings

- **Format**: `$ADC, [SensorType], [SerialNumber], [Reserved]`
- **Example**: `$ADC,USTSIPIN03A,1290c00806a20091c449a000a0000038,7844`
- **Description**: 

### Histogram Data

- **Format**: `$HIST, [message number], [time], ..., [Value1], [Value2], ...`
- **Example**: `$HIST,0,12.8,8,255,...`
- **Description**: A detailed histogram representing the distribution of detected events or measurements across various categories.

## Notes

- The plain text file format ensures compatibility and ease of parsing for both humans and machines.
- This format is currently in use and represents the latest data output in UST detectors.
- Each line type in the file serves a specific purpose in capturing and representing data from the particle detector.
