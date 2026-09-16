---
title: "FPGA Digital Piano"
description: "Designing a VHDL digital piano with note selection, clock division, and seven-segment display output."
weight: 30
cover:
  image: "/images/fpga.jpg"
  alt: "Temporary digital logic diagram used as the FPGA piano project cover"
  caption: "Temporary cover image"
---

_VHDL · FPGA design · Vivado simulation · Seven-segment display_

## Project Goal

I designed a digital piano on an FPGA that turns switch and push-button inputs into musical notes. The system decodes the selected note, generates the correct tone using a clock divider, and displays the note and octave on a four-digit seven-segment display.

## How It Works

- Encoded the seven natural notes using one-hot switch inputs.
- Used push-buttons to select flats, sharps, and the upper octave.
- Converted the selected note into a divider value based on the desired audio frequency.
- Generated the speaker clock with a counter and toggle-based clock divider.
- Scanned the seven-segment display to show the note letter, octave, and sharp indicator.
- Added reset and silence behavior for invalid or empty switch combinations.

## Verification

I created VHDL testbench stimulus to exercise the complete range of inputs, including all seven notes, sharps, flats, octave changes, silence, rapid switching, and non-sequential note changes. The simulations confirmed that the input signals and display outputs responded to the programmed test cases.

The design also revealed a practical limitation of behavioral simulation: the FPGA's MMCM clock manager requires hardware timing to lock, so some downstream outputs remain uninitialized in simulation even while the input stimulus is applied correctly.

## Project Graphs & Figures

These figures document the main verification steps from the lab report. One placeholder remains for the seven-segment display output.

<div class="project-photo-grid">
  <figure class="project-photo-placeholder project-photo-real">
    <img src="/images/clock_divider.png" alt="Clock divider waveforms showing the clock, counter, trigger, output clock, and one-shot signals" loading="lazy" />
    <figcaption><strong>Clock divider waveforms</strong><br />The CLK, counter, trigger, CLK_OUT, and ONE_SHOT signals show how the input clock becomes the audio clock.</figcaption>
  </figure>
  <figure class="project-photo-placeholder project-photo-real">
    <img src="/images/note_verification.png" alt="Chart comparing target and actual piano note frequencies" loading="lazy" />
    <figcaption><strong>Frequency verification</strong><br />The target-versus-actual note-frequency graph verifies the divider calculations used for the piano notes.</figcaption>
  </figure>
  <figure class="project-photo-placeholder project-photo-real">
    <img src="/images/waveform.png" alt="Vivado waveform showing note-switching testbench signals" loading="lazy" />
    <figcaption><strong>Simulation testbench</strong><br />The Vivado waveform shows switch_in cycling through C to B, modifier changes, reset behavior, and rapid note switching.</figcaption>
  </figure>
</div>

## Tools and Technologies

- VHDL
- FPGA digital design
- Vivado simulation
- Clock dividers and counters
- Seven-segment display multiplexing
- Digital logic testbenches
