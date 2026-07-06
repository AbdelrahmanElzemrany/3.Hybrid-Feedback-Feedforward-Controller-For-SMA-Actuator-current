[Click here and press view raw to download and view the integrated control loop video.](A%20hybrid_Feedback_Feedforward_controller%20fe.mp4)

# Hybrid-Feedback-Feedforward-Controller

An end-to-end electro-thermal modeling framework and hybrid feedforward-feedback control architecture to validate Joule heating dynamics in integrated Shape Memory Alloy (SMA) bending actuators. Built using Simulink, Simscape Multibody, and MATLAB.
## 📝 Project Overview

While path-dependent feedforward architectures driven by First-Order Reversal Curve (FORC) lookup arrays can cancel out baseline material hysteresis, they operate blindly under fixed environmental assumptions. In real-world applications, SMA actuators are subjected to **varying operational loads and external mechanical disturbances**. Because mechanical stress directly alters the material's internal thermodynamic state and shifts its underlying phase-transition temperatures, a pure feedforward controller will suffer from significant steady-state tracking offsets whenever the real-world load deviates from the initial calibration baseline.

This project solves this limitation by developing an end-to-end **hybrid feedforward-feedback control framework**. Instead of forcing a reactive feedback loop to battle massive non-linear hysteresis alone, or relying entirely on an unadaptable feedforward map, this hybrid architecture splits the control effort into two complementary tasks:
* **The Dominant Feedforward Core**: Employs computationally efficient 1-D FORC lookup arrays to compute and instantaneously deliver the bulk of the non-linear voltage required to drive the material phase fractions.
* **The Auxiliary Feedback Trim**: Layers a negative-gain PI loop over the system to dynamically capture and cancel out the small, unmodeled tracking errors induced by fluctuating mechanical loads and external disturbances.

By combining these two strategies, the controller achieves exceptional trajectory tracking precision across variable load spaces, ensuring robust stability without requiring high feedback gains that would otherwise cause actuator saturation or overshoot.


This repository is dedicated to the integration of the electro-thermal Joule heating system into a hybrid control framework driven by FORC-extracted feedforward lookup tables and an auxiliary feedback loop.

## 🚀 Pipeline & File Architecture

The repository is structured to take the system from raw thermodynamic equations to a verified controller tracking trajectories under varying operational loads:

### 1. Trajectory Mapping & Data Calibration
* **`sma_pure_1d_switching.mat`**: MATLAB workspace data file containing the 1-D lookup tables extracted via First-Order Reversal Curve (FORC) measurements to capture the core non-linear phase physics of the system.

### 2. Hybrid Control Integration & Simulation
* **`Hybrid_Feedback_Feedforwardcontroller.slx`**: The fully integrated multi-physics system. Implements a hybrid control strategy where the computationally efficient FORC 1-D lookup tables serve as the dominant feedforward driving force, while an auxiliary negative-gain PI controller dynamically compensates for tracking errors induced by varying mechanical loads.
