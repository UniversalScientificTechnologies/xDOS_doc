---
layout: page
title: DEMODOS
permalink: /demodos/
has_children: true
has_toc: false
---

# DEMODOS: Remote-Controlled Dosimeter Simulator for Training and Education

DEMODOS is a sophisticated dosimeter emulator designed to simulate radiation exposure in controlled training environments. Developed for educational and training purposes, the system allows users to simulate radiation risks without exposing participants to real radiation hazards. This tool is ideal for training personnel in scenarios requiring familiarity with radiation safety protocols, such as emergency response teams or nuclear facility staff.


![SPACEDOS PAD with Dosimeter Display Unit](https://github.com/user-attachments/assets/acbfe5dc-d8ca-4c22-b7dc-aa1cb41bda3a)

## Overview

The DEMODOS system provides a flexible, safe, and remote-controlled system for simulating radiation exposure. DEMODOS is particularly useful for training scenarios where real radioactive sources cannot be used for safety reasons. The system is designed to enhance the learning experience by simulating real-world scenarios involving radiation exposure while ensuring complete safety for participants.

## Key Features

- **Realistic Radiation Simulation**: DEMODOS allows to emulate various radiation exposure scenarios, allowing users to simulate different levels of radiation intensity in real-time.
- **Remote Operation**: The system is entirely remote-controlled, meaning that no real radioactive sources are involved, ensuring maximum safety for participants.
- **Multi-User Capability**: DEMODOS supports multiple users, enabling team-based exercises where each interacts with their simulated dosimeter.

## Components of DEMODOS

### 1. Personal Active Dosimeter (PAD) Emulator
The **PAD emulator** replicates the functions of a real personal dosimeter, monitoring, and recording simulated radiation levels in real time. Participants can wear this device during exercises, mimicking the experience of tracking radiation exposure in field conditions.

![SPACEDOS Personal Active Dosimeter](https://github.com/user-attachments/assets/1ad55b66-e335-4a74-a256-f7421073e868)

### 2. Dosimeter Display Unit (DDU)
The **DDU** is a wristwatch-like display unit similar to a smartwatch. It shows current simulated radiation levels as detected by the PAD emulator and provides real-time feedback, ensuring that participants can monitor their "exposure" throughout the exercise.

![SPACEDOS Dosimeter Display Unit](https://github.com/user-attachments/assets/b3888b79-f818-4eb6-a282-9b013ce5907d)


## System Specifications

### PAD Emulator Specifications
- **Dimensions**: 98x69x22 mm 
- **Charging Interface**: USB-C
- **Battery Life**: Up to 20 hours at 15-second update intervals
- **Weight**: 74g
- **Ingress Protection**: IP40

### DDU Specifications
- **Form Factor**: Wrist-watch display unit
- **Display**: Digital readout of current radiation levels
- **Vibration Motor**: Alerts users when critical radiation levels are simulated
- **Messaging Capability**: Displays important scenario updates from the control center

## Software

The DEMODOS system is controlled through a software [TUI interface](https://en.wikipedia.org/wiki/Text-based_user_interface) written in Python. The software provides mission operators the ability to simulate radiation levels and control what is displayed on each participant's DDU and PAD. The software also includes features to simulate stochastic noise, making the experience more realistic. The software is intended to be run on the server available to the DEMODOS devices over the wifi network. Mission operators control the software through the [SSH](https://en.wikipedia.org/wiki/Secure_Shell) protocol running the user interface application. 

![Demodos operator interface](https://github.com/user-attachments/assets/b746ed27-2748-4429-8d20-bde783a12b54)

### Features:
- **TUI Interface**: Provides clear and efficient controls for simulation management.
- **Noise Simulation**: Adds realistic fluctuations to the simulated data, mimicking the natural variations in radiation measurements encountered in real-world situations.
- **Remote Control**: The system can be operated entirely remotely over a Wi-Fi network, making it suitable for a wide range of training environments. This capability allows for the easy integration of DEMODOS into various training scenarios, such as mock hazardous events or exercises conducted in large facilities.

## Use Cases

DEMODOS is ideal for:

- **Training for space missions (SPACEDOS version)**: The SPACEDOS variant of DEMODOS is designed to simulate radiation exposure on spacecraft in Earth orbit or during interplanetary missions. Astronauts can practice procedures for identifying optimal locations to shield themselves from harmful cosmic radiation, particularly during solar events like Coronal Mass Ejections (CME).
  
- **Simulating radiation events on Earth**: DEMODOS enables exercises related to potential radiation leaks from industrial or energy facilities. Trainees can simulate decision-making processes during such incidents, affecting the course of the exercise based on their actions and strategies for minimizing radiation exposure.

- **Educational purposes**: DEMODOS is a valuable tool for institutions focusing on nuclear physics, radiology, or emergency preparedness. It provides a safe, controlled environment for learning about radiation, its effects, and proper safety protocols.

The simulator can be adapted for various scenarios, including simulating hotspots with higher radiation exposure, safe zones, and areas with gradual increases in radiation levels. Each participant’s data is tracked individually, allowing for detailed post-exercise evaluations.

## Safety and Benefits

One of the most significant advantages of DEMODOS is that it allows for realistic radiation risk training without the dangers associated with real radioactive sources. The remote operation of the system ensures complete safety, making it an essential tool for training environments where real radioactive exposure would be impractical or hazardous.

- **No Actual Radiation Exposure**: Since all radiation is simulated, there is no risk of participants being exposed to dangerous levels of radiation during training.
- **Realistic Learning Environment**: Despite the lack of actual radiation, DEMODOS provides a highly realistic simulation, ensuring effective and practical learning outcomes.

## Flexibility and Customization

The DEMODOS system is highly flexible and scalable, making it adaptable to a wide variety of training environments and user requirements. It can be expanded in terms of the number of client dosimeters as well as the area covered by the system. Whether you are simulating radiation in a confined industrial facility or across a large, open space, DEMODOS can be configured to meet your needs.

- **Scalable number of dosimeters**: DEMODOS supports multiple dosimeters, allowing each participant to use their own device. This scalability ensures that the system can accommodate both small groups and large-scale training sessions involving multiple teams.

- **Scalable Area of Operation**: DEMODOS can be deployed in various environments, from small indoor spaces to large outdoor areas. For enclosed industrial sites, the system can integrate with existing on-premise infrastructure using the customer’s internal network. If sharing infrastructure is not possible due to legal or security restrictions, DEMODOS can be set up with a dedicated network specifically built for the training scenario.

- **Alternative Networking Technologies**: For expansive areas where Wi-Fi may not be reliable, DEMODOS can use alternative communication technologies that do not require proximity to access points. This allows the system to operate efficiently even in large or remote training locations.

- **Individual and Group Radiation Settings**: Radiation levels can be adjusted for each participant individually or applied to groups. This allows for customized scenarios where different teams face varying radiation conditions during the exercise.

- **Hotspot Simulation with User Localization**: Using automatic user localization, the system can simulate areas with higher radiation levels (hotspots). As participants move through the training area, they experience changing radiation levels based on their location, adding realism to the simulation.

This flexibility makes DEMODOS easy to customize for specific training scenarios, ensuring it can meet the unique requirements of each exercise.



