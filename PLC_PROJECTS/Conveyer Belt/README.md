# Conveyor Control Ladder Logic Program (Siemens S7-200)

## Overview
This project implements an automated **conveyor control system** using Siemens S7-200 PLC ladder logic. The program manages conveyor motor operation, bottle/item counting, and timed sequencing with safety interlocks. The logic is structured across the **Main Program (OB1)**, a **Subroutine (SBR_0)**, and an **Interrupt Routine (INT_0)**.

## Program Structure
- **Main Block (OB1):**
  - Input signals (`I0.0`, `I0.1`, `I0.2`, `I0.3`, `I0.4`) control conveyor start, stop, and sensor feedback.
  - Counter **C0** tracks items on the conveyor.
  - Timer **T37** manages conveyor delay and ensures controlled transfer.
  - Outputs **Q0.0 – Q0.4** drive conveyor motors and actuators.
- **Subroutine (SBR_0):**
  - Encapsulates reusable logic for enabling conveyor sequence.
  - Input variable `EN` (BOOL) used for enabling.
- **Interrupt Routine (INT_0):**
  - Provides interrupt-driven handling for fast response to sensor inputs.
  - Uses temporary variables for event-driven control.

## Features
- **Conveyor start/stop control:** Inputs `I0.0` and `I0.3` initiate and halt conveyor operation.
- **Item counting:** Counter **C0** increments with sensor input (`I0.1`).
- **Timed sequencing:** Timer **T37** ensures conveyor runs for preset duration (200 × 100 ms).
- **Multi-output control:** Outputs `Q0.0`–`Q0.4` manage conveyor motors, actuators, and auxiliary devices.
- **Reset logic:** Input `I0.3` resets counter and clears outputs.

## Technical Details
- **PLC Platform:** Siemens S7-200 series
- **Programming Software:**
  - STEP 7 MicroWIN V4.0.9.25
  - S7-200 Explorer V2.0.0.27
- **Inputs:**
  - `I0.0` → Start pushbutton
  - `I0.1` → Item sensor (counting)
  - `I0.2` → Secondary sensor
  - `I0.3` → Reset/Stop input
  - `I0.4` → Auxiliary sensor
- **Outputs:**
  - `Q0.0` → Conveyor motor
  - `Q0.1` → Secondary actuator
  - `Q0.2` → Counter-driven output
  - `Q0.3`, `Q0.4` → Additional conveyor actuators
- **Counters/Timers:**
  - `C0` → Item counting
  - `T37` → Conveyor timing (200 × 100 ms)

## How It Works
1. Conveyor starts when `I0.0` is pressed, activating `Q0.0`.
2. Sensor input (`I0.1`) increments counter `C0`.
3. Timer `T37` ensures conveyor runs for a preset time before stopping.
4. Outputs `Q0.1`, `Q0.2`, `Q0.3`, and `Q0.4` activate based on counter and sensor conditions.
5. Reset input (`I0.3`) clears counter and resets all outputs.

## Applications
- Automated conveyor systems in manufacturing.
- Material handling and packaging lines.
- Demonstration of PLC-based sequencing with counters and timers.

## Author
Developed by **Yashvi**  
Part of the PLC Ladder Logic Program Projects portfolio.
