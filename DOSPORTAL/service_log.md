---
layout: page
title: "DOSPORTAL: Service log"
parent: "DOSPORTAL - Cloud-based Dosimetry Data Platform"
permalink: /dosportal/service_log
nav_exclude: true
search_exclude: true
sitemap: false
---

# Service logbook

The service logbook is the operational history of an individual detector. While the measured data describes the radiation field, the logbook describes the state of the detector that produced it — where it is, what state it is in and what has been done to it.

{: .warning }
> DOSPORTAL is under active development. The service log is being actively worked on and the set of entry types may still change.

## Entry types

A number of useful details can be recorded in the logbook:

- **Location update** — where the detector is currently located.
- **Start and stop** — the state of the detector, recorded as start and stop entries marking when it was switched on and when it was switched off.
- **Maintenance** — a service action carried out on the detector.
- **Calibration** — a calibration added to the detector.
- **Note** — a free remark that does not fit the other types.

Further entry types are available beyond those listed above.

## The detector page

The page shows the technical details of the detector together with an overview of what the detector has measured, so the detector and its measurements can be seen in one place.

## Integration across the platform

The information from logbook is used throughout DOSPORTAL, where it makes working with the measured data easier — for example, it suggest data for the detection of flights described in [Pairing records with flights](/dosportal/flight_pairing) or suggest when the detector was turned on when data are uploaded.
