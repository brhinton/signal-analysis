# Rock5B+ UART-TX Signal Measurements

This directory contains three oscilloscope captures of the UART-TX signal on the
Radxa Rock5B+. The goal is to document the edge behavior of the RK3588 3.3V UART
driver at the board-level test point.

## Measurement Setup

- **Board:** Radxa Rock5B+
- **Signal:** UART TX (3.3V CMOS)
- **Baud Rate:** 1.5 Mbps
- **Test Location:** Breakout board pad directly connected to SoC UART-TX
- **Oscilloscope:** Rigol DHO914  
- **Probe:** 10× passive probe, short ground spring  
- **Acquisition Mode:** Normal  
- **Persistence:** Off  
- **Trigger:** Falling edge, ~1.6V threshold  

These captures show the raw output of the SoC, not the USB-serial adapter.

## Images

### `uart-tx-edge-20ns-rock5bp.png`
Fine-scale view of the falling edge. Shows edge shape, preshoot, and damping.

### `uart-tx-edge-50ns-rock5bp.png`
Medium zoom. Useful for observing ringing and general edge quality.

### `uart-tx-edge-1us-rock5bp.png`
Wider view showing multiple UART bits for context.

## Notes

- Typical fall time observed: ~11–12 ns  
- Overshoot and preshoot are low and within expected limits  
- Measurements represent the actual RK3588 pad output, not cable or dongle distortion  

---

## Rising-Edge Measurement

### `uart-tx-rise-2ns-rock5bp.png`
High-resolution 2 ns/div capture of the TX rising edge. This measurement uses the same probe configuration as the falling-edge captures and reflects the true behavior of the RK3588 UART driver at the board-level pad.

**Rising-Edge Characteristics**
- Typical rise time: **~10.2 ns**
- Voltage transition observed: **~2.68 V → 3.46 V**
- Overshoot: **0.0%**
- Preshoot: **0.0%**
- Ringing: **minimal / well-damped within ~20–30 ns**
- Edge shape is smooth and monotonic with no discontinuities

The rising-edge capture confirms that the RK3588 UART TX output is well-controlled and exhibits minimal distortion. No DTS-level drive-strength adjustments appear necessary for the Rock5B+ under typical board-level routing conditions.
