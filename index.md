---
title: UST detectors overview
layout: home
nav_order: 1
---

# UST particle detectors documentation overview

The detectors have multiple series depending on expected use cases. 

## AIRDOS: In-Flight Ionizing Radiation Monitoring

[AIRDOS](https://docs.dos.ust.cz/airdos) is designed for measuring ionizing radiation at flight altitudes aboard aircraft. It must detect mixed radiation fields, to save energy and weight is realized with a semiconductor detector. It places significant demands on low power consumption since it could lack an external power source. High reliability is crucial as it operates independently on board an aircraft and ensures it does not expose aircraft to a hazard. The service interval is around one month, with shorter servicing time compared to the aircraft itself preparation for flight, involving memory media and energy source replacement, to maintain continuous measurements within a single calibrated instrument on one aircraft.

## GEODOS: Ground-Based Radiation Detection

[GEODOS](https://docs.dos.ust.cz/geodos) is suitable for ground-based applications, both mobile and stationary. It can detect radiation occurring on the Earth's surface, typically using a scintillation detector. It has relatively low requirements for low power consumption since there is usually sufficient power available (solar or station-socket-based). High reliability is essential as it operates as a standalone device without supervision, with a service interval of approximately six months, primarily for memory media replacement.

## SPACEDOS: Spaceborne Radiation Dosimetry

[SPACEDOS](https://docs.dos.ust.cz/spacedos) is intended for measuring ionizing radiation in space conditions, with extreme mixed field energy values, typically in lower particle fluence than AIRDOS. It comes in two variants: for piloted and unpiloted missions, primarily differing in user interfaces or data access interfaces. The variant for piloted missions functions as a standard passive dosimeter that can be placed either statically or dynamically on a cosmonaut's body. The variant for unpiloted missions is firmly integrated into the system it operates within, such as a satellite or spacecraft. It requires low power consumption due to energy and cooling constraints in a vacuum environment. High safety and reliability are essential, similar to AIRDOS. Energy sources include onboard power for unpiloted flights or chemical cells (primary cells/accumulators) for piloted flights. The service interval is the duration of one mission, roughly around six months for the ISS, or longer, with no maintenance required until the next service window.

## LABDOS: Experimental Radiation Detection instrument

[LABDOS](https://docs.dos.ust.cz/labdos) is an experimental device that can theoretically be used in all the aforementioned applications. But due limitation of the universal design its primary purpose is to design and verify experiments before employing more specific instruments mentioned above. It serves as a testbed for new technologies, currently using a semiconductor diode as a detector, with potential future expansion to include scintillation detectors. High reliability is not a requirement because it is primarily operated under direct user supervision. There are also no high demands for power consumption or power supply, as it is expected to be powered by a mobile source (tablet, smartphone, computer, power banks) via USB-C.
