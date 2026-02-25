---
layout: page
title: DOSPORTAL
permalink: /dosportal/
parent: Tools and resources
has_children: true
nav_order: 7
---


# DOSPORTAL

## Introduction

DOSPORTAL is a cloud-based dosimetry tool developed by [UST](https://www.ust.cz/), designed to facilitate the visualization and management of logs from radiation sensors. This documentation is intended for users of DOSPORTAL, frequent flyers, scientists working with ionising radiation detectors, to IT professionals responsible for institutional system integration and management. Our goal is to provide you with a tool that will enable you to leverage all the features of UST's dosimeters.

DOSPORTAL is primarily designed for use with UST's particle detectors: [LABDOS](/labdos), [AIRDOS](/airdos), and [GEODOS](/geodos). 

{: .warning }
> Please note that DOSPORTAL is currently in a development phase and is not yet publicly available. For more updates about the schedule, please contact us.

### Overview of DOSPORTAL

DOSPORTAL simplifies the process of managing and analyzing data obtained from ionising radiation detectors. Thanks to visualization tools and a user-friendly interface, DOSPORTAL allows users to gain insights from their data quickly. The platform supports a range of data log formats and offers multiple options for their processing, from predefined filters to custom analysis using custom plugins.

![image](https://github.com/UniversalScientificTechnologies/xDOS_doc/assets/5196729/6b18ef7f-3251-4674-94ab-62444ec7ba43)
> Preview from DOSPORTAL record page. 

## Fast glossary
Brief overview of the  main elements of DOSPORTAL

- **Record**: This term refers to the smallest unit of measurement within DOSPORTAL. A record corresponds to a single time series obtained from a detector. The key attributes of a record include:
  - **Log File**: Filename obtained from device
  - **Time Tracking (Yes/No)**: Indicates whether the log is timestamped, meaning if it could be placed on a real-time axis.
  - **Start Time**: If time is tracked, the beginning time of the log is required.
  - **Detector**: Identified automatically for logs supporting detector identification. Assumes the detector is already registered in the system.
  - **Calibration**: Automatically applies the latest available calibration from the associated detector.

