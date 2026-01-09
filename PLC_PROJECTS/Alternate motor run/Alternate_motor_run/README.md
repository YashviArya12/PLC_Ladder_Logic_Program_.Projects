# Alternate Motor Run Timer (Siemens S7-200)

## Overview
This project implements an **alternate motor running control system** using Siemens S7-200 PLC ladder logic. The program ensures that two motors operate alternately with timer-based switching, balancing usage and preventing simultaneous operation. The logic is structured across the **Main Program (OB1)**, a **Subroutine (SBR_0)**, and an **Interrupt Routine (INT_0)**.

## Program Structure
- **Main Block (OB1):**
  - Handles initialization and timer-based motor switching.
  - Uses timers **T37** and **T38** for sequencing.
  - Controls outputs **Q0.0** (Motor 1) and **Q0.1** (Motor 2).
- **Subroutine (SBR_0):**
  - Encapsulates reusable logic for enabling/disabling motor alternation.
  - Input variable `EN` (BOOL) used for enabling sequence.
- **Interrupt Routine (INT_0):**
  - Provides interrupt-driven control for precise timing.
  - Uses temporary variables for handling fast switching events.

## Features
- **Alternate motor operation**: Motor 1 and Motor 2 run in sequence, never simultaneously.
- **Timer-based control**: TON instructions with preset times (100 ms) ensure controlled alternation.
- **Safety logic**: Prevents overlap between motor outputs.
- **Modular design**: Separation into OB1, SBR, and INT routines for clarity and scalability.

## Technical Details
- **PLC Platform:** Siemens S7-200 series
- **Programming Software:**
  - STEP 7 MicroWIN V4.0.9.25
  - S7-200 Explorer V2.0.0.27
- **Inputs:**
  - I0.0 → Start pushbutton
  - I0.1 → Stop/Reset input
- **Outputs:**
  - Q0.0 → Motor 1 relay
  - Q0.1 → Motor 2 relay
- **Timers:**
  - T37 → Motor 1 timing
  - T38 → Motor 2 timing

## How It Works
1. **Start input (I0.0)** activates Motor 1 (Q0.0).
2. **Timer T37** runs for the preset duration, then hands control to Motor 2.
3. **Motor 2 (Q0.1)** runs under control of **Timer T38**.
4. The sequence alternates continuously until the **Stop input (I0.1)** is pressed.
5. **Reset logic** ensures the program starts again with Motor 1.

## Applications
- Pumping systems requiring alternate motor operation.
- Conveyor systems with dual motor setups.
- Industrial processes where load balancing between motors is critical.

## Repository Structure
