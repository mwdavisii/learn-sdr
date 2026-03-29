

## What It Is

readsb is an ADS-B Mode S decoder. It listens on 1090 MHz, decodes aircraft transponder broadcasts, and outputs to network ports (Beast/AVR/SBS format) and/or JSON files. Used with tar1090 for the local aircraft map.

## Key Flags

| Flag | Purpose |
|------|---------|
| `--device-index 0` | Select first RTL-SDR |
| `--gain -10` | Auto gain (recommended starting point) |
| `--freq 1090000000` | 1090 MHz (ADS-B Mode S) |
| `--net` | Enable network output (Beast port 30005, SBS port 30003) |
| `--json-dir /path` | Write JSON state files for tar1090 |
| `--write-json-every 1` | Update JSON every 1 second |
| `--net-connector host,port,format` | Feed data to a remote host |

## Common Invocation

```bash
mkdir -p /tmp/readsb

readsb \
  --device-index 0 \
  --gain -10 \
  --freq 1090000000 \
  --net \
  --json-dir /tmp/readsb \
  --write-json-every 1
```

## tar1090 Integration

tar1090 reads aircraft.json from `--json-dir`. Start readsb first, then open tar1090. It serves a web map at `http://localhost:8080` by default. See [[02-projects/01-adsb-aircraft-map]] for full setup.

## Feeding Networks

```bash
# FlightAware
readsb ... --net-connector feed.flightaware.com,1200,beast_out

# ADS-B Exchange
# Use adsbexchange-feed package (check nixpkgs or ADS-B Exchange install script)
```

Feeding gives you a personal stats page showing your coverage range and aircraft count.

## Gotchas

- Requires ADS-B antenna for useful range. The stock whip will decode aircraft overhead but misses anything more than a few km away at 1090 MHz.
- Holds the RTL-SDR device exclusively. Close SDR++Brown/GQRX before running.
- `--gain -10` means auto gain, not −10 dB. readsb uses −10 as the sentinel value for "let the driver decide."

## See Also

→ [[02-projects/01-adsb-aircraft-map]]
→ [[Memphis Signals Reference]] (KMEM/FedEx context)
