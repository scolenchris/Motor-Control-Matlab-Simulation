# Motor-Control-Matlab-Simulation

- [中文版](./README_CN.md)

## Project Name: Design of Hoisting Mechanism Electric Drive System

![image](https://github.com/user-attachments/assets/e2db160d-72df-40f9-a545-13a39d66bf20)

### Table of Contents

- [Motor-Control-Matlab-Simulation](#motor-control-matlab-simulation)
  - [Project Name: Design of Hoisting Mechanism Electric Drive System](#project-name-design-of-hoisting-mechanism-electric-drive-system)
    - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
  - [Detailed principle and result analysis](#detailed-principle-and-result-analysis)
  - [Design Requirements](#design-requirements)
  - [Design Content](#design-content)
  - [Technical Parameters](#technical-parameters)
  - [Simulation Platform](#simulation-platform)
  - [Instructions](#instructions)

---

## Project Overview

This project aims to design an electric drive system for a hoisting mechanism, focusing on minimizing the time for lifting and lowering loads. The design process includes motor parameter selection, control scheme design, and simulation validation.

## Detailed principle and result analysis

- Due to space limitations, please click on the subordinate link to view.
- [中文版](./Design_CN.md)
- [English Version](./Design_EN.md)

## Design Requirements

1. **Analyze Technical Parameters and Control Requirements**

   - Analyze load characteristics and control requirements.
   - Provide a block diagram of the drive system composition.

2. **Select Motor**

   - Choose appropriate DC or AC motor rated parameters based on technical parameters and control requirements (calculation required before selection).

3. **Design Control Scheme**

   - Select suitable motor start, speed regulation, and braking schemes according to control requirements.
   - Analyze the four-quadrant operating points based on motor operation principles and mechanical characteristic curves (lifting the weight from the ground to a high place and then smoothly placing it back on the ground).

4. **Build MATLAB Simulation Platform**

   - Set motor parameters.
   - Simulate the chosen motor start, braking, and speed control methods using MATLAB.

5. **Simulate the Drive System**
   - Build a simulation framework for the drive system on the MATLAB simulation platform.
   - Simulate the entire process of lifting and lowering the weight.
   - Debug the system operation, observe changes in key variables (speed, current, voltage, torque), and adjust the control scheme according to load control requirements.

## Design Content

- **Control Objective**: Design the electric drive system of the hoisting mechanism with the shortest possible lifting/lowering time as the control objective.

## Technical Parameters

1. Empty hook weight: 10 kg
2. Maximum load: 1000 kg
3. Transmission ratio: 100:1
4. Transmission efficiency: 0.9
5. Maximum lifting speed: 1500 r/min
6. Minimum lowering speed: 300 r/min
7. Lifting/lowering height: 25 m
8. Drum diameter: 0.4 m

## Simulation Platform

- Open platform: MATLAB 2023 Simulink

## Instructions

1. Determine motor selection and control scheme by analyzing technical parameters.
2. Use MATLAB Simulink to build the simulation platform, input motor parameters and control schemes.
3. Run the simulation, observe key variable changes, and adjust the control scheme to achieve optimal performance.
