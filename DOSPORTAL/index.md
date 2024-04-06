---
layout: page
title: DOSPORTAL
permalink: /dosportal/
has_children: true
---


# DOSPORTAL

## Introduction

DOSPORTAL is an innovative cloud-based tool developed by UST, designed to facilitate the visualization and management of logs from particle detectors. This documentation is intended for all users of DOSPORTAL, ranging from technicians and scientists working with particle detectors to IT professionals responsible for system integration and management. Our goal is to provide you with a comprehensive guide that will enable you to fully leverage all the features and capabilities that DOSPORTAL offers.

DOSPORTAL is primarily designed for use with UST's particle detectors: [LABDOS](/labdos), [AIRDOS](/airdos), and GEODOS. You can learn more about these detectors in other sections of this documentation or on the [official website](https://www.ust.cz/UST-dosimeters/).

{: .warning }
> Please note that DOSPORTAL is currently in an active development phase and is not yet publicly available. The anticipated launch of the service to the public in a test version is scheduled for Q3 2024.


### Purpose of the Documentation

This documentation has been created with the objective to:

- Provide users with clear and structured information on how to get started with DOSPORTAL.
- Offer detailed guides and best practices for efficient visualization, management, and analysis of logs.
- Explain advanced features and integration with other tools or services.
- Ensure answers to common questions and solutions to typical problems users may encounter.

### Overview of DOSPORTAL

DOSPORTAL is a cloud platform that simplifies the process of managing and analyzing data obtained from particle detectors. Thanks to advanced visualization tools and a user-friendly interface, DOSPORTAL allows users to quickly gain deeper insights from their data. The platform supports a wide range of log formats and offers flexible options for their processing, from predefined filters to custom analysis using integrated tools.

Whether you need to quickly check outputs from a detector, analyze complex data sets, or integrate data with other applications, DOSPORTAL provides all the necessary tools and functionalities for efficient management of your particle data.


![image](https://github.com/UniversalScientificTechnologies/xDOS_doc/assets/5196729/6b18ef7f-3251-4674-94ab-62444ec7ba43)
> Preview from DOSPORTAL record page. 


## Fast glosary
Brief overview of main elements of DOSPORTAL

- **Record**: This term refers to the smallest unit of measurements within DOSPORTAL. A record corresponds to a single log (file) obtained from a detector. The key attributes of a record include:
  - **Log File**: File obtained from device
  - **Time Tracking (Yes/No)**: Indicates whether the log is timestamped, meaning if it's placed in real time. Set 'No' for "laboratory" measurements. 
  - **Start Time**: If time is tracked, the beginning time of the log is required.
  - **Detector**: Identified automatically for logs supporting detector identification. Assumes the detector is already registered in the system.
  - **Calibration**: Automatically applies the latest available calibration from the associated detector.

- **Measurement**: 
