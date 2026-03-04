# Schmitt Trigger Design and Characterization

This repository contains the design, simulation, and characterization of a **CMOS Schmitt Trigger**. The design flow involves schematic capture and netlist generation in **Synopsys Custom Compiler**, followed by full electrical characterization in **LTspice**.

## Table of Contents
* [Introduction](#introduction)
* [Circuit Design](#circuit-design)
* [Simulation Environment](#simulation-environment)
* [Characterization Results](#characterization-results)
* [Hysteresis and Waveforms](#hysteresis-and-waveforms)
* [Log and Error Analysis](#log-and-error-analysis)
* [How to Run](#how-to-run)
* [Author](#author)

---

## Introduction
A Schmitt Trigger is a dual-threshold comparator circuit that uses positive feedback to implement hysteresis. It is essential in VLSI systems for noise immunity and cleaning up "noisy" digital signals by preventing multiple transitions at the output for a single threshold crossing.

## Circuit Design
The design utilizes a standard 6-transistor CMOS configuration. The switching thresholds ($V_{TH+}$ and $V_{TH-}$) are determined by the ratio of the PMOS and NMOS device widths.

* **Process Node:** Generic 105nm (Level 1 Models)
* **Supply Voltage ($V_{DD}$):** 1.05V
* **Transistor Sizes:** $W=0.1\mu m, L=0.03\mu m$



## Simulation Environment
The project was verified using **LTspice**. The raw netlist exported from Synopsys Custom Compiler was modified to include generic Level 1 models to ensure tool interoperability and open-source accessibility.

### Tools Used
* **Design:** Synopsys Custom Compiler
* **Simulation:** LTspice XVII
* **Platform:** AlmaLinux (RHEL-based)

## Characterization Results
The circuit was characterized using a triangle wave input to observe both rising and falling transition points.

| Parameter | Value | Status |
| :--- | :--- | :--- |
| **$V_{TH+}$ (Rising Threshold)** | **~0.78 V** | Verified |
| **$V_{TH-}$ (Falling Threshold)** | **~0.47 V** | Verified |
| **$V_{H}$ (Hysteresis Width)** | **~0.31 V** | Calculated |
| **Average Power** | **~201.5 nW** | Verified |



## Hysteresis and Waveforms

### 1. Circuit Symbol and Setup
The logic symbol and the testbench setup used for characterization.
| Symbol | Testbench |
| :---: | :---: |
| ![Symbol](./images/symbol.png) | ![Testbench](./images/testbench.png) |

### 2. Hysteresis Loop (VTC)
The Voltage Transfer Characteristic (VTC) curve plotted as $V_{out}$ vs $V_{in}$ showing the distinct hysteresis window.
![Hysteresis Curve](./images/hysteresis_curve.png)

## Log and Error Analysis
The following snippets represent the numerical verification from the Spice Error Log:

```text
vth_plus: v(vout_final)=0.525 AT 4.78357e-008
avg_power: AVG(i(v_vdd)*v(vdd!))=-2.01495e-007
