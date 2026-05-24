---
title: "GPS-Free Drone Navigation Using Computer Vision"
description: "What if a drone could figure out where it is using nothing but its camera?"
cover:
  image: "/images/drone-satellite.png"
  alt: "Description de l'image"
  caption: "Source : NASA / mon labo"
  relative: true
---

[View on GitHub](https://github.com/vassily60) · [Read the paper](/papers/drone-satellite-project.pdf)

---

<!-- --- AJOUTER UNE IMAGE
title: "Mon projet"
cover:
  image: "images/mon-projet/cover.png"
  alt: "Description de l'image"
  caption: "Source : NASA / mon labo"
  relative: true
--- -->

### In Summary

This project builds a visual localization pipeline that estimates a drone's GPS position by matching its camera feed against a pre-loaded satellite map — no GPS, no wireless signal required. It compares two classical feature matching algorithms, SIFT and ORB, and stress-tests them under a range of degraded image conditions to find out where each one breaks down.

### Context & Motivation

I have always been fascinated by the idea that a machine can look at the world and figure out where it is, the same way you might recognize a neighborhood from a window seat on a plane. When I came across the problem of GPS-denied drone navigation, it felt like the perfect intersection of computer vision, real-world constraints, and genuinely high stakes applications — search and rescue, military operations, remote exploration. The question that really hooked me was not just "can we do this?" but "how robust is it really?" Most research papers test their algorithms under near-perfect conditions, but in the real world, images are blurry, noisy, and low resolution. I wanted to know exactly at what point the system stops working — and whether the choice of algorithm actually matters.

### What I Did

Built a full localization pipeline in Python using OpenCV and rasterio, matching drone images against a satellite map through feature detection, descriptor matching, and homography estimation
Implemented and compared two feature detectors: SIFT, known for its accuracy and scale robustness, and ORB, a faster binary alternative
Used the UAV-VisLoc dataset, a large-scale benchmark containing 6,742 drone images paired with satellite maps across 11 locations in China — focusing on a single location covering roughly 64 km² in the Taizhou region
Divided the satellite map into overlapping tiles and matched each drone image against every tile independently, selecting the best match by inlier count
Ran five independent degradation experiments — motion blur, Gaussian noise, and resolution reduction on drone images, and resolution reduction and coverage reduction on the satellite map — to identify failure thresholds for each algorithm

![Pipeline diagram](/images/drone-pipeline.png)

### Results

The results were honest and a little humbling. SIFT was the only algorithm that worked at all — ORB failed entirely across every single condition, including the clean baseline, because the scale difference between drone and satellite imagery simply exceeded what its scale pyramid could handle. That was not what I expected going in.
SIFT held up surprisingly well under Gaussian noise, maintaining a 100% success rate at both noise levels tested. Motion blur was the most damaging degradation, with success rate dropping to 40% at a blur kernel of 5 pixels and collapsing to 20% at kernel 15. Resolution reduction told a similar story — robust at moderate levels, then a sharp cliff at higher factors.
The localization errors were large in absolute terms (around 4000–5000 meters on an 8.86 km map), which means the pipeline is finding something but not with useful precision. In this context, success rate turned out to be a far more informative metric than raw localization error.

![Drone image (right) matched with corresponding satellite tile (left).](/images/drone-matching.png)

### What I Take Away

This project taught me that negative results are results too. I went in expecting a clean speed–accuracy tradeoff between SIFT and ORB, and instead found that ORB was simply not geometrically capable of handling this task — a much more interesting finding in its own way. If I were to do this again, I would test on a much larger image sample (the full 768 images rather than just 5), explore preprocessing steps like contrast enhancement to help with cross-view matching, and investigate whether tuning ORB's scale pyramid parameters could make it viable. The pipeline works, but there is a lot of room to make it work better — and now I know exactly where to look.

### Resources

🐙 [Source code](https://github.com/vassily60)
📄 [Read the paper](/papers/drone-satellite-project.pdf)
🛰️ [Dataset](https://github.com/IntelliSensing/UAV-VisLoc)
📊 [Slides](/papers/drone-satellite-slides.pdf)
