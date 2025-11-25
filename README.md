# Signal Analysis & Embedded Linux Board Bring-Up

This repository contains my ongoing work on signal-integrity analysis and embedded Linux board bring-up across multiple SoCs and development boards.  
It includes oscilloscope captures, DTS experimentation, build instructions, and hardware bring-up notes.

---

## Repository Structure

### `boards/`
Per-board bring-up directories.  
Each board folder may include:

- UART / I²C / SPI signal-integrity captures  
- Probe setup and measurement methodology  
- Early bring-up logs and hardware validation notes  
- DTS experiments and interface characterization  

(Current boards include the Radxa Rock 5B+ / RK3588, with more to be added.)

### `signal-analysis/`
General signal-integrity work not tied to a specific board:
- Oscilloscope captures and annotated screenshots  
- Drive-strength and I/O timing tests  
- Measurement procedures  
- Reproducible waveform samples

### `u-boot/`
- Build scripts and environment setup  
- Notes and patches for mainline U-Boot bring-up  
- Upstreaming workflow notes

### `kernel/` *(optional)*
- Kernel build notes  
- DTS work  
- Configuration and debugging details

---

## Purpose

This repository documents:

- Board bring-up across multiple embedded Linux platforms  
- Reproducible signal-integrity measurement techniques  
- U-Boot and Linux enablement work  
- Reference configurations, scripts, and debugging notes

---

## Status

This is active and evolving work. Expect updates as I continue:

- Adding new boards and SoC families  
- Expanding SI methodology  
- Tuning drive strength and I/O timing  
- Publishing new captures and build instructions  
- Preparing bring-up patches for U-Boot and the Linux kernel

---

## License
- GPLv2  
