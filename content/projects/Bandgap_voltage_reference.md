---
title: "BiCMOS Bandgap Voltage Reference"
description: "Designing and characterizing a temperature-stable 1.2 V reference in a 130-nm CMOS process."
weight: 20
cover:
  image: "/images/bandgap.png"
  alt: "Pixel array image used as a temporary cover for the bandgap reference project"
  caption: "Simple Bandgap Circuit Diagram"
  relative: true
---

**February 2026 - April 2026**  
_Cadence Virtuoso · Spectre · 130-nm CMOS PDK_

## Project Overview

I designed a transistor-level 1.2 V BiCMOS bandgap voltage reference that generates a stable voltage across temperature and process variations. The project focused on analog circuit design, simulation, and physical-layout verification.

## What I Designed

- Built a temperature-compensated reference using PTAT and CTAT voltage components.
- Designed the bipolar devices, current mirrors, and feedback circuitry in Cadence Virtuoso.
- Combined the opposing temperature dependencies to produce a stable 1.2 V output.

## Characterization

I evaluated the reference with Cadence Spectre across the conditions that matter for an integrated analog circuit:

- Temperature sweeps
- Power-supply rejection ratio (PSRR)
- Noise and power consumption
- Process, voltage, and temperature (PVT) corners
- Monte Carlo mismatch analysis

## Physical Verification

I verified the physical IC layout with design-rule checking (DRC), layout-versus-schematic (LVS) verification, and parasitic extraction. I then compared pre-layout and post-layout performance to understand the impact of physical implementation on the circuit.

## Tools and Technologies

- Cadence Virtuoso
- Cadence Spectre
- BiCMOS circuit design
- PTAT/CTAT temperature compensation
- 130-nm CMOS PDK
- DRC, LVS, and parasitic extraction

<!-- ## Project Evidence

These are the key moments worth documenting as the design develops. Replace each placeholder with a screenshot or photo of your own work.

<div class="project-photo-grid">
  <figure class="project-photo-placeholder">
    <div class="project-photo-placeholder-art"><span>01</span><strong>Capture the schematic</strong></div>
    <figcaption><strong>Bandgap schematic</strong><br />Take a clean screenshot of the complete transistor-level schematic in Cadence Virtuoso, with the PTAT, CTAT, current-mirror, and feedback sections visible.</figcaption>
  </figure>
  <figure class="project-photo-placeholder">
    <div class="project-photo-placeholder-art"><span>02</span><strong>Capture the simulations</strong></div>
    <figcaption><strong>Simulation results</strong><br />Capture the 1.2 V output across temperature, plus one useful plot such as PSRR, noise, or the temperature sweep.</figcaption>
  </figure>
  <figure class="project-photo-placeholder">
    <div class="project-photo-placeholder-art"><span>03</span><strong>Capture the layout</strong></div>
    <figcaption><strong>Physical layout</strong><br />Take a screenshot of the completed layout and, if possible, a second view showing the DRC/LVS verification result.</figcaption>
  </figure>
  <figure class="project-photo-placeholder">
    <div class="project-photo-placeholder-art"><span>04</span><strong>Capture the result</strong></div>
    <figcaption><strong>Final comparison</strong><br />Show a small table or plot comparing pre-layout and post-layout performance, including the effect of parasitic extraction.</figcaption>
  </figure>
</div> -->
