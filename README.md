# SpaceRacer: Integrated Autonomous Racing with VCAP³

This repository accompanies **“An Integrated Autonomous Racing System with Velocity-Curvature-Adaptive Predictive Pure Pursuit Control.”**

**SpaceRacer** is a ROS 2 autonomous racing system for the RoboRacer / F1TENTH platform. It integrates 3D LiDAR sensing, mapping and localization, global raceline generation, obstacle perception, local replanning, and lightweight predictive tracking control.

> **Release note:** Upon paper acceptance, we will release the source code, configurations, and reproduction instructions in this repository.

---

## Demo

🎬 **Demo video:** [Watch on Bilibili](https://www.bilibili.com/video/BV1k44i6yEmq/)

---

## Overview

High-speed autonomous racing requires accurate state estimation, responsive trajectory tracking, and obstacle avoidance within a limited onboard computation budget. SpaceRacer addresses these requirements through three closely integrated components:

1. **Velocity-Curvature-Adaptive Predictive Pure Pursuit (VCAP³).** A lightweight geometric controller combining short-horizon position prediction, velocity–curvature-adaptive lookahead, and filtered heading compensation with longitudinal speed regulation and steering constraints.
2. **3D-to-2D localization and 2.5D obstacle perception.** Deskewed, height-filtered Livox MID-360 point clouds are registered against a 2D occupancy map, with IMU and wheel-speed measurements supporting continuous state propagation. The perception pipeline retains height information for obstacle segmentation before constructing planar obstacle envelopes in Frenet coordinates.
3. **An integrated ROS 2 racing stack.** Offline mapping and raceline optimization provide the global reference, while online behavior selection and spline-based local replanning supply tracking references for racing and static-obstacle avoidance.

---

## System Architecture

- **Offline preparation:** Cartographer mapping → 2D occupancy map → iterative quadratic programming (IQP) for a minimum-curvature raceline → reference speed profile.
- **Localization:** MID-360 point clouds + IMU + wheel odometry → motion compensation and height filtering → 2D map registration → continuous vehicle state estimates.
- **Perception:** Point-cloud filtering → 3D clustering → Frenet obstacle envelopes → obstacle tracking.
- **Behavior and local planning:** Vehicle state + global reference + obstacle tracks → reference selection and spline-based static-obstacle avoidance.
- **Control:** Active reference + vehicle state → VCAP³ → speed and steering commands → vehicle actuation.

The control loop operates at **50 Hz**. Architecture diagrams and module documentation will accompany the code release.

---

## Requirements

The current development and evaluation setup includes:

- **ROS 2 Foxy** on Linux.
- **NVIDIA Jetson** onboard computer.
- **Livox MID-360** 3D LiDAR with IMU measurements.
- **RoboRacer / F1TENTH** Ackermann-steered vehicle with a VESC-based drivetrain and wheel odometry.
- **F1TENTH Gym** for simulation-based controller evaluation.

Dependency versions, sensor calibration, and platform configuration details will be provided with the public code release.

---

## Getting Started

**Installation and usage instructions will be available upon paper acceptance.** The release will include:

- Environment setup and dependency installation.
- Workspace build instructions and ROS 2 launch files.
- Mapping, localization, and offline raceline-generation workflows.
- Simulation and real-vehicle configurations.
- Racing, static-obstacle avoidance, and experiment reproduction instructions.

---

## Results (Summary)

The manuscript evaluates the system through F1TENTH Gym ablations and physical experiments on the indoor G track. Reported results include:

- **Racing performance:** A mean lap time of **6.77 s** over ten physical racing laps, compared with **10.02 s** for LTV-MPC and **8.02 s** for a reactive racing baseline under the tested deployment configurations.
- **Computational efficiency:** A mean controller computation time of approximately **0.030 ms** within the **20 ms** control cycle. This measures controller execution, rather than end-to-end stack latency.
- **Simulation ablation:** The full VCAP³ configuration achieves shorter lap times and driven distances than basic Pure Pursuit, with a tradeoff in lateral reference-tracking accuracy.
- **Static-obstacle avoidance:** Physical demonstrations of avoidance maneuvers on a straight and at a tight bend through the integration of perception, local replanning, and tracking control.

Detailed evaluation settings, plots, and reproduction instructions will accompany the release.

---

## Citation

If you use SpaceRacer in your research, please cite the accompanying paper:

**An Integrated Autonomous Racing System with Velocity-Curvature-Adaptive Predictive Pure Pursuit Control.**

The final bibliographic information and BibTeX entry will be added after publication.
