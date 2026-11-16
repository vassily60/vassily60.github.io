---
title: "Design and Characterization of a Pixel Readout Chip"
description: "A pixel readout chip mixing both rolling and global shutter."
weight: 10
cover:
  image: "/images/photopixel.jpg"
---

## A note on project details

Some of this project is covered by a non-disclosure agreement, so I cannot share the detailed design or implementation. I can, however, explain the motivation and the challenge I set out to explore.

## Why shutter type matters

A camera sensor turns light into an image, but it does not always capture every part of a moving scene at exactly the same time. With a **rolling shutter**, the sensor captures or reads the image one row at a time. When something moves quickly, different rows can represent different moments. The spinning fan below shows how that timing can distort the shape of moving objects.

![Comparison of a spinning fan captured with rolling and global shutters, illustrating motion distortion in the rolling-shutter image.](/images/fan.jpg)

A **global shutter** captures the scene across the sensor at the same time. This can represent fast motion more naturally. Achieving that can require extra pixel circuitry and storage, which brings its own design trade-offs.

![Global-shutter pixel readout diagram showing a photodiode, floating diffusion, and storage elements.](/images/globalshutter.jpg)

The four-transistor (4T) pixel diagram below is another example of the building blocks used in image sensors. It shows a pinned photodiode, a transfer gate (`TX`), a floating diffusion (`FD`), and reset and select transistors.

![Four-transistor pixel schematic with a pinned photodiode, transfer gate, floating diffusion, reset, and select transistors.](/images/4tpixel.png)

## The project goal

The goal of this project is to explore a pixel readout approach that brings together the useful motion-capture behavior of a global shutter and the practical advantages of a rolling shutter, while avoiding their usual drawbacks as much as possible. The challenge is to balance these competing needs in a pixel architecture.

Because of the NDA, I am keeping this page focused on the motivation rather than the implementation. The diagrams help explain the problem the project is trying to address, without going into the protected design details.
