# Mixing Plant Control Ladder Logic Program (Siemens S7-200)

## Overview
This project implements an automated **mixing plant control system** using Siemens S7-200 PLC ladder logic. The program coordinates mixer operation, valve control, and analog output adjustments for precise process management. It uses memory bits, timers, counters, and analog word instructions to ensure safe and efficient mixing. The logic is structured across the **Main Program (OB1)**, a **Subroutine (SBR_0)**, and an **Interrupt Routine (INT_0)**.

## Program Structure
- **Main Block (OB1):**
  - Input signals (`I0.0`, `I0.1`, `I0.2`, `I0.3`, `I0.4`) control start, stop, and sensor feedback.
  - Memory bits (`M0.0`, `M0.1`) store intermediate states for sequencing.
  - Timers **T37** and **T38** manage mixing and delay intervals.
  - Outputs **Q0.0 – Q0.6** drive mixer motor, valves, and actuators.
  - Analog outputs (`AQW0`) are set using **MOV_W** instructions for precise control values (12800, 19200).
- **Subroutine (SBR_0):**
  - Encapsulates reusable logic for enabling mixing sequence.
  - Input variable `EN` (BOOL) used for enabling.
- **Interrupt Routine (INT_0):**
  - Provides interrupt-driven handling for fast response to sensor inputs.
  - Uses temporary variables for event-driven control.

## Features
- **Start/Stop control:** Input `I0.0` initiates mixing; `I0.1` provides reset/stop functionality.
- **Mixer sequencing:** Memory bit `M0.0` enables mixer logic; `M0.1` manages timed stages.
- **Timed mixing:** Timers `T37` and `T38` ensure controlled mixing intervals (50 × 100 ms each).
- **Valve and actuator control:** Outputs `Q0.0 – Q0.6` operate mixer motor, inlet/outlet valves, and auxiliary actuators.
- **Analog output control:** MOV_W instructions set analog word `AQW0` to values 12800 and 19200, simulating variable motor speed or valve position.
- **Reset logic:** Inputs `I0.1` and `I0.4` clear memory bits and reset all outputs (`Q0.0 – Q0.6`).

## Technical Details
- **PLC Platform:** Siemens S7-200 series
- **Programming Software:**
  - STEP 7 MicroWIN V4.0.9.25
  - S7-200 Explorer V2.0.0.27
- **Inputs:**
  - `I0.0` → Start pushbutton
  - `I0.1` → Stop/Reset input
  - `I0.2` → Mixer sensor
  - `I0.3` → Stage sensor
  - `I0.4` → Emergency reset
- **Outputs:**
  - `Q0.0` → Mixer motor
  - `Q0.1` → Valve actuator
  - `Q0.2` → Auxiliary actuator
  - `Q0.3`, `Q0.4`, `Q0.5`, `Q0.6` → Additional valves/actuators
- **Memory Bits:**
  - `M0.0` → Mixing sequence enable
  - `M0.1` → Stage control
- **Timers:**
  - `T37`, `T38` → Mixing and delay timing (50 × 100 ms each)
- **Analog Outputs:**
  - `AQW0` set to 12800 and 19200 via MOV_W instructions

## How It Works
1. Start input (`I0.0`) sets memory bit `M0.0`, enabling the mixing sequence.
2. Mixer motor (`Q0.0`) and valve (`Q0.2`) activate based on sensor `I0.2`.
3. Timer `T37` runs for 50 × 100 ms, setting memory bit `M0.1`.
4. Timer `T38` continues sequencing, resetting `M0.1` after its interval.
5. Outputs `Q0.1`, `Q0.3`, `Q0.4`, `Q0.5`, and `Q0.6` activate in sequence for valve and actuator control.
6. MOV_W instructions set analog output `AQW0` to 12800 and 19200, simulating variable control signals.
7. Reset inputs (`I0.1`, `I0.4`) clear memory bits and reset all outputs.

## Applications
- Industrial mixing plants (chemicals, food, beverages).
- Automated batching and blending systems.
- Demonstration of PLC-based sequencing with timers, memory bits, and analog outputs.

## Author
Developed by **Yashvi**  
Part of the PLC Ladder Logic Program Projects portfolio.
