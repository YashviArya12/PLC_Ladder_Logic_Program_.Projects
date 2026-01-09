# VFD Up/Down Control Ladder Logic Program (Siemens S7-200)

## Overview
This project implements a **Variable Frequency Drive (VFD) up/down control system** using Siemens S7-200 PLC ladder logic. The program allows controlled adjustment of motor speed by incrementing or decrementing analog output values. It uses arithmetic instructions, timers, and memory bits to ensure safe and precise VFD operation. The logic is structured across the **Main Program (OB1)**, a **Subroutine (SBR_0)**, and an **Interrupt Routine (INT_0)**.

## Program Structure
- **Main Block (OB1):**
  - Inputs (`I0.0`, `I0.1`) control VFD enable and direction (up/down).
  - Memory bits (`M0.0`, `M0.1`) store intermediate states for increment/decrement logic.
  - Timer **T37** manages delay intervals for speed adjustments.
  - Data registers (`VW100`, `VW200`) store intermediate values for analog output.
  - Analog output (`AQW0`) drives the VFD reference signal.
  - Arithmetic instructions (ADD_I, SUB_I, MOV_W) adjust speed values.
- **Subroutine (SBR_0):**
  - Encapsulates reusable logic for enabling VFD sequence.
  - Input variable `EN` (BOOL) used for enabling.
- **Interrupt Routine (INT_0):**
  - Provides interrupt-driven handling for fast response to control inputs.
  - Uses temporary variables for event-driven control.

## Features
- **Start/Stop control:** Input `I0.0` enables VFD operation; `I0.1` provides reset/down control.
- **Analog output control:** MOV_W instructions transfer values from data registers (`VW100`, `VW200`) to analog output `AQW0`.
- **Increment logic:** ADD_I increases speed reference stored in `VW100` and `VW200`.
- **Decrement logic:** SUB_I decreases speed reference when conditions are met.
- **Timer-based sequencing:** Timer `T37` ensures controlled delay (2000 × 100 ms) between adjustments.
- **Safety limits:** Speed reference values are bounded (e.g., >500, <1500) to prevent unsafe operation.

## Technical Details
- **PLC Platform:** Siemens S7-200 series
- **Programming Software:**
  - STEP 7 MicroWIN V4.0.9.25
  - S7-200 Explorer V2.0.0.27
- **Inputs:**
  - `I0.0` → VFD enable/start
  - `I0.1` → Down/reset input
- **Outputs:**
  - `Q0.0` → VFD run signal
- **Memory Bits:**
  - `M0.0` → Increment enable
  - `M0.1` → Decrement enable
- **Timers:**
  - `T37` → Delay timer for speed adjustments (2000 × 100 ms)
- **Data Registers:**
  - `VW100`, `VW200` → Speed reference values
- **Analog Output:**
  - `AQW0` → VFD reference signal

## How It Works
1. Start input (`I0.0`) enables VFD run (`Q0.0`).
2. MOV_W instructions initialize speed reference values in `VW100` and `VW200`.
3. Analog output `AQW0` is updated continuously with `VW100` values.
4. Timer `T37` triggers increment logic:
   - ADD_I increases `VW100` and `VW200` by fixed steps.
5. When speed exceeds threshold (e.g., 1500), decrement logic activates:
   - SUB_I reduces `VW100` and `VW200` gradually.
6. Reset input (`I0.1`) clears values and stops VFD output.

## Applications
- Motor speed control using VFDs.
- Industrial automation requiring variable speed adjustment.
- Demonstration of PLC-based analog output control with arithmetic operations.

## Author
Developed by **Yashvi**  
Part of the PLC Ladder Logic Program Projects portfolio.
