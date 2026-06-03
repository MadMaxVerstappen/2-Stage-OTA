# 2-Stage Operational Transconductance Amplifier (OTA) Design

## Problem Statement & Required Specifications

Design a low-power two-stage operational transconductance amplifier (OTA) using TSMC 180nm technology. The project is implemented and verified across two environments: LTspice (for initial schematic validation and closed-loop testing) and Cadence Virtuoso (for physical layout, common-centroid matching, and post-layout verification).

**Required Specifications:**
* The OTA must operate in a non-inverting amplifier configuration with a closed-loop gain of 2 (LTspice).
* The open-loop DC gain of the OTA must be at least 40 dB (with higher targets for the Cadence layout).
* The amplifier must be stable, with a phase margin of approximately 60° to 75°.
* The design should respond properly to a 0.2 V step input.

## Overview
This repository contains the design, mathematical calculations, and simulation parameters for a 2-stage OTA implemented in TSMC 180nm CMOS technology. The primary objective of this project is to utilize the designed OTA to construct a non-inverting amplifier with a closed-loop gain of 2, while ensuring the op-amp maintains an open-loop gain of at least 40 dB.

## Design Specifications
*   **Technology Node:** TSMC 180nm ($L_{min}$ = 0.18 µm)
*   **Supply Voltage ($V_{DD}$):** 1.8 V
*   **Threshold Voltages:** $V_{TN}$ = 0.37 V, $|V_{TP}|$ = 0.39 V
*   **Mobility Parameters:** $\mu_n C_{ox}$ = 230 µA/V², $\mu_p C_{ox}$ = 100 µA/V²

## Transistor Sizing (W/L Ratios)
The following table summarizes the theoretical and practical dimensions used for the MOSFETs in the circuit:

| Transistor | Theoretical (W/L) | Practical (W/L) |
| :--- | :--- | :--- |
| **M0** (Tail Current) | 10.9 | 10.9 |
| **M1, M2** (Input Differential Pair) | 5.45 | 5.45 |
| **M3, M4** (Current Mirror Load) | 10 | 10 |
| **M5** (Second Stage Common Source) | 10 | 10 |
| **M6** (Second Stage Load) | 5.435 | 5.4 |
| **M7** (Bias Circuit) | 1.09 | 1.09 |

## Performance Characteristics
The OTA was analyzed for both open-loop and closed-loop configurations. 

### Open-Loop Performance
*   **First Stage Gain:** 102.06 (Theoretical) / 83.02 (Practical)
*   **Second Stage Gain:** 25.53 (Theoretical) / 36.47 (Practical)
*   **Overall Open-Loop Gain:** 2605.59 (Theoretical) / 3027.82 (Practical)
*   **Power Dissipation:** 0.144 mW

### Frequency Response & Compensation
*   **Load Capacitance ($C_L$):** 10 pF
*   **Compensation Capacitance ($C_c$):** 3 pF
*   **Nulling Resistor ($R_2$):** 3.9 kΩ (added in series with $C_c$ to shift the zero and improve phase margin)
*   **Phase Margin (PM):** Adjusted to 60°
*   **Bandwidth:** ~4.98 MHz

### Closed-Loop Non-Inverting Amplifier
To achieve the desired gain of 2, the OTA is configured with a feedback network:
*   **Feedback Resistor ($R_f$):** 21 kΩ
*   **Input Resistor ($R_1$):** 20 kΩ
*   **Practical Closed-Loop Gain ($V_{out}/V_{in}$):** ~2.05 (Error of ~0.6%)
