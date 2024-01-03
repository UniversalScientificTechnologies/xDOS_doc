---
layout: page
title: "AIRDOS04: Quick start guide"
permalink: /airdos/AIRDOS04_quickstart
parent: AIRDOS
nav_order: "10"
---

# AIRDOS04: Quick start guide

{: .highlight }
This is an simplified version of the full user guide, made for fast detector setup. This quick-start guide contains only basic operations with the detector. For the complete manual, please refer [complete version](./AIRDOS04).


## Detector ativation

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/5E_j_orvsTs?loop=1">
   </iframe>
 </div>

The AIRDOS04 airborne radiation dosimeter and spectrometer and its detachable module, BATDATUNIT01, are laid out on a table. Then should be effortlessly assembled, connecting the two parts together. As they fit into place, the device acknowledges the successful assembly with a series of LED flashes and a brief beep, signaling it's powered on and operational. The AIRDOS04, now fully assembled, continues to exhibit its functionality by periodically blinking its LED. The detector is not possible to power off by any of the button.

[Detailed instructions in full manual]({{site.baseurl}}/airdos/AIRDOS04#detector-power-up).

## Status check

### Measurement

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/OLHI1WTeeHw?loop=1">
   </iframe>
 </div>

To confirm that the detector is actively recording data, observe the LEDs. The detector blinks its LED3 indicator (MCU LEDs) after each exposure (usually 10 seconds long, depending on FW configuration), indicating that the spectrum has been written to the inbuilt memory media.

[Detailed instructions in full manual]({{site.baseurl}}/airdos/AIRDOS04#status-indicator-description).

### Battery status

Battery status could be checked outside from detector or directly in the detector without interruption of measurement.

[Detailed instructions in full manual]({{site.baseurl}}/airdos/AIRDOS04#status-indicator-description).

#### Directly in detector

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/BMAA3ZnrR8o?loop=1">
   </iframe>
 </div>

#### Disconnected from the detector

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/BRZ_Ix2QTNE?loop=1">
   </iframe>
 </div>


## Battery/Data-storage unit replacement

### Removal

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/jfwqo6pnUCM?loop=1">
   </iframe>
 </div>

To the removal the user should carefully unscrews and gently removes the recording and power module, BATDATUNIT01, from the AIRDOS04 detector.

{: .highlight }
It's important to accurately note the time of this action, as marking the precise moment of shutdown is essential for subsequent data analysis. This time-stamping ensures that the data log can be accurately synchronized with radiation events, an integral part of the data processing and evaluation process. Please refer [complete version](./AIRDOS04#replacing-the-digital-part-of-the-detector) of manual to more details.

### Insertion

The insertion process is the same as described in 'Detector activation' section.

## Accumulator module charging

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/qtMtmowHTfo?loop=1">
   </iframe>
 </div>

Plug-in of USB-C cable to the AIRDOS04 device, initiating its power-up process. It is indicated by a series of visual and audible cues. The charging indicator lights up, signaling the commencement of the accumulator's charging cycle. The charging process is very slow to achieve maximal capacity and endurance of the li-ion accumulators.

# Data-accessing (Connecting to PC)

 <div style="width:100%; padding-top: 56.25%;position: relative;overflow: hidden;">
   <iframe style="width: 100%;height: 100%;position: absolute;top: 0;left: 0;" src="https://www.youtube.com/embed/uuGJzn98xzY?loop=1">
   </iframe>
 </div>

In case the BATDATUNIT01 outside from detector is connected to a computer, transition into an external mass storage. This function switch allows the user to access the memory media within, revealing files that contain the recorded data. The files, neatly organized and easily accessible, represent the valuable data gathered by the AIRDOS04, now ready for analysis or archiving.


[Detailed instructions in full manual]({{site.baseurl}}/airdos/AIRDOS04#measured-data-read-out-enforcing-mass-storage-mode).
