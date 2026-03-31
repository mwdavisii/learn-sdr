# Project 01: ADS-B Aircraft Map

> **Requires the ADS-B mag mount antenna.** The stock whip works poorly at 1090 MHz — range will be severely limited. This project is gated on the dedicated antenna arriving ~2026-04-01.

## Overview

Decode Mode S ADS-B transponder broadcasts at 1090 MHz. Every equipped aircraft squawks position, altitude, speed, callsign, and ICAO ID. Feed the decoded data into tar1090 — a browser-based live map with aircraft tracks.

In Memphis this is unusually rewarding. KMEM is FedEx's global superhub; peak hours (~22:00–06:00 local) bring 100–300 cargo movements. You'll see MD-11Fs, 767Fs, 777Fs, A300-600Fs stacked in holding patterns and sequenced onto 36L/36R simultaneously.

See [[Memphis Signals Reference]] for frequency context and [[reference/readsb]] for full flag reference.

## Hardware Setup

- Mount the mag mount on a metal surface with a clear sky view — 1090 MHz is line-of-sight. Roof of a car, metal shelf, or HVAC enclosure all work.
- Keep coax runs short. LMR-240 loses ~0.5 dB/ft at 1090 MHz; a 20 ft run costs ~3 dB, noticeably reducing range.
- SMA Male connector → RTL-SDR SMA Female. No adapter needed if using the standard RTL-SDR Blog v3/v4.

## Run readsb

```bash
# Close SDR++Brown/GQRX first — exclusive device access
mkdir -p /tmp/readsb

readsb \
  --device-type rtlsdr \
  --device=0 \
  --freq 1090000000 \
  --gain -10 \
  --lat YOUR_LAT \
  --lon YOUR_LON \
  --net \
  --net-ro-port 30002 \
  --net-sbs-port 30003 \
  --write-json=/tmp/readsb
```

`--gain -10` is readsb's sentinel value for automatic gain — not literally -10 dB. Start here; tune manually if you're seeing a lot of noise or missed decodes.

Key flags:

| Flag | Value | Purpose |
|------|-------|---------|
| `--freq` | `1090000000` | 1090 MHz Mode S |
| `--gain` | `-10` | Auto gain |
| `--lat` / `--lon` | `YOUR_LAT` / `YOUR_LON` | Your coordinates; enables range/bearing display |
| `--net` | — | Opens network ports for tar1090 |
| `--net-ro-port` | `30002` | Beast binary output (tar1090 reads this) |
| `--net-sbs-port` | `30003` | SBS/BaseStation format (optional, VRS/FR24) |
| `--write-json` | `/tmp/readsb/` | JSON files tar1090 reads |

## tar1090 Setup

tar1090 is not in nixpkgs. Run it directly from the repo:

```bash
git clone https://github.com/wiedehopf/tar1090 ~/tools/tar1090

# tar1090 fetches from data/ relative to html/ — symlink the entire readsb output dir
ln -s /tmp/readsb ~/tools/tar1090/html/data

# Serve from html/, not the repo root (repo root gives a directory listing)
python3 -m http.server 8080 --directory ~/tools/tar1090/html
```

Then open `http://localhost:8080`. tar1090 fetches `data/aircraft.json`, `data/receiver.json`, etc. — symlinking the whole directory covers all of them.

## Running Persistently

```ini
# ~/.config/systemd/user/readsb.service
[Unit]
Description=readsb ADS-B decoder
After=network.target

[Service]
ExecStartPre=/usr/bin/mkdir -p /tmp/readsb
ExecStart=readsb --device-type rtlsdr --device=0 --freq 1090000000 --gain -10 --lat YOUR_LAT --lon YOUR_LON --net --net-ro-port 30002 --net-sbs-port 30003 --write-json=/tmp/readsb
Restart=on-failure
RestartSec=10

[Install]
WantedBy=default.target
```

```bash
systemctl --user daemon-reload
systemctl --user enable readsb
systemctl --user start readsb
systemctl --user status readsb
```

Stop it before running SDR++Brown or any other SDR app:

```bash
systemctl --user stop readsb
```

## Optional: Feed Public Networks

All three accept feeder clients that connect to readsb's Beast port (30002). Check each for their feeder package:

- **FlightAware (FlightFeeder / piaware):** https://flightaware.com/adsb/piaware/install
- **ADS-B Exchange:** https://www.adsbexchange.com/how-to-feed/
- **adsb.fi:** https://adsb.fi/feed/

Running a feeder gives you access to their premium/unlimited tiers. Each feeder runs as a separate process connecting to port 30002 — readsb stays running, no extra dongle needed.

## 978 MHz UAT (Best-Effort)

The ADS-B mag mount is spec'd 900–1800 MHz but the manufacturer lists 978 MHz as compatible. UAT is used by lighter GA aircraft (Cessnas, Pipers) in the US below 18,000 ft.

Limitation: only one frequency at a time per dongle. To monitor 978 MHz:

```bash
# Run a separate readsb instance for UAT — swap frequency, different JSON dir
readsb --device-type rtlsdr --device=0 --freq 978000000 --gain -10 --lat YOUR_LAT --lon YOUR_LON \
  --net --net-ro-port 30004 --write-json=/tmp/readsb-uat
```

With one dongle you can only run one frequency at a time — stop the 1090 instance first. Two dongles would allow simultaneous 1090 + 978 coverage. For now, treat UAT monitoring as a separate session, not a parallel feed.

## What You'll See in Memphis

- **FedEx peak (22:00–06:00 local):** MD-11F, 767F, 777F, A300-600F in constant arrival/departure sequence on 36L/36R. Expect 30–50 aircraft visible simultaneously within 50 nm at altitude.
- **Daytime:** FedEx Express regional feeders (ATR-72, Cessna 208), Southwest/Delta/AA narrowbodies at KMEM, GA transiting the area.
- **Holding stacks:** Watch for FDX heavies stacked over the VOR/DME fixes south of the field during high-volume arrival pushes.
- **Range:** With the mag mount at elevation, expect 100–150 nm radius on cruise-altitude traffic. Local ground traffic depends heavily on antenna height.

## See Also

→ [[reference/readsb]]
→ [[Memphis Signals Reference]]

---
[< Previous: Exploration 06 — Ham Repeaters](../01-explorations/06-ham-repeaters.md) | [Next: Project 02 — IoT Dashboard >](./02-iot-dashboard.md)
