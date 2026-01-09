# Bottle Filling Station Ladder Logic Program (Siemens S7-200)

## Overview
This project implements an automated **bottle filling station** using Siemens S7-200 PLC ladder logic. The program controls the filling process by counting bottles, timing the filling duration, and sequencing outputs for smooth operation. The logic is structured across the **Main Program (OB1)**, a **Subroutine (SBR_0)**, and an **Interrupt Routine (INT_0)**.

## Program Structure
- **Main Block (OB1):**
  - Uses counters **C0** and **C1** to track bottle counts.
  - Timers **T37** and **T38** manage filling and transfer delays.
  - Controls outputs **Q0.0**, **Q0.1**, and **Q0.2** for filling, conveyor, and bottle release.
  - Reset logic clears outputs when stop input is pressed.
- **Subroutine (SBR_0):**
  - Encapsulates reusable logic for enabling bottle filling sequence.
  - Input variable `EN` (BOOL) used for enabling.
- **Interrupt Routine (INT_0):**
  - Provides interrupt-driven handling for precise timing and fast response.
  - Uses temporary variables for event-driven control.

## Features
- **Bottle counting:** Counter **C0** increments with each bottle detected at input `I0.0`.
- **Timed filling:** Timer **T37** ensures accurate filling duration before conveyor activation.
- **Conveyor control:** Timer **T38** triggers conveyor motor (`Q0.1`) for bottle transfer.
- **Release mechanism:** Counter **C1** drives output `Q0.2` for bottle release after filling.
- **Reset logic:** Input `I0.1` resets counters and clears outputs (`Q0.0`, `Q0.1`, `Q0.2`).

## Technical Details
- **PLC Platform:** Siemens S7-200 series
- **Programming Software:**
  - STEP 7 MicroWIN V4.0.9.25
  - S7-200 Explorer V2.0.0.27
- **Inputs:**
  - `I0.0` → Bottle sensor (detects presence of bottle)
  - `I0.1` → Reset/Stop input
- **Outputs:**
  - `Q0.0` → Filling valve/motor
  - `Q0.1` → Conveyor motor
  - `Q0.2` → Bottle release actuator
- **Counters/Timers:**
  - `C0`, `C1` → Bottle counting
  - `T37`, `T38` → Filling and transfer timing

## How It Works
1. Bottle detected at `I0.0` → Counter `C0` increments.
2. Filling valve (`Q0.0`) activates for a preset time via **T37**.
3. Conveyor (`Q0.1`) runs after filling, controlled by **T38**.
4. Counter `C1` tracks completed bottles and triggers release (`Q0.2`).
5. Reset input (`I0.1`) clears counters and resets all outputs.

## Applications
- Automated filling lines in beverage or chemical industries.
- Demonstration of PLC-based sequencing with counters and timers.
- Educational project for industrial automation training.

## Author
Developed by **Yashvi**  
Part of the PLC Ladder Logic Program Projects portfolio.
