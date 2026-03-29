

## What It Is

multimon-ng decodes digital modes from audio input. Key supported protocols include AFSK1200 (APRS), POCSAG (pager), DTMF, and EAS (Emergency Alert System). It reads raw audio from stdin or a WAV file.

## Key Flags

| Flag | Purpose | Example |
|------|---------|---------|
| `-t raw` | Read raw audio from stdin | always used with rtl_fm pipe |
| `-t wav` | Read from WAV file | `-t wav recording.wav` |
| `-a AFSK1200` | Enable APRS decoder | for 144.390 MHz |
| `-a POCSAG512` | Enable pager decoder (512 baud) | `-a POCSAG512` |
| `-a POCSAG1200` | Enable pager decoder (1200 baud) | `-a POCSAG1200` |
| `-a EAS` | Emergency Alert System | for NOAA relay alerts |
| `-a ALL` | Enable all decoders | verbose; use for discovery |

## Common Invocations

```bash
# APRS decode from rtl_fm
rtl_fm -f 144.390M -s 22050 -g 40 | multimon-ng -t raw -a AFSK1200 /dev/stdin

# POCSAG pager decode
rtl_fm -f 152.0M -s 22050 | multimon-ng -t raw -a POCSAG512 -a POCSAG1200 /dev/stdin

# Decode from a recorded WAV file
multimon-ng -t wav -a AFSK1200 recording.wav

# Enable all decoders (noisy but useful for discovery)
rtl_fm -f 144.390M -s 22050 | multimon-ng -t raw -a ALL /dev/stdin
```

## Why `-s 22050`

The `-s 22050` flag sets the rtl_fm output audio sample rate to 22,050 Hz. This is the audio sample rate multimon-ng expects for correct decode — not the SDR sample rate. Changing this value will break decoding.

## Decoded Output Format (APRS example)

```
AFSK1200: W4XYZ-9>APRS,WIDE1-1,WIDE2-1:!3510.22N/08954.31WO230/015/A=000233
```

Format: `SOURCE>DESTINATION,PATH:PAYLOAD`
- Position packets contain lat/lon in the payload
- Look up any callsign on aprs.fi

## Gotchas

- rtl_fm holds the RTL-SDR device. Close SDR++Brown/GQRX before running the pipeline.
- If the pipe breaks (e.g., rtl_fm crashes), multimon-ng exits silently — no error message.
- On noisy signals: try adjusting rtl_fm gain (`-g 30` to `-g 50`). Too high a gain = more noise = more decode errors.

## See Also

→ [[01-explorations/03-aprs]]
→ [[02-projects/03-aprs-station]]
