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

The DEMODOS system providing a flexible, safe, and remote-controlled system for simulating radiation exposure. DEMODOS is particularly useful for training scenarios where real radioactive sources cannot be used for safety reasons. The system is designed to enhance the learning experience by simulating real-world scenarios involving radiation exposure while ensuring complete safety for participants.

## Key Features

- **Realistic Radiation Simulation**: DEMODOS emulates various radiation exposure scenarios, allowing users to simulate different levels of radiation intensity in real-time.
- **Remote Operation**: The system is entirely remote-controlled, meaning that no real radioactive sources are involved, ensuring maximum safety for participants.
- **Multi-User Capability**: DEMODOS supports multiple users, enabling team-based exercises where each individual interacts with their simulated dosimeter.

## Components of DEMODOS

### 1. Personal Active Dosimeter (PAD) Emulator
The **PAD emulator** replicates the functions of a real personal dosimeter, monitoring and recording simulated radiation levels in real-time. Participants can wear this device during exercises, mimicking the experience of tracking radiation exposure in field conditions.

![SPACEDOS Personal Active Dosimeter](https://github.com/user-attachments/assets/1ad55b66-e335-4a74-a256-f7421073e868)

### 2. Dosimeter Display Unit (DDU)
The **DDU** is a display unit in form of wrist-watch, similar to a smart-watch. It shows current simulated radiation levels as detected by the PAD emulator. The DDU provides real-time feedback, ensuring that participants can monitor their "exposure" throughout the exercise.

![SPACEDOS Dosimeter Display Unit](https://github.com/user-attachments/assets/b3888b79-f818-4eb6-a282-9b013ce5907d)

### 3. Vibration Alerts
The PAD and DDU is equipped with a vibration motor to alert users when radiation levels exceed preset thresholds. This feature ensures immediate notification during critical moments, closely mimicking how real-world radiation alerts work.

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

The DEMODOS system is controlled through a user-friendly software interface written in Python. The software provides mission operators the ability to simulate radiation levels and control what is displayed on each participant's DDU and PAD. The software also includes features to simulate radiation noise, making the experience more realistic.

![obrazek](https://github.com/user-attachments/assets/b746ed27-2748-4429-8d20-bde783a12b54)

### Features:
- **Rich Interface**: Provides clear and efficient controls for simulation management.
- **Noise Simulation**: Adds realistic fluctuations to the simulated data, mimicking the natural variations in radiation measurements encountered in real-world situations.
- **Remote Control**: The system can be operated entirely remotely over a Wi-Fi network, making it suitable for a wide range of training environments. This capability allows for the easy integration of DEMODOS into various training scenarios, such as mock hazardous events or exercises conducted in large facilities.

## Use Cases

DEMODOS is ideal for:
- **Training for space missions and Solars events** on how to select the best place to hide before cosmic radiation.
- **Training emergency response teams** on how to safely navigate radiation exposure zones.
- **Educational purposes** in institutions focusing on nuclear physics, radiology, or emergency preparedness.
  
The simulator can be adapted for various scenarios, including simulating hotspots with higher radiation exposure, safe zones, and areas with gradual increases in radiation levels. Each participant’s data is tracked individually, allowing for detailed post-exercise evaluations.


![Mission crew](https://github.com/user-attachments/assets/577bf104-f723-4bd3-977e-e23b2fbb7165)

## Safety and Benefits

One of the most significant advantages of DEMODOS is that it allows for realistic radiation risk training without the dangers associated with real radioactive sources. The remote operation of the system ensures complete safety, making it an essential tool for training environments where real radioactive exposure would be impractical or hazardous.

- **No Actual Radiation Exposure**: Since all radiation is simulated, there is no risk of participants being exposed to dangerous levels of radiation during training.
- **Realistic Learning Environment**: Despite the lack of actual radiation, DEMODOS provides a highly realistic simulation, ensuring effective and practical learning outcomes.


## Flexibility and Customization

The DEMODOS system is designed with scalability and adaptability in mind, making it suitable for a wide range of training environments and user needs. It can be scaled both in terms of the number of client dosimeters and the area of operation. Whether you are simulating radiation in a confined industrial facility or a large, open space, DEMODOS can be tailored to fit your specific requirements.

- **Scalable Client Dosimeters**: The system can support multiple dosimeters simultaneously, enabling team-based exercises where each participant uses their own device. This scalability ensures that DEMODOS can be used for both small-scale training sessions and large group exercises.
  
- **Scalable Area of Operation**: DEMODOS can be implemented in various environments, from compact spaces to large-scale outdoor areas. For closed industrial sites, the system can integrate with existing on-premise infrastructure, utilizing the customer's internal network for seamless operation. If using shared infrastructure is impractical due to legal or security concerns, DEMODOS can be deployed with a dedicated network built specifically for the training environment.

- **Alternative Networking Technologies**: In large areas where Wi-Fi coverage may be insufficient, alternative communication technologies can be utilized. These technologies enable operation without the need for nearby access points, ensuring flexibility even in large or remote locations.

All system parameters can be scaled and customized according to the user's needs. For further details or inquiries about the system's capabilities, please contact us.
