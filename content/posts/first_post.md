---
title: "Why Analog Communication is Still Relevant in a Digital World"
date: 2026-05-21
description: "Why is analog communication still releventin a world  where almost everything is digital? Let's explore how analog communication works and why it might come back in the future."
tags: ["communication", "digital", "analog", "technology"]
draft: false
---

# Introduction

Analog communication systems were the first and dominant form of communication used in modern history. From transmitting your voice through a telephone line to listening to radio and watching television, analog communication is hidden everywhere !

But why analog communication and what does "analog" mean in this context ? You might be disappointed by how short the answer is, but put simply, analog means continuous. In other words an analog signal is a function that can take up any value within a continuous range.

One way to think about how analog communication appeared is that most natural phenomena are in fact continuous and hence an intuitive way to capture their entirety is by using a continuous system. Of course, technology was also the main limiting factor. When Alexander Graham Bell invented the telephone in 1876 (long before the famous Bell Labs was formally established in 1925), none of the technology required to digitize a continuous signal existed, so digital wasn't even an option!

Going back to analog signals and communication, let's take temperature as an example, although one might round its value to an integer, it is a continuous value. Height, time or even voltage are other examples. And surprisingly enough, when you want to capture your voice to send it to your neighbor (with a telephone !), a natural way to proceed is by representing it as a continuous signal. Think about it for a second, as you speak the air pressure changes smoothly taking up any value over time - it is the exact definition of a continuous function, or analog signal - perfect to transmit to our neighbor.

Generalizing this example, it is easy to convince yourself that analog is the right choice for cases where you want to transmit continuous information ! We will see, this might not be always true but for now let's keep in mind this example and let's dive deeper into the theory behind analog communication.

# Analog Communication Theory

There are three main types of modulation in analog communication Amplitude Modulation (AM), Frequency Modulation (FM) and Phase Modulation (PM). You might be wondering now what modulation mean, and it is a fair question to ask, in simple terms it means applying your original signal to a another high frequency signal called a carrier wave. It might seem abastract, but it will make more sense in the following paragarphs. For now though, I will say that increasing the frequency of the original signal is necessary for two reasons. To make it travel further (low frequency signals loose energy quickly !) and use smaller antennas to receive the signal (an antenna of length 1/4 of the wavelength transmitted is required !).

## AM

AM was developed in the first quarter of the 20th century and was mostly used for radio broadcasting. It is straightforward and consist of three main parts

$$
s(t) = A_c \bigl[1 + \mu m(t)\bigr] \cos\left(2\pi f_c t\right)
$$

Let's break it down. $A_c$ is the amplitude of the carrier wave, simply how strong the carrier is to begin with. $m(t)$ is nothing more than your original message (your voice for example !), and $\mu$, called the modulation index, controls how much the message is allowed to affect the amplitude of the carrier. Finally $\cos(2\pi f_c t)$ is the carrier wave itself, oscillating at frequency $f_c$. Put together, what AM does is make the amplitude of the carrier follow the shape of your message - the louder you speak, the bigger the swing in amplitude !

This simplicity is exactly why AM was so popular for radio broadcasting, the receiver only needs to detect how the amplitude changes over time to recover the original message, which is a fairly cheap operation. But this simplicity comes at a cost, since most of the noise picked up along the way (lightning, electrical interference, you name it !) also affects amplitude, AM signals tend to be quite noisy, you have probably experienced this yourself if you ever listened to AM radio !

## FM

FM was developed later, in the 1930s, by Edwin Armstrong, mainly to solve the noise problem we just talked about. Instead of varying the amplitude of the carrier, FM varies its frequency, while keeping the amplitude constant.

$$
s(t) = A_c \cos\left(2\pi f_c t + 2\pi k_f \int_0^t m(\tau) d\tau\right)
$$

Here again $A_c$ and $f_c$ play the same role as before, the amplitude and frequency of the carrier. $k_f$ is the frequency sensitivity, it tells you how much the frequency should shift for a given value of the message $m(t)$. The integral might look intimidating but all it really says is that the instantaneous frequency of the carrier is constantly adjusted by the value of the message at each point in time.

Because the information is now carried by the frequency and not the amplitude, FM signals are much less sensitive to the kind of noise that affects amplitude. This is the reason why FM radio (the 88-108 MHz band you are used to !) sounds so much clearer than AM, at the cost of needing a wider bandwidth to transmit the signal.

## PM

PM, for its part, takes a similar idea but instead varies the phase of the carrier rather than its frequency.

$$
s(t) = A_c \cos\left(2\pi f_c t + k_p m(t)\right)
$$

$k_p$ here is the phase sensitivity, equivalent to $k_f$ for FM, and it controls how much the message shifts the phase of the carrier. You might notice that FM and PM look very alike, and they are, in fact PM and FM are mathematically related to each other (one is essentially the derivative of the other !), which is why they are often grouped together. FM was historically more popular for analog broadcasting, but PM ended up being more useful for digital communication, where it became the basis for modulation schemes still used today like PSK (Phase Shift Keying).

# Conclusion

So there you have it, three different ways of carrying a message over a carrier wave, by playing with its amplitude, frequency or phase. AM, simple but noisy, FM, clearer but requiring more bandwidth, and PM, less common on its own but foundational to a lot of what came after.

Going back to our original question, why analog communication, I hope it is now clearer how naturally continuous signals like your voice fit into this framework, and why for most of the 20th century, this was simply the only way to communicate over long distances. Of course, as we will see in a future post, digital communication eventually took over for most applications, but it is worth remembering that the theory behind it owes a lot to the analog systems we just covered !
