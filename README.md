# Two-Stage Miller Compensated CMOS Op-Amp in Cadence

## Overview

This repository contains the transistor-level design and simulation of a **two-stage Miller compensated CMOS operational amplifier** designed using **Cadence Virtuoso/ADE** in a **3.3 V, 180 nm-style CMOS PDK**.

The op-amp uses a standard two-stage architecture with an NMOS differential input pair, PMOS current mirror load, second-stage gain device, Miller compensation capacitor, and a nulling resistor for stability improvement.

This project focuses on schematic-level analog IC design, simulation, debugging, and verification across nominal, PVT, and Monte Carlo conditions.

---

## Why I Did This Project

This was my first ever Analog IC Design project and so I wanted to gain practical experience using Cadence Virtuoso and to experience the complete design flow end-to-end. The goal was not just to simulate an op-amp, but to understand the full design process behind it: architecture selection, transistor sizing, biasing, compensation, stability analysis, large-signal behavior, PVT robustness, and mismatch offset verification. This helped me connect textbook analog design concepts with practical Cadence-based simulation and debugging.

---

## Target Specifications

| Parameter            |    Target |
| -------------------- | --------: |
| Supply Voltage       |     3.3 V |
| DC Gain              |   ≥ 80 dB |
| Unity Gain Bandwidth |  ≈ 10 MHz |
| Phase Margin         |     ≥ 60° |
| Slew Rate            | ≥ 10 V/µs |
| Load Capacitance     |     10 pF |
| Power Consumption    |  < 1.5 mW |

---

## Final Simulated Performance

| Parameter                |      Final Result | Status                          |
| ------------------------ | ----------------: | ------------------------------- |
| Nominal DC Gain          |           ≈ 81 dB | Pass                            |
| Nominal UGB              |         ≈ 9.7 MHz | Pass                            |
| Nominal Phase Margin     |           ≈ 75.7° | Pass                            |
| Gain Margin              |         ≈ 35.1 dB | Pass                            |
| Slew Rate                |       ≈ 10.6 V/µs | Pass                            |
| Nominal Power            |         ≈ 1.25 mW | Pass                            |
| Output Swing             | ≈ 0.15 V to 3.1 V | Pass                            |
| ICMR                     |  ≈ 0.2 V to 2.8 V | Pass                            |
| PSRR+                    |           ≈ 91 dB | Pass                            |
| PSRR-                    |          ≈ 104 dB | Pass                            |
| CMRR                     |           ≈ 78 dB | Acceptable                      |
| Monte Carlo Offset σ     |        ≈ 6.526 mV | Acceptable                      |

More detailed results can be seen in [`results.md`](results.md)

---

## Simulations Performed

| Simulation           | Purpose                                                   | Result / Screenshot                        |
| -------------------- | --------------------------------------------------------- | ------------------------------------------ |
| DC Operating Point   | Check bias currents and device operating regions          | [View](simulations/dc_operating_point.png) |
| AC Gain / STB        | Measure gain, UGB, phase margin, and gain margin          | [View](simulations/ac_gain_stb.png)        |
| Small-Step Transient | Verify closed-loop settling behavior                      | [View](simulations/transient_step.png)     |
| Slew Rate            | Measure large-signal output transition speed              | [View](simulations/slew_rate.png)          |
| Output Swing         | Find valid output voltage range                           | [View](simulations/output_swing.png)       |
| ICMR                 | Find valid input common-mode range                        | [View](simulations/icmr.png)               |
| PSRR / CMRR          | Measure supply and common-mode rejection                  | [View](simulations/psrr_cmrr.png)          |
| Load Sweep           | Verify stability for different load capacitances          | [View](simulations/load_sweep.png)         |
| PVT Analysis         | Check robustness across process, voltage, and temperature | [View](simulations/pvt_summary.png)        |
| Monte Carlo Offset   | Estimate mismatch-induced offset                          | [View](simulations/monte_carlo_offset.png) |

---

## Important Debugging Notes

Some important debugging issues were found and fixed during the project:

* The input polarity was initially reversed.
* Open-loop equal-input biasing caused the output to rail.
* The second-stage gain was improved by increasing device lengths.
* The nulling resistor was tuned to improve phase margin.

The detailed debugging process and struggle is documented here:

[`debugging_log.md`](debugging_log.md)

---

## Limitations

This is a schematic-level design only.

Current limitations:

* No layout was performed
* No post-layout parasitic extraction was done
* No common-centroid matching was implemented
* No offset trimming circuit was added

---

## Future Work

Planned improvements:

* Complete layout of the op-amp
* Use common-centroid layout for matched transistor pairs
* Add dummy devices for better matching
* Perform post-layout extraction and re-simulation
* Optimize offset using larger input devices
* Add offset trimming or auto-zero/chopper techniques for precision applications
* Extend load capacitance verification beyond 20 pF

---

## Final Summary

This project successfully demonstrates the schematic-level design and verification of a two-stage Miller compensated CMOS op-amp in Cadence. The final design achieves approximately 81 dB gain, 9.7 MHz UGB, 75.7° phase margin, 10.6 V/µs slew rate, and 1.25 mW nominal power consumption. PVT analysis confirms stable operation across corners, and Monte Carlo mismatch analysis shows reasonable offset behavior for an untrimmed CMOS op-amp.
