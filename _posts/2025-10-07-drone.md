---
title: "Autonomous Drone Patrol"
date: 2025-10-07
categories: [projects]
tags: [reinforcement learning, drone, PPO, DDPG, simulation, AirSim]
---

This project aims to develop an autonomous drone system capable of patrolling high-risk forest areas to monitor for fire threats using reinforcement learning.

### 🌲 Project Overview

- Focus: Forest fire risk monitoring via drone patrol  
- Environment: Simulated 3D forest built in Unreal Engine using AirSim plugin  
- Objective: Train a drone agent to navigate, avoid obstacles, and maintain stable patrol routes

---

### 🤖 Methodology

- **Control Algorithms:**  
  - Proximal Policy Optimization (PPO)  
  - Deep Deterministic Policy Gradient (DDPG)  
  - Transfer learning applied for policy reuse

- **Simulation:**  
  - AirSim-based environment with realistic lighting, wind, and trees  
  - Drone trained for obstacle avoidance, stability, and path-following

- **Hardware Integration:**  
  - Pixhawk flight controller  
  - Telemetry modules for bidirectional data flow  
  - Carbon fiber body design and custom 3D modeling via SolidWorks

---

### 🖼️ Sample Outputs

<img src="/assets/img/outdoor.png" width="400"/>
<img src="/assets/img/map.png" width="400"/>
<img src="/assets/img/drone.png" width="400"/>
<img src="/assets/img/results_rl.png" width="400"/>

---

### ⚙️ Tools & Technologies

`PPO`, `DDPG`, `AirSim`, `Unreal Engine`, `Python`, `Pixhawk`, `SolidWorks`, `Reinforcement Learning`

> This project was awarded 1st place at the BEST For Energy Ideathon, supported by the Ministry of Industry and Technology and ENSIA.
