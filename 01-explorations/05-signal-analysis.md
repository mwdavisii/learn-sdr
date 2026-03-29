# Exploration 05: Signal Analysis with inspectrum

## Why This Matters

Not every signal has a known decoder. Signal analysis is the skill of reading a signal's structure visually to determine: what modulation? what bandwidth? what symbol rate? This gives you vocabulary to search for a decoder or write one — and it applies to every unknown signal you'll encounter.

## Step 1: Record an IQ File

**SDR++Brown:** Settings → Recording → set output path → click the record button (top bar) while tuned to the target signal. Output: `.iq` (cf32 interleaved).

**GQRX:** File → Start I/Q recorder. Output: `.raw`.

Record 10–30 seconds. Make sure the signal is visible and centered in the waterfall before recording.

## Step 2: Open in inspectrum

```bash
# Open a standard terminal (NOT a Nix shell — inspectrum is pacman-installed)
inspectrum recording.iq
```

## Step 3: Read the Signal

1. **Zoom time axis:** scroll wheel to expand/compress the time view
2. **Zoom frequency axis:** Ctrl+scroll to zoom in on the signal width
3. **Measure bandwidth:** use the cursor to span the signal from edge to edge — this is the occupied bandwidth
4. **Identify modulation by shape:**
   - Constant-width stripe, brightness varies = AM
   - Constant-brightness stripe, horizontal position varies = FM/FSK
   - On/off pulses with no carrier = OOK
   - Regular dots in a line = PSK or QAM (needs phase plot)
5. **Add symbol rate plot:** right-click → Add derived plot → Symbol rate. Drag the cursors until symbols become visible. The symbols/second rate is your symbol rate (baud).

## Signal Vocabulary

| Property | What It Tells You | How to Measure |
|----------|------------------|----------------|
| Bandwidth | How much spectrum it uses | Width of signal in inspectrum |
| Symbol rate | Symbols per second (baud) | inspectrum symbol rate plot |
| Modulation | How data is encoded | Shape/pattern of signal |
| Duty cycle | Continuous vs. bursty | Vertical streaks vs. dots in time axis |

## Identifying the Signal

Once you have bandwidth, symbol rate, and a modulation guess:
- Search [sigidwiki.com](https://www.sigidwiki.com) — a community database of signal signatures
- Search Reddit r/RTLSDR or r/signalidentification with your measurements
- Cross-reference with [[Memphis Signals Reference]] — is the frequency in a known service band?

## What to Try Next
→ [[reference/inspectrum]] — controls reference
→ [[reference/gqrx]] — alternative IQ recording tool
