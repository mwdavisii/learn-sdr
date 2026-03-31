# Antenna Guide

## The One Rule

**Higher + outside = better.** Every other optimization is secondary to this. A mediocre antenna on a roof hears more than a perfect antenna in a basement.

## Stock Telescoping Whip

The stock whip is a quarter-wave monopole. Its optimal length depends on target frequency (quarter wavelength = 75,000 / MHz in mm, roughly):

| Target | Optimal Length | Notes |
|--------|---------------|-------|
| FM broadcast (98 MHz) | ~75 cm | Full extension |
| NOAA / airband (162 MHz) | ~46 cm | ~60% extension |
| APRS (144 MHz) | ~52 cm | ~70% extension |
| 433 MHz ISM | ~17 cm | ~25% extension |
| General scanning | ~16–20 cm | Reasonable compromise |

**Ground plane:**
The stock whip is a monopole — it technically requires a ground plane (counterpoise) to work correctly. Without one, the radiation pattern is asymmetric and signal levels are lower than they should be. In practice, it still *works* for FM/airband/APRS on a desk, but you're leaving performance on the table. Options:
- Set the dongle on a metal surface (PC case, cookie sheet, metal shelf)
- Attach 2–4 radial wires (~quarter-wave length for target frequency) to the SMA shell
- Accept the degraded performance for casual scanning — it's often fine enough

**Placement tips:**
- Window sill > desk in middle of room
- Keep USB cable away from the antenna (USB is noisy — use an extension cable to move the dongle away from the PC)
- Vertical polarization (straight up) matches most terrestrial signals
- Avoid running the whip parallel to power cables or monitors

## ADS-B Mag Mount Antenna (Incoming)

This antenna is tuned for 978–1090 MHz. Use it for aircraft tracking only — the stock whip outperforms it below ~800 MHz.

**Setup:**
- Mount on a metallic ground plane (car roof, metal shelf, PC case lid) — the mag mount needs metal to form a counterpoise
- Position near a window with sky view; 1090 MHz is line-of-sight
- Run the 1.5 m cable to the dongle; at 1090 MHz, 1.5 m of coax costs ~0.5 dB loss — acceptable
- Aim for the highest point you can reach with the cable length

**Switching antennas:** The SMA connector on the dongle is the same for both. Just swap when you switch use cases. Running the ADS-B antenna on 144 MHz or 433 MHz will degrade performance.

---
[< Previous: Hardware Setup](./03-hardware-setup.md) | [Next: Exploration 01 — FM & NOAA >](../01-explorations/01-fm-and-noaa.md)
