---
layout: page
title: "Pairing records with flights"
parent: "DOSPORTAL - Cloud-based Dosimetry Data Platform"
permalink: /dosportal/flight_pairing
nav_order: 4
sitemap: false
---

# Pairing records with flights

A dosimetric data on its own answers the question *how much* radiation was measured. To answer *where*, the data has to be connected to the flight during which it was acquired.

{: .warning }
> DOSPORTAL is under active development. Flight pairing is being actively worked on and the workflow described below may still change.

## Getting flight data into DOSPORTAL

There are two ways to make flight trajectories available for pairing.

![Flight linking interface in DOSPORTAL](/DOSPORTAL/img/flight_linking.png)

*The flight linking interface: the timeline at the bottom shows how the flights overlap the record.*

### Uploading a trajectory file

Flight trajectory files can be uploaded manually. The importer is designed for several trajectory formats; the format currently supported is the Flightradar CSV format.

### Automatic pairing through an API key

An organization that holds an [Flightradar24 API key](https://fr24api.flightradar24.com/) can have its flights paired automatically. Flights are matched to the organization's measurements on the basis of the aircraft registration number together with further parameters. DOSPORTAL may support more services in the future.

## The pairing workflow

Immediately after data is uploaded, the data are paired with flights automatically based on time. The data is split along the flights it covers. Each flight then has its own page, so the measurement from an individual flight can be viewed on its own.

## What the flight data adds

Pairing makes information available that the detector itself does not record:

- **Flight properties** — origin, destination, airline and further flight attributes.
- **The flight on a map** — the trajectory flown.
- **Flight altitude** — the pressure altitude along the flight.
- **Radiation on a map** — the measured values drawn along the trajectory.

![Dose rate evolution drawn on a map of the flight](/DOSPORTAL/img/dosage_map.png)

*Dose rate along the flight path. The colour encodes the moving-average dose rate from low (green) to high (red), and the same values are shown below against time.*

### Methodology: how measurements are placed on the map

The trajectory is known as a series of aircraft positions. Individual measurement points are placed on a linear interpolation between these positions, which is what allows the measured values to be drawn along the flight path.
