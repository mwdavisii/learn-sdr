# Exploration 03: APRS — Automatic Packet Reporting System

## Why APRS

APRS is a 1200 baud digital protocol on 144.390 MHz. Amateur radio operators, weather stations, and emergency services broadcast position reports, weather data, and messages as AX.25 packets. It's the bridge from "listening to audio" to "receiving structured data" — same antenna, same dongle, but now you're parsing packets in the terminal.

## The Pipeline

rtl_fm tunes and demodulates to audio. multimon-ng decodes the AFSK1200 audio tones to AX.25 packets.

```bash
# Close SDR++Brown/GQRX first — exclusive device access
rtl_fm -f 144.390M -s 22050 -g 40 | multimon-ng -t raw -a AFSK1200 /dev/stdin
```

Flag notes:
- `-s 22050`: audio sample rate multimon-ng expects (not the SDR sample rate)
- `-g 40`: manual gain; adjust if you see too many decode errors (try 30–50)
- If you hear the characteristic "data burble" audio but see no decodes, gain may be too high

## What to Expect

Decoded packets look like:
```
AFSK1200: W4XYZ-9>APRS,WIDE1-1,WIDE2-1:!3510.22N/08954.31WO230/015/A=000233
AFSK1200: W5MEM-1>BEACON,TCPIP*,qAC:!3507.32N/08952.14W#PHG5130/W5MEM Digipeater
```

Format: `SOURCE>DESTINATION,PATH:PAYLOAD`
- Position packets (`!` or `=` in payload) contain lat/lon — paste coordinates into maps
- `WIDE1-1,WIDE2-1` in the path = packet being digipeated across the network
- Look up any callsign on [aprs.fi](https://aprs.fi)

## Adjusting Gain

If you see garbled output or no decodes:
1. Verify SDR++Brown is closed
2. Try `-g 30`, `-g 35`, `-g 45` — there's a sweet spot per location
3. If you hear audio burbles but multimon decodes nothing, gain is too high (noise overdriving the decoder)

## What to Try Next
→ [[reference/multimon-ng]]
→ [[02-projects/03-aprs-station]] — persistent pipeline with logging and map view
