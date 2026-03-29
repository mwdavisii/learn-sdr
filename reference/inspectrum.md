

## What It Is

inspectrum is a Qt-based GUI for visualizing IQ recordings. Open a captured IQ file and read the signal's structure visually: measure bandwidth, estimate symbol rate, identify modulation type. Essential for analyzing unknown signals.

## Launch

```bash
# Must be launched from a standard shell (NOT a Nix shell — inspectrum is pacman-installed)
inspectrum recording.iq
```

Supported formats: `.iq` (cf32, from SDR++Brown), `.raw` (from GQRX), `.cf32`, `.cs16`, `.cs8`.

## Key Controls

| Action | How |
|--------|-----|
| Zoom time axis | Scroll wheel |
| Zoom frequency axis | Ctrl + scroll wheel |
| Measure bandwidth | Drag cursor across signal width |
| Add symbol rate plot | Right-click → Add derived plot → Symbol rate |
| Adjust symbol rate | Drag the symbol rate plot handles |

## Analysis Workflow

1. Record an IQ file in SDR++Brown (Settings → Recording → Record) or GQRX (File → Start I/Q recorder)
2. Tune to the target signal before recording; record 10–30 seconds
3. Open file: `inspectrum recording.iq`
4. Scroll to zoom in on the signal in time; Ctrl+scroll to zoom frequency
5. Measure bandwidth by dragging a cursor across the signal's width
6. Right-click → Add derived plot → Symbol rate; adjust until individual symbols are visible
7. Note: bandwidth, approximate symbol rate, and modulation shape
8. Cross-reference on sigidwiki.com or search "SDR signal identification" communities

## Signal Shape Reference

| What You See | Modulation Hint |
|-------------|----------------|
| Constant-width stripe, varying brightness | AM |
| Constant-brightness stripe, varying position | FM |
| On/off blips (no carrier between) | OOK (On-Off Keying) |
| Two-frequency alternation | FSK |
| Constellation of dots (needs phase plot) | PSK / QAM |

## Gotchas

- inspectrum is installed via `pacman`, not Nix. It will not be on PATH in a Nix shell. Open a standard terminal.
- Large IQ files (>1 GB) may be slow to load. Record shorter samples when possible.
- The symbol rate plot requires manual adjustment — there's no auto-detect. Zoom in until you can count symbols by eye, then match the cursor spacing.

## See Also

→ [[01-explorations/05-signal-analysis]]
→ [[reference/gqrx]] (IQ recording)
