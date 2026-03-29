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
