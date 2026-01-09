# Analog to Digital Input Ladder Logic Program (Siemens S7-200)

## Overview
This project demonstrates the conversion of **analog input signals** into **digital outputs** using Siemens S7-200 PLC ladder logic. The program reads an analog value from the PLC input channel, processes it through arithmetic operations, and drives digital outputs based on threshold conditions. The logic is structured across the **Main Program (OB1)**, a **Subroutine (SBR_0)**, and an **Interrupt Routine (INT_0)**.

## Program Structure
- **Main Block (OB1):**
  - Reads analog input from `AIW0` (Analog Input Word).
  - Moves and scales values into data registers (`VW100`, `VD100`).
  - Compares analog values against thresholds (40.0, 80.0) to control digital outputs.
  - Controls outputs **Q0.0**, **Q0.1**, and **Q0.2** based on ranges.
- **Subroutine (SBR_0):**
  - Encapsulates reusable logic for enabling analog-to-digital conversion.
  - Input variable `EN` (BOOL) used for enabling sequence.
- **Interrupt Routine (INT_0):**
  - Provides interrupt-driven handling for analog input processing.
  - Uses temporary variables for fast response to analog changes.

## Features
- **Analog-to-digital conversion**: Maps analog input values into discrete digital outputs.
- **Threshold-based control**: 
  - Below 40.0 → Q0.0 ON
  - Between 40.0 and 80.0 → Q0.1 ON
  - Above 80.0 → Q0.2 ON
- **Arithmetic operations**: MOV_W, DIV_R instructions used for scaling and processing.
- **Modular design**: Separation into OB1, SBR, and INT routines for clarity and scalability.

## Technical Details
- **PLC Platform:** Siemens S7-200 series
- **Programming Software:**
  - STEP 7 MicroWIN V4.0.9.25
  - S7-200 Explorer V2.0.0.27
- **Inputs:**
  - `AIW0` → Analog input word
  - `I0.0` → Digital enable input
- **Outputs:**
  - `Q0.0`, `Q0.1`, `Q0.2` → Digital outputs based on analog thresholds
- **Data Registers:**
  - `VW100`, `VD100` → Intermediate storage and scaling registers

## How It Works
1. Analog input is read from `AIW0` and moved into `VW100`/`VD100`.
2. Arithmetic operations scale the analog value for comparison.
3. If the value is **< 40.0**, output `Q0.0` is activated.
4. If the value is **between 40.0 and 80.0**, output `Q0.1` is activated.
5. If the value is **> 80.0**, output `Q0.2` is activated.
6. The subroutine and interrupt routine ensure modularity and fast response.

## Applications
- Sensor signal processing (temperature, pressure, flow).
- Converting analog sensor values into discrete control signals.
- Demonstration of analog-to-digital conversion in PLC-based automation.

## Author
Developed by **Yashvi**  
Part of the PLC Ladder Logic Program Projects portfolio.
