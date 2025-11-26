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

## Images and Details

All measurements below are taken at **1.5 Mbps** UART TX on the Rock5B+, probed at the breakout pad directly connected to the RK3588 UART-TX pin.

### `uart-tx-edge-20ns-rock5bp.png`
Fine-scale view of a single **falling edge** at 20 ns/div.

- Timebase: **20 ns/div**
- Fall time: **≈ 11.2 ns**
- Vmax: **≈ 3.52 V**
- Vmin: **≈ 0.19 V**
- Preshoot: **≈ 1.1%**
- Ringing: very small, damped within ~20–30 ns

This capture is useful for inspecting the detailed edge shape, preshoot, and how quickly the driver settles to a stable low level.

---

### `uart-tx-edge-50ns-rock5bp.png`
Medium-zoom view of the **falling edge** at 50 ns/div.

- Timebase: **50 ns/div**
- Fall time: **≈ 12.0 ns**
- Vmax: **≈ 3.52 V**
- Vmin: **≈ 0.18 V**
- Preshoot: **≈ 1.1%**
- Ringing: clearly visible but well-controlled and fully damped before the next bit period

This screenshot makes it easier to see overall edge quality, including how much energy is in the post-transition ringing and how quickly it dies out relative to the 1.5 Mbps bit period.

---

### `uart-tx-edge-1us-rock5bp.png`
Wider view at 1 µs/div showing multiple UART bits.

- Timebase: **1.0 µs/div**
- Rise time: **≈ 11.5 ns**
- Fall time: **≈ 11.5 ns**
- Vmax: **≈ 3.54 V**
- Vmin: **≈ 0.16 V**
- Preshoot: **≈ 1.2%**

At this scale, the line looks like clean, well-formed digital levels with sharp transitions and ample timing margin for 1.5 Mbps operation. This view is useful for visually confirming bit width, duty cycle, and general signal cleanliness over several bit intervals.

---

### `uart-tx-rise-2ns-rock5bp.png`
High-resolution **rising-edge** capture at 2 ns/div.

- Timebase: **2 ns/div**
- Rise time: **≈ 10.2 ns**
- Voltage transition observed: **≈ 2.68 V → 3.46 V** (mid-bit rising transition)
- Overshoot: **0.0%**
- Preshoot: **0.0%**
- Ringing: minimal, well-damped within ~20–30 ns
- Edge shape: smooth and monotonic with no discontinuities

This rising-edge capture confirms that the RK3588 UART TX driver is well-controlled and does not exhibit significant overshoot or ringing, even when examined at the highest time resolution supported by the scope.


---

### `uart-tx-rise-0v-2ns-rock5bp.png`
High-resolution 2 ns/div capture of a **true 0 V → 3.3 V rising edge** on UART TX. The trigger threshold was lowered to ~800 mV to ensure the transition begins from a logic-low condition.

**Rising-Edge Characteristics (0 → 3.3 V)**
- Timebase: **2 ns/div**
- Rise time: **≈ 5.46 ns**
- Vmin: **≈ 0.18 V**
- Vmax: **≈ 3.22 V**
- Overshoot: **≈ 9.9%**
- Preshoot: **≈ 1.1%**
- Ringing: **minimal, well-damped**

This capture demonstrates the maximum edge rate and worst-case overshoot behavior of the RK3588 UART TX driver at the Rock5B+ board-level test point.

---

## Summary Notes

- Typical **rise and fall times** are in the **~10–12 ns** range at 3.3 V.
- Overshoot and preshoot are low and within expected limits for a short board-level trace.
- The measurements represent the **actual RK3588 pad output**, not cable or USB-serial dongle distortion.
- No DTS-level drive-strength tuning appears necessary for this board and routing at 1.5 Mbps.
