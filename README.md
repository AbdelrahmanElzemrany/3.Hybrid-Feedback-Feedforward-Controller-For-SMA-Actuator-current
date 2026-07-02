[Click here and press view raw to download and view the integrated control loop video.](A%20hybrid_Feedback_Feedforward_controller%20fe.mp4)

# Hybrid-Feedback-Feedforward-Controller

An end-to-end electro-thermal modeling framework and hybrid feedforward-feedback control architecture to validate Joule heating dynamics in integrated Shape Memory Alloy (SMA) bending actuators. Built using Simulink, Simscape Multibody, and MATLAB.

This repository is dedicated to the integration of the electro-thermal Joule heating system into a hybrid control framework driven by FORC-extracted feedforward lookup tables and an auxiliary feedback loop.

## 🚀 Pipeline & File Architecture

The repository is structured to take the system from raw thermodynamic equations to a verified controller tracking trajectories under varying operational loads:

### 1. Trajectory Mapping & Data Calibration
* **`sma_pure_1d_switching.mat`**: MATLAB workspace data file containing the 1-D lookup tables extracted via First-Order Reversal Curve (FORC) measurements to capture the core non-linear phase physics of the system.

### 2. Hybrid Control Integration & Simulation
* **`Hybrid_Feedback_Feedforwardcontroller.slx`**: The fully integrated multi-physics system. Implements a hybrid control strategy where the computationally efficient FORC 1-D lookup tables serve as the dominant feedforward driving force, while an auxiliary negative-gain PI controller dynamically compensates for tracking errors induced by varying mechanical loads.
