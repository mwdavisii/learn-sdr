# 

## What It Is

GQRX is a Qt-based software defined radio receiver. Slightly older than SDR++Brown but excellent for IQ file recording and for routing audio to other applications via virtual audio sinks.

## Key Settings

| Setting | Where | Notes |
|---------|-------|-------|
| Device string | Configure I/O → Device | Use `rtl=0` for first RTL-SDR |
| Sample rate | Configure I/O → Input rate | 2.4M is a safe default |
| LNA gain | Receiver Options → LNA gain | Start at 30 dB; adjust for noise floor |
| Mode | Mode dropdown | WFM, NFM, AM, etc. |
| Squelch | SQL slider | Drag up from minimum to suppress noise |

## IQ Recording Workflow

1. Tune to the target signal
2. Set demodulation mode and gain
3. File → Start I/Q recorder
4. Set output path (`.raw` format, cf32)
5. Record 10–30 seconds of the signal
6. File → Stop I/Q recorder

Output file is loadable in inspectrum.

## Audio Routing (Alternative APRS Pipeline)

GQRX can route audio to a PipeWire/PulseAudio virtual sink. This lets you pipe GQRX audio into multimon-ng without using rtl_fm, keeping the GUI visible. Advanced setup; see PipeWire loopback sink documentation.

## Gotchas

- Same exclusive device access as SDR++Brown — only one can hold the dongle at a time.
- GQRX may save a broken config on first run if device isn't detected. Delete `~/.config/gqrx/default.conf` and relaunch if it won't start.
- On Arch with Nix, ensure you launch from the Nix environment where gqrx was installed.

## See Also

→ [[01-explorations/05-signal-analysis]] (IQ recording for inspectrum)
→ [[reference/inspectrum]]
