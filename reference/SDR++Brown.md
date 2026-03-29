

## What It Is

SDR++Brown is the primary wideband receiver GUI — open source, plugin-based, and the Brown fork adds extra demodulator and decoder plugins. It's the main tool for visual spectrum scanning and audio listening.

## Key Settings

| Setting | Where | Notes |
|---------|-------|-------|
| Source | Source module → RTL-SDR | Must be selected before pressing Play |
| Sample rate | Source → Sample Rate | 2.4 MSPS is a good default; higher = wider view |
| Gain | Source → Gain | Start with "Auto"; manual range 0–50 dB |
| PPM | Source → PPM Correction | Enter value from `rtl_test -p`; default 0 |
| Demodulation mode | Bottom bar dropdown | WFM, NFM, AM, USB, LSB, etc. |
| Bandwidth | Bottom bar slider | Match to signal: ~200 kHz FM, ~10 kHz NFM |

## First Launch Workflow

1. Open SDR++Brown
2. Left panel → Source module → select "RTL-SDR"
3. Click ▶ Play
4. Type a frequency in the top bar or click on the waterfall
5. Set demodulation mode and bandwidth for your target signal

## Demodulation Modes

| Mode | Use For |
|------|---------|
| WFM | FM broadcast (88–108 MHz) |
| NFM | NOAA weather, APRS, ham repeaters |
| AM | Airband voice (108–137 MHz) |
| USB/LSB | Ham SSB (out of scope for RTL-SDR without upconverter) |

## Recording IQ Files

Settings → Recording → set output path. Click the record button (top bar) while tuned to a signal. Output format is `.iq` (cf32 interleaved). Used with inspectrum for signal analysis.

## Gotchas

- Only one application can hold the RTL-SDR device at a time. If SDR++Brown is running, `rtl_fm`, `rtl_433`, and `readsb` will fail to open the device.
- The first time you run it, SDR++Brown may open with no source configured — go to Source module and select RTL-SDR before pressing Play.
- If you get no audio: check the audio output device in the Audio module (right panel).

## See Also

→ [[01-explorations/01-fm-and-noaa]]
→ [[01-explorations/02-airband-voice]]
→ [[01-explorations/03-aprs]] (close SDR++Brown before running rtl_fm pipeline)
→ [[01-explorations/04-iot-sensors]] (close SDR++Brown before running rtl_433)
→ [[01-explorations/05-signal-analysis]] (IQ recording)
