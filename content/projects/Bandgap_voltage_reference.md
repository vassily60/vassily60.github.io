---
title: "CMOS Bandgap Voltage Reference"
description: "Designing and characterizing a temperature stable 1.2 V reference."
weight: 20
cover:
  image: "/images/bandgaap.webp"
  caption: "Simple Bandgap Circuit Diagram"
  relative: true
---

<!-- **July 2026 - August 2026**   -->

## Project Overview

I designed a transistor-level 1.2 V bandgap voltage reference that generates a stable voltage across temperature and process variations. In general, it is super important for a circuit to have a stable reference voltage otherwise some components might behave in the wrong way. When I say stable, I mean that the voltage should not change, or change very minimally, with temperature and process variations. So I designed a bandgap reference that uses the opposing temperature dependencies of two voltage components to produce a stable output.

## What I Designed

- Built a temperature-compensated reference using PTAT and CTAT voltage components.
- Designed the bipolar devices, current mirrors, and feedback circuitry in Cadence Virtuoso.
- Combined the opposing temperature dependencies to produce a stable 1.2 V output.

## Characterization

I evaluated the reference with Cadence Spectre across the conditions that matter for an integrated analog circuit:

- Temperature sweeps
- Power supply rejection ratio (PSRR)
- Noise and power consumption
- Process, voltage, and temperature (PVT) corners
- Monte Carlo mismatch analysis

## Physical Verification

I verified the physical IC layout was DRC and LVS clean. Parasitic extraction was also performed to compare pre-layout and post-layout performance to understand the impact of physical implementation on the circuit.

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
