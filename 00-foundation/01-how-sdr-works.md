# How SDR Works

## The Dongle Does One Thing

The RTL2832U chip is an analog-to-digital converter (ADC). That's it. It tunes the R820T2 tuner to a center frequency, samples the RF at a set rate, and streams raw IQ (in-phase/quadrature) samples to your computer over USB. Everything else — demodulation, decoding, filtering — happens in software.

This matters because: any bug is a software bug. The hardware is dumb on purpose.

## Four Parameters You'll Touch Constantly

| Parameter | What It Controls | Typical Range | Notes |
|-----------|-----------------|---------------|-------|
| **Center frequency** | What frequency the tuner points at | 24–1766 MHz | You see ~2–3 MHz around this |
| **Sample rate** | How many IQ samples/second | 0.25–3.2 MSPS | Higher = wider view; >2.4 MSPS may drop samples |
| **Gain** | RF amplification | 0–50 dB | Too high → noise floor rises; too low → weak signals invisible |
| **PPM correction** | Corrects dongle's crystal oscillator error | typically −20 to +20 | Run `rtl_test -p` to measure yours |

## Reading the Waterfall

The waterfall is a 2D signal history:
- **X axis** — frequency (center ± half your bandwidth)
- **Y axis** — time (new data scrolls down from top)
- **Color** — signal power (dark = noise floor, bright = signal)

A signal looks like a vertical stripe. Width = bandwidth. Brightness = power.
FM stations are wide (~200 kHz). NOAA weather is narrow (~10 kHz). ADS-B is a tiny blip at 1090 MHz.

## Why You See Only 2–3 MHz at Once

The R820T2 tunes a 24–1766 MHz range, but the RTL2832U ADC runs at a fixed sample rate. At 2.4 MSPS you see 2.4 MHz of spectrum centered wherever you tune. To see more, move the center frequency.

Think of it like a microscope: wide range, narrow field of view. SDR++ lets you zoom out by lowering sample rate (less bandwidth) or in by raising it (more bandwidth, up to hardware limits).
