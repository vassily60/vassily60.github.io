---
title: "Design and Characterization of a Pixel Readout Chip"
description: "A pixel readout chip mixing both rolling and global shutter."
weight: 10
cover:
  image: "/images/photopixel.jpg"
---

## A note on project details

This project took part during my internship at STMicroelectronics and I'm so grateful they gave me the opportunity to learn and explore mixed signal IC design and specifically pixel readout architectures. Some of the work I did is under a non disclosure agreement which prevents me from going into the details of the design, but I still want to share my experience and motivation for this project.

## Why shutter type matters

When I came in I did not know anything about pixel and I had to learn from scratch. Enthiusastic and motivated I worked during 3 months with my supervisor on a chip that incorporates a new pixel readout architecture, that had never been tested on silicon before. The main principle is simple, combine the advantages of rolling and global shutter and avoid their drawbacks.

When a camera sensor turns light into an image, it does not always capture every part of a moving scene at exactly the same time. With a **rolling shutter**, the sensor captures or reads the image one row at a time. When something moves quickly, different rows can represent different moments. The spinning fan below shows how that timing can distort the shape of moving objects.

![Comparison of a spinning fan captured with rolling and global shutters, illustrating motion distortion in the rolling-shutter image.](/images/fan.jpg)

A **global shutter** captures the scene across the sensor at the same time. This can represent fast motion more naturally. Achieving that can require extra pixel circuitry and storage, which brings its own design trade-offs.

It is exactly in this context that my project took place. Exploring a way to combine the advantages of both pixels, while keeping the architecture simple.

## Type of Pixels

The two pixels have some of the same parts, but they store and read the image in different ways. The 4T pixel is simpler. The global-shutter pixel adds storage capacitors so the image can be captured across the sensor at the same time and read later.

### 4T pixel

![Four-transistor pixel schematic with a pinned photodiode, transfer gate, floating diffusion, reset, and select transistors.](/images/4tpixel.png)

The name **4T** means the pixel has four transistors:

- **TX (transfer gate):** Opens the path from the photodiode to the floating diffusion (FD).
- **RESET:** Clears the FD before a new measurement.
- **Source follower:** Buffers the FD voltage so it can be read without disturbing the FD.
- **SELECT:** Connects the pixel signal to the column so it can be read.

During exposure, the photodiode collects charge from light. When TX turns on, that charge moves to the FD and changes its voltage. The source follower buffers this voltage, and SELECT connects it to the column. In this example, the sensor reads the rows one at a time, so it is a rolling-shutter pixel.

### Global-shutter pixel

![Global-shutter pixel readout diagram showing a photodiode, floating diffusion, and storage elements.](/images/globalshutter.jpg)

The global-shutter pixel has the same photodiode, TX, FD, and RESET, but it also has extra transistors and capacitors:

- **TX:** Moves charge from the photodiode to the FD when the pixel is captured.
- **RST (reset):** Resets the FD before the next capture.
- **SF1:** Buffers the FD voltage so it can be sampled.
- **PC:** Turns on the path that lets SF1 drive the sampling circuit.
- **S1 and S2:** Switch the signal onto capacitors **C1** and **C2**.
- **SF2:** Buffers the stored voltage for readout.
- **RS:** Connects the pixel output to the column.

The photodiode stores the light signal as charge (the **charge domain**). At the end of exposure, all pixels transfer their charge to the FD at the same time, where it becomes a voltage. S1 and S2 save voltage samples on C1 and C2. This is **voltage-domain storage**: the capacitors hold voltage, not the original photodiode charge. The camera can then read the stored voltages row by row, after the whole image has been captured.
