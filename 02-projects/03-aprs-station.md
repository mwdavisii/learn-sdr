# Project 03: Persistent APRS Decode Station

## Overview

Build on [[01-explorations/03-aprs]]. Run a persistent APRS decode pipeline that logs packets to file with timestamps, and cross-reference decoded callsigns on aprs.fi to see Memphis-area operator positions and activity.

## Persistent Pipeline with Logging

```bash
# Log APRS packets to file with timestamps
rtl_fm -f 144.390M -s 22050 -g 40 | \
  multimon-ng -t raw -a AFSK1200 /dev/stdin | \
  while IFS= read -r line; do echo "$(date -Iseconds) $line"; done | \
  tee ~/aprs-log.txt
```

This runs until you Ctrl+C. Packets accumulate in `~/aprs-log.txt`.

## Running in the Background

```bash
# Start in background, output to log
rtl_fm -f 144.390M -s 22050 -g 40 | \
  multimon-ng -t raw -a AFSK1200 /dev/stdin | \
  while IFS= read -r line; do echo "$(date -Iseconds) $line"; done \
  >> ~/aprs-log.txt 2>&1 &

echo "PID: $!"  # save this to kill later

# Watch the log live
tail -f ~/aprs-log.txt

# Stop
kill <PID>
```

## Understanding AX.25 Packets

Format: `SOURCE>DESTINATION,PATH:PAYLOAD`

| Field | Example | Meaning |
|-------|---------|---------|
| SOURCE | `W4XYZ-9` | Transmitting callsign + SSID (-9 = mobile) |
| DESTINATION | `APRS` | Protocol identifier |
| PATH | `WIDE1-1,WIDE2-1` | Digipeater routing path |
| PAYLOAD | `!3510.22N/08954.31WO230/015` | Position report |

**SSID meanings (common):**
- `-0` (no SSID) — home station
- `-9` — mobile
- `-1` to `-6` — various (check aprs.fi)
- `-15` — Internet gateway (iGate)

**Payload type indicators:**
- `!` or `=` — position without/with messaging
- `@` — position with timestamp
- `:` — message
- `>` — status
- `_` — weather report

## Cross-Referencing on aprs.fi

1. Copy a callsign from the log (e.g., `W4XYZ-9`)
2. Go to aprs.fi and search for it
3. See: last heard position, track history, station info

## Memphis APRS Landscape

Memphis has active APRS infrastructure:
- **W4BS** digipeater network covers the metro area
- Traffic peaks during large events (Memphis in May, St. Jude Marathon, severe weather)
- Emergency management and ARES operators run positions during exercises

Local digipeaters to watch for: search aprs.fi for active stations near your location. Look for stations with "DIGI" or "WIDEn-n" in their beacons.

## Gotchas

- `rtl_fm` holds the device — stop the pipeline before using SDR++Brown
- The pipeline has no reconnect logic: if rtl_fm crashes, the whole thing stops silently. For long-running setups, wrap in a while loop or use a systemd service
- High local RF noise can cause many decode errors; try reducing gain (`-g 30`) if the log fills with garbage

## See Also

→ [[01-explorations/03-aprs]]
→ [[reference/multimon-ng]]

---
[< Previous: Project 02 — IoT Dashboard](./02-iot-dashboard.md)
