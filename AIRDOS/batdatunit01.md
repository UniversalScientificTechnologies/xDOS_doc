---
layout: page
title: "BATDATUNIT01: Power and data storage"
permalink: /airdos/BATDATUNIT01
parent: AIRDOS
nav_order: "1"
---

# BATDATUNIT01 - Power and data storage

The AIRDOS04, designed with efficiency and modularity, separates its detection capabilities from its data storage and power supply functions. These functions are executed through interchangeable modules, which also act as processor units with firmware, data storage with high capacity, and power sources.

The separation of the data storage and power supply from the detection part results from a desire to enhance the flexibility and ease of maintenance of the AIRDOS04B detector. By compartmentalizing these functions, the detector allows for easier upgrades, maintenance, and customization based on specific user needs or changing technological advancements.

The concept of an interchangeable digital part significantly reduces the maintenance time required to keep the detector operational. Maintenance on-site (such as on-board aircraft) involves swapping the digital part with another unit that is pre-prepared with cleared data storage and properly charged batteries.

All the firmware for the detector is also located in this digital part (BATDATUNIT). This ensures that firmware updates can be conducted out of the detection site, off the aircraft, so that the time required for regular maintenance is not extended by firmware updates.

The [BATDATUNIT01](https://github.com/mlab-modules/BATDATUNIT01) is a specialized module optimized for use in the AIRDOS04 series of detectors. It is a critical component, combining data storage and power supply functionalities in a single, compact unit. This integration simplifies the detector's design and enhances its ease of use, particularly in scenarios requiring mobility and efficiency.

1. **Integrated Data Storage and Power Supply**: The BATDATUNIT01 has substantial data storage capacity, allowing for extensive data accumulation over prolonged periods. It also includes a built-in power source, which is important for the detector's long-term autonomous operation, or in the cases in environments where external power may not be readily available.

1. **Embedded Processor with Firmware**: BATDATUNIT01 contains a microcontroller unit that controls the entire detector system and peripherals. This processor is loaded with the firmware, ensuring proper detector operation and can be easily updated with new features or improvements.

1. **Environmental Sensors**: The module is fitted with internal sensors, including a thermometer, hygrometer, and barometer. These sensors provide valuable data on the ambient temperature, humidity, and atmospheric pressure, factors that can be important for more precise data processing.

1. **USB Mass-Storage Interface**: For data management, the module is equipped with a USB mass-storage interface, allowing users to easily access and transfer data from the module. This feature makes the process of data retrieval and analysis straightforward and user-friendly.

1. **Modular design**: The module is specifically designed for quick installation and removal, without any advanced tools. This design ensures that the AIRDOS04 can be maintained and operated with minimal hassle.

### BATDATUNIT01-BAT - Integrated battery power source type

The accumulator module of the AIRDOS04 detector offers an integrated energy storage solution. This module is equipped with up to five lithium-ion cells housed in 18650 battery cases, providing a significant power capacity that can sustain the detector's operation for up to one month. The maximum capacity corresponds to 64 Wh of energy. The exact number of cells and therefore capacity could be altered to fit the specific application requirements or restrictions. Contact us to get more details on that topic.

The battery module could  be continuously connected to a USB-C power supply, functioning similarly to an [Uninterruptible Power Supply (UPS)](https://en.wikipedia.org/wiki/Uninterruptible_power_supply). In scenarios where the external power supply experiences outages, the accumulator module ensures that the AIRDOS04 continues to operate without interruption, maintaining consistent data collection and detector functionality.

The AIRDOS uses the same protection techniques as has been used in [SPACEDOS03](/spacedos/SPACEDOS03) on board of [ISS](https://en.wikipedia.org/wiki/International_Space_Station). Therefore each cell in the battery is over-voltage, under-voltage, over-current, and over-temperature protected.  Should be also noted that the over-current protection is managed for each cell separately by a non-reversible fuse. That means any uncommon power situation results in electrical disconnection of the affected cell. This protective action is not user-reversible for safety reasons.
Additionally, the cells are mounted in medical equipment grade cell holders, which ensures that each cell is separated enough, to avoid thermal runaway of the battery in case of an internal short circuit of one cell. For that the worst case there is an over-pressure fuse in each cell cylinder to avoid an explosion. Also, the plastic material used in AIRDOS has reduced toxicity in case of combustion.


### BATDATUNIT01-EXT - External power source type

The digital/data module variant is without any lithium accumulators for applications where batteries are not allowed due to safety restrictions. Designed for environments where a continuous external power source is readily available, this module prioritizes data handling and processing capabilities while relying on external power, through a USB-C connection.

This module contains the same critical digital components and firmware of the AIRDOS04 as BATDATUNIT01-BAT. Its design facilitates efficient data management, allowing for quick data transfer and analysis when connected to a computer or other devices. The absence of an accumulator is useful in cases where you need to put a detector in places where lithium cells are not permitted.

The integrated data storage of the detector is accessible as a mass-storage device via the USB-C interface. This feature provides fast and user-friendly access to the internal storage, without requiring any external memory readers. More information about the initialization of mass-storage mode is written in the “Device operations” part of this manual.

## Firmware update

The both types of BATDATUNIT contains AIRDOS04 firmware. Updating the firmware of your AIRDOS particle detector is an important process for ensuring the device is equipped with the latest features and any known bugs are solved. The following guide provides a step-by-step approach to updating the firmware using the AVRDUDE tool.

### Preparation

 * Ensure that your computer is compatible with the [AVRDUDE tool](https://github.com/avrdudes/avrdude).
 * Install the AVRDUDE tool, which is available for various operating systems.
 * Verify the presence of the AVRDUDE tool in your system by running the command `avrdude -v` in the command line.
 * Obtain the BATDATUNIT01 programming device

![BATDATUNIT01 firmware programming device](https://raw.githubusercontent.com/mlab-modules/BATDATUNIT01/BATDATUNIT01B/doc/img/BATDATUNIT01_programming_device.jpg)

### Obtaining the Firmware

 * Acquire the latest version of the firmware for AIRDOS from the manufacturer. The latest firmware is publicly accessible in the AIRDOS04 repository as a [release](https://github.com/UniversalScientificTechnologies/AIRDOS04/releases).
 * Before proceeding, make sure you have the correct firmware file for your detector model.

### Connecting the Detector

 * Connect the programming device to the computer using a USB A-B cable.
 * Insert the AIRDOS detector into the slots on the programming device as shown in the following photo

![BATDATUNIT01 firmware programming device](https://raw.githubusercontent.com/mlab-modules/BATDATUNIT01/BATDATUNIT01B/doc/img/BATDATUNIT01_programming.jpg)

### Uploading the Firmware

 * Open the command line on your computer.
 * Execute the firmware upload using the following command:

`avrdude -v -patmega1284p -carduino -P/dev/ttyUSB0 -b57600 -D -Uflash:w:<fw_path>:i`

Replace `<fw_path>` with the path to the downloaded firmware file. Ensure the `/dev/ttyUSB0` port matches the port where the programming device is connected.

### Verification

 * Check that the upload occurred without reported errors.
 * After updating the firmware, conduct tests to verify the functionality of the detector and the successful addition of new features or fixes.

When updating the firmware, it is important to follow instructions carefully and be cautious to avoid damaging the equipment. If uncertain or in need of more information, always refer to the manufacturer or consult an expert.
