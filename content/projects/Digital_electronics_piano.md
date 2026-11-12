---
title: "FPGA Digital Piano"
description: "Designing a VHDL digital piano with note selection, clock division, and seven-segment display output."
weight: 30
cover:
  image: "/images/fpga.jpg"
---

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

These figures document the main verification steps from the lab report.

The CLK, counter, trigger, CLK_OUT, and ONE_SHOT signals show how the input clock becomes the audio clock.

![Clock divider waveforms showing the clock, counter, trigger, output clock, and one-shot signals.](/images/clock_divider.png)

The target-versus-actual note-frequency graph verifies the divider calculations used for the piano notes.

![Chart comparing target and actual piano note frequencies.](/images/note_verification.png)

The Vivado waveform shows switch_in cycling through C to B, modifier changes, reset behavior, and rapid note switching.

![Vivado waveform showing note-switching testbench signals.](/images/waveform.png)

## Conclusion & Final Notes

It is a pretty fun and hands on project I would recommend to anobody interested in learning FPGA and hardware description languages. What I like the most about this project is the final physical result, just being able to play and hear the notes is super satisfying.

📄 [Read the report](/papers/DigitalElectronics.pdf)
