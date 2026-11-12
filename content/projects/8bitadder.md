---
title: "8-bit Ripple-Carry Adder"
description: "A transistor-level 8-bit signed ripple-carry adder with addition, subtraction, and overflow detection."
weight: 20
cover:
  image: "/images/adder/8bitadderlayout.png"
---

<br>

## Project Overview

The goal of this project is to design and layout a ripple carry adder for two 8 bit signed values. Addition and subtraction are supported, and overflow is detected. It is part of a bigger project, where I want to design an entire CPU core. For this reason, the bit pitch (size needed for one bit) is crucial as it will be used on other components such as the shifter.

For this specific design the critical path is determined by the carry propagation and it is essential to minimize it, by sizing the transistors correctly. The sizes are shown on the schematics and layouts below.

<br>

## Circuit Design

The overall design is made of 8 full adder stages, each of which output a sum and a carry. It supports two inputs, A and B, as well as a substract bit to choose from addition or substraction. I used xor gates to implement the substraction as it it basically take the 2's complement of the B input and add it to A (with +1 from the first carry in). The overflow is detected by xor'ing the carry in and carry out of the most significant bit.

The overall design is shown below !

![Schematic of the complete 8-bit ripple-carry adder.](/images/adder/8bitadder.png)

Let's first build the XOR gate. We set the bit pitch to 2.91um for ease of routing and avoid DRC violations. It will also be easier for the full adder as it more complex and need more space for routing.

![Transistor-level schematic of the XOR gate.](/images/adder/xor.png)

![Physical layout of the XOR gate with a 2.91 u  bit pitch.](/images/adder/xorlayout.png)

I then built a full adder from transistor-level logic. It is a pretty standard way of doing a full adder. Transistors are sized standardly using a minimum transistor width of 150 nm. Big PMOS transistors were also fingered to make them more compact and reduce the capacitance. Diffusion sharing was used as much as possible to reduce the area.

![Transistor-level schematic of a one-bit full adder.](/images/adder/fulladder.png)

The physical layout of one full-adder stage is shown below.

![Physical layout of the one-bit full adder.](/images/adder/fulladderlayout.png)

Finally, putting everything together I got the following layout. We can clearly see the bit pitch matching for the xor and full adder which facilitates the routing. As a side note, I strictly used M1 and M2 metals for the xor and full adder layout and kept M3 for the overall routing.

![Physical layout of the complete 8-bit ripple-carry adder.](/images/adder/8bitadderlayout.png)

<br>

## Verification and Critical Path Timing

I then verified the design with a pulse voltage source and text-file test vectors. For the signed 8-bit range of -128 to 127, I used **-1 + 1 = 0** as an example and traced both the input and output signals in simulation.

Input A is initially 11111111, the 8-bit two's-complement representation of -1. At 5 ns its sign bit changes, making A equal to 127.

![Simulation input waveforms for A, initially set to negative one before its sign bit changes.](/images/adder/signednegativeone.png)

B changes from 0 to 1 at 4 ns while subtraction remains disabled, setting up the -1 + 1 test.

![Simulation input waveforms for B, changing from zero to positive one at 4 ns.](/images/adder/signedpositiveone.png)

The output trace shows the sum bits responding in sequence as the carry propagates from the least significant bit toward the most significant bit. I measured delay from the 50% voltage crossings: B0 at 4.01 ns and Sum7 at 4.38 ns. This gives a critical-path delay of **370 ps**.

The sum settles to 00000000. Sum7 is the last sum bit to cross the 50% threshold after the input transition, giving a 370 ps critical path delay. When A changes to 127 at 5 ns while B stays at 1, overflow asserts because the result is out of range.

![Simulation output waveforms showing sum bits responding in sequence, along with the overflow signal.](/images/adder/resultoneminusone.png)

<br>

## Conclusion & Final Notes

And this is the end of this post ! There are definitely ways of improving this design but the main goal was to have a working adder. The learning curve of learning virtuoso is steep but this kind of project is really helpful. Hope this post helps if you are designing your own adder !

📄 [Read the full project report (PDF)](/papers/PS6%20VLSI%20.pdf)
