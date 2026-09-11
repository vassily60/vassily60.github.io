---
title: "Sign Language Controlled Robot"
description: "What if a robot could understand sign language and respond to it in real time?"
cover:
  image: "/images/robot-cover.jpg"
  alt: "Robot dancing that could be controlled by sign language"
  caption: "Source : Philosophy Magazine"
  relative: true
---

[View on GitHub](https://github.com/vassily60/Sign-Language-Controlled-Robot-Capstone-Project) · [Read the paper](/papers/sign-language-project.pdf)

# I Built a Robot That Understands Sign Language

## The Idea

I wanted to build a robot that you could control just by showing it hand signs, no remote, no keyboard, just American Sign Language (ASL). The goal was to keep it simple, fast, and cheap enough for anyone to build.

## How It Works

The system has two main parts:

1. **A camera** mounted on a small robot (built with a Raspberry Pi)
2. **A nearby laptop** that does the "thinking"

The robot takes a picture of your hand sign and sends it wirelessly to the laptop. The laptop figures out which sign you made and sends the answer back. The robot then moves in that direction.

I used four signs, each one is both a letter and a direction:

- **L** = Left
- **R** = Right
- **N** = North (forward)
- **S** = South (backward)

## Teaching the Robot to "See"

To recognize signs, I needed a lot of hand pictures to train a model. I used three sets of images:

- A big public dataset from Kaggle (mostly plain backgrounds)
- My own photos, taken with messier, more realistic backgrounds
- A mix of both

Training on more varied images helped the robot recognize signs in real rooms, not just in perfect lighting.

## The Brain Behind It

Instead of building a neural network from scratch, I used two existing, well-tested models (VGG16 and DenseNet201) and combined them together. Each one is good at spotting different kinds of details in an image. By merging their strengths, the combined model was much better at recognizing signs it hadn't seen in that exact setting before, kind of like getting a second opinion before making a decision.

The architecture of the combined model looks like this:
![Data Flow Architecture](/images/dataflow.png)

## Does It Actually Work?

Yes, pretty well:

- On test data, the combined model reached up to **97% accuracy**.
- In live, real-world testing (different people, different backgrounds), it got things right about **70% of the time**.
- Each prediction took about **0.24 seconds**, and the whole process (camera to robot movement) took under **3 seconds**, fast enough to feel responsive.

I also tested it with people of different skin tones. It worked a bit less reliably there, which shows the training data needs to be more diverse going forward.

## What's Next

This was a first step. Future versions could:

- Recognize more signs, including moving (dynamic) ones
- Work better across different skin tones and lighting
- Let the robot do more than just move, like picking up objects or navigating on its own

## Why It Matters

Projects like this show that sign-language-controlled devices don't need expensive, complicated hardware to work. With just a Raspberry Pi and a regular laptop, it's possible to build something useful for accessibility and hands-free control, and to do it in a way that's fast enough for real use.

### Resources

🐙 [Source code](https://github.com/vassily60/Sign-Language-Controlled-Robot-Capstone-Project)
📄 [Read the paper](/papers/sign-language-project.pdf)
🛰️ [Dataset](https://www.kaggle.com/datasets/grassknoted/asl-alphabet)
📊 [Slides](/papers/sign-language-slide.pdf)
▶️ [Demo video](https://youtu.be/JY7ufIt0C-c)
