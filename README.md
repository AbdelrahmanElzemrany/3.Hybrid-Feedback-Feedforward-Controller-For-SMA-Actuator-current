# Hybrid High-Bias Feedforward-Feedback Controller for SMA Actuators

An end-to-end electro-thermal modeling framework and hybrid high-bias feedforward-feedback control architecture to validate Joule heating dynamics in integrated Shape Memory Alloy (SMA) bending actuators. Built using Simulink, Simscape Multibody, and MATLAB.

## 📝 Project Overview

Standard feedback loops battle massive non-linear hysteresis alone, while typical 1-D feedforward maps suffer from input-inversion and state-misalignment under varying operational loads. When an SMA wire is operated under loads higher than its calibration baseline, the stress-induced upward shift in phase-transformation temperatures causes standard feedforward tables to output a cool command instead of the required heating command. 

This project solves this architectural flaw by utilizing a **High-Bias Feedforward Calibration Framework** bound by real-world hardware limits. By calibrating the 1-D First-Order Reversal Curve (FORC) lookup arrays at a maximum load baseline (e.g., $70\text{ m}^{-1}$) structurally higher than all intended operating profiles (e.g., shifting between $62\text{ m}^{-1}$ and $52\text{ m}^{-1}$):
1. **Elimination of Input Inversion**: The desired operating envelope sits entirely below the calibration ceiling. Moving toward any target position strictly implies a trajectory of thermal contraction, ensuring the feedforward map always outputs a well-aligned, proactive heating command.
2. **High-Bias Feedforward Core**: The lookup tables operate with an inherent "high bias," outputting the maximum necessary baseline voltage required for worst-case loading states to rapidly overcome thermal deadbands.

3. **Auxiliary Feedback Trim**: A negative-gain PI loop operates in parallel to dynamically act as a cooling or adjustment trim. Because the fixed 2V limit and convective cooling create an unyielding physical thermodynamic bottleneck, the auxiliary feedback loop is heavily bound by anti-windup clamping to cleanly stabilize the system the moment the wire catches up to its physics-limited destination.

<img width="1807" height="742" alt="image" src="https://github.com/user-attachments/assets/c7c07f7d-9bfd-4863-90ca-64be0a4ad0e5" />



<img width="1917" height="935" alt="image" src="https://github.com/user-attachments/assets/88c46a66-bf40-4933-9dde-164a973f75ad" />

<img width="1917" height="925" alt="image" src="https://github.com/user-attachments/assets/244b3806-1dc1-42ab-9b1f-29c9565cab66" />

<img width="1917" height="926" alt="image" src="https://github.com/user-attachments/assets/1d81a71d-c90a-41bf-9f25-2f2c29c6c715" />





## 🚀 Pipeline & File Architecture

The repository is structured to implement and verify this high-bias control methodology under strict physical boundaries:

### 1. High-Bias Trajectory Calibration
* **`sma_pure_1d_switching.mat`**: MATLAB workspace data file containing the 1-D lookup tables extracted via First-Order Reversal Curve (FORC) measurements. The data arrays are explicitly calibrated at the maximum load ceiling ($70\text{ m}^{-1}$) to establish the high-bias forward-transformation (heating) and reverse-transformation (cooling) pathways.

### 2. Control Integration & Hard-Capped Simulation
* **`Hybrid_Feedback_Feedforwardcontroller.slx`**: The fully integrated multi-physics system in Simulink. Implements the parallel architecture where the high-bias 1-D lookup block delivers dominant voltage commands, while the auxiliary negative-gain PI loop trims transient errors. Includes a strict 2V saturation clamp and an active conditional integration anti-windup block to manage the physical thermal lag smoothly without causing software-induced overshoots.
