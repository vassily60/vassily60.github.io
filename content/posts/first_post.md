---
title: "Why Analog Communication is Still Relevant in a Digital World"
date: 2026-05-21
description: "Why is analog communication still relevent where almost everything is digital? Let's explore how analog communication works why it might come back in the future."
tags: ["communication", "digital", "analog", "technology"]
draft: false
---

# Introduction

Analog communication systems were the first and dominant form of communication used in modern history. From transmitting your voice through a telephone line to listening to radio and watching television, analog communication is hidden everywhere !

But why analog communication and what does "analog" mean in this context ? You might be disappointed by how short the answer is, but put simply, analog means continuous. In other words and analog signal is a function that can take up any values. One way I like thinking about how analog communication appeared (as opposed to digital communication) is that most natural phenomenon are in fact continuous and hence an intuitive way to capture their entirety is using a continuous system. Of course technology was also the main limiting factor, when Alexander Graham Bell (Bell's Labs !) invented the telephone in 1876, none of the technology to make a continuous signal digital existed, so this was not even an issue !

Going back to analog signals and communication, let's take temperature as an example, although one might round its value to an intger, it is a continuous value. Height, time or even voltage are other examples. And surprinsgly enough, when you want to capture your voice to send it to your neighbor (with a telephone !), a natural way to proceed is by representing it as a continuous signal. Think about it for a second, as you speak the air pressure changes smoothly taking up any value over time - it is the exact definition of a continuous function, or analog signal - perfect to transmit to our neighbhor.

Generalizing this example, it is easy to convince yourself that analog is the right choice for cases where you want to transmit continuous information ! We will see, this might not be always true but for now let's keep in mind this example and let's dive deeper into the theory behind analog communication.

# Analog Communication Theory

There are three main types of modulation in analog communication Amplitude Modulation (AM), Frequency Modulation (FM) and Phase Modulation (PM). You might be wondering now what modulation mean, and it is a fair question to ask, in simple terms it means applying your original signal to a another high frequency signal called a carrier wave. It might seem abastract, but it will make more sense in the following paragarphs. For now though, I will say that increasing the frequency of the original signal is necessary for two reasons. To make it travel further (low frequency signals loose energy quickly !) and use smaller antennas to receive the signal (an antenna of length 1/4 of the wavelength transmitted is required !).

## AM

AM was developed in the first quarter of the 20th century and was mostly used for radio broadcasting. It is straightforward and consist of three main parts

$$
s(t) = A_c \bigl[1 + \mu m(t)\bigr] \cos\\left(2\pi f_c t\right)
$$

## FM

## PM
