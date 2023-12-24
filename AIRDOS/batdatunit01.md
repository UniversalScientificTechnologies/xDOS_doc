---
layout: page
title: "BATDATUNIT01: Power and data storage"
permalink: /airdos/BATDATUNIT01
parent: AIRDOS
---

# BATDATUNIT01 - Power and data storage

The AIRDOS04, designed with efficiency and modularity in mind, separates its detection capabilities from its data storage and power supply functions. These functions are executed through interchangeable modules, which also act as processor units with firmware, data storage with high capacity and power source.

The separation of the data storage and power supply from the detection part results from a desire to enhance the flexibility and ease of maintenance of the AIRDOS04B detector. By compartmentalizing these functions, the detector allows for easier upgrades, maintenance, and customization based on specific user needs or changing technological advancements.

The concept of an interchangeable digital part significantly reduces the maintenance time required to keep the detector operational. Maintenance on-site (such as on-board aircraft) involves swapping the digital part with another unit that is pre-prepared with a cleared data storage and properly charged batteries.

All the firmware for the detector is also located in this digital part (BATDATUNIT). This ensures that firmware updates can be conducted out of the detection site, off the aircraft, so that the time required for regular maintenance is not extended by firmware updates.

The [BATDATUNIT01](https://github.com/mlab-modules/BATDATUNIT01) is a specialized module optimized for use in the AIRDOS04 series of detectors. It contains as a critical component, combining both data storage and power supply functionalities in a single, compact unit. This integration simplifies the detector's design and enhances its ease of use, particularly in scenarios requiring mobility and efficiency.

1. **Integrated Data Storage and Power Supply**: The BATDATUNIT01 is equipped with substantial data storage capacity, allowing for extensive data accumulation over prolonged periods. It also includes a built-in power source, which is important for the detector's long-term autonomous operation, or in the cases in environments where external power may not be readily available.

1. **Embedded Processor with Firmware**: BATDATUNIT01 contains microcontroller unit that controls the entire detector system and peripherials. This processor is loaded with the firmware, ensuring proper detector operation and can be easily updated with new features or improvements.

1. **Environmental Sensors**: The module is fitted with internal sensors, including a thermometer, hygrometer, and barometer. These sensors provide valuable data on the ambient temperature, humidity, and atmospheric pressure, factors that can be important for more precise data processing.

1. **USB Mass-Storage Interface**: For data management, the module is equipted with a USB mass-storage interface, allowing users to easily access and transfer data from the module. This feature makes the process of data retrieval and analysis straightforward and user-friendly.

1. **Modular design**: The module is specifically designed for quick installation and removal, without any advanced tools. This design ensures that the AIRDOS04 can be maintained and operated with minimal hassle.

### BATDATUNIT01-BAT - Integrated battery power source type

The accumulator module of the AIRDOS04 detector, offers an integrated energy storage solution. This module is equipped with up to five lithium-ion cells housed in 18650 battery cases, providing a significant power capacity that can sustain the detector's operation for up to one month. The exact number of cells and therefore capacity could be altered to fit the specific application requirements or restrictions. Contact support@ust.cz to get more details on that topic.

The battery module could  be continuously connected to a USB-C power supply, functioning similarly to an [Uninterruptible Power Supply (UPS)](https://en.wikipedia.org/wiki/Uninterruptible_power_supply). In scenarios where external power supply experiences outages, the accumulator module ensures that the AIRDOS04 continues to operate without interruption, maintaining consistent data collection and detector functionality.


### BATDATUNIT01-EXT - External power source type

The digital/data module variant without any lithium accumulators for applications where batteries are not allowed due to safety restrictions. Designed for environments where a continuous external power source is readily available, this module prioritizes data handling and processing capabilities while relying on external power, through a USB-C connection.

This module contains the same critical digital components and firmware of the AIRDOS04 as BATDATUNIT01-BAT. Its design facilitates efficient data management, allowing for quick data transfer and analysis when connected to a computer or other devices. The absence of an accumulator is useful in cases where you need to put a detector in places where lithium cells are not permitted.

The integrated data storage of the detector is accessible as a mass-storage device via the USB-C interface. This feature provides fast and user-friendly access to the internal storage, without requiring any external memory readers. More information about initialization of mass-storage mode is written in “Device operations” part of this manual.




