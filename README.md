# Autonomous Vision-Guided Ball Tracking Robot

An autonomous differential-drive robot powered by a Raspberry Pi 4 that tracks and intercepts red target objects in real time using computer vision and ultrasonic sensing. Built during the **BlueStamp Engineering** program.

---

## Technical Architecture

* **Processor:** Raspberry Pi 4 (Linux, Python runtime, OpenCV, RPi.GPIO)
* **Vision Pipeline:** Dual-space color segmentation (**HSV** + **YCrCb**) to isolate target contours; centroid and bounding area calculation for closed-loop steering error correction.
* **Actuation:** L9110S H-Bridge driving dual DC gear motors via directional GPIO switching.
* **Proximity Sensing:** Dual HC-SR04 ultrasonic sensors using $1\text{k}\Omega / 2\text{k}\Omega$ resistor voltage dividers to step $5\text{V}$ Echo signals down to $3.33\text{V}$ logic tolerance.

---

## System Schematic & Logic Flow
[Camera (160x120) ] ──> [ HSV/YCrCb Mask ] ──> [ Contour Centroid (x, y) ]
│
▼
[ GPIO Motor Commands ] <── [ Proportional Turn/Search ] <── [ Offset Error: e = x - 80 ]
---

## Engineering Challenges Resolved

* **Common Ground Isolation:** Resolved extreme H-Bridge thermal overload by establishing a unified ground plane across the Raspberry Pi, motor driver, and external battery pack.
* **Lighting Resilience:** Implemented a combined HSV and YCrCb mask to prevent target loss under variable environmental light.
