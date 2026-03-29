# RTL-SDR Getting Started Guide (Linux)

A progressive getting-started guide for RTL-SDR on Linux, structured as a personal knowledge base. Built for developers who are new to radio but not new to computers.

## Hardware

- **Dongle:** RTL-SDR RTL2832U + Rafael Micro R820T2 (~$25–35)
- **Tuning range:** ~24–1766 MHz
- **Antenna:** Stock telescoping whip works for most explorations; a dedicated ADS-B mag mount is used for the aircraft tracking project

## Software Stack

All tools are open source and available on most Linux distributions.

| Tool | Purpose |
|------|---------|
| SDR++Brown | Primary wideband receiver + waterfall GUI |
| GQRX | Secondary receiver; better for IQ recording |
| rtl_433 | Decoder for 433 MHz ISM band IoT sensors |
| readsb | ADS-B Mode S decoder for aircraft tracking |
| multimon-ng | Multi-protocol decoder (APRS, POCSAG, DTMF) |
| inspectrum | IQ file visual signal analysis |

## Structure

```
00-foundation/   — Core concepts: how SDR works, spectrum overview, hardware setup, antennas
01-explorations/ — Guided hands-on sessions (FM, airband, APRS, IoT sensors, signal analysis, ham repeaters)
02-projects/     — Longer-form setups that produce a persistent data stream or service
reference/       — Per-tool reference + local signal frequency index
```

**Start here:** `00-foundation/01-how-sdr-works.md`

## Local Signals

The `reference/memphis-signals.md` file contains a frequency index for Memphis, TN (KMEM airport, NOAA weather radio, APRS, local ham repeaters, ISM band). If you're not in Memphis, you can use it as a template and substitute your local frequencies via [AirNav](https://www.airnav.com), [RadioReference](https://www.radioreference.com), and [RepeaterBook](https://www.repeaterbook.com).

## Notes

- Written and maintained as an [Obsidian](https://obsidian.md) notebook. Internal links use `[[wikilink]]` syntax, which renders natively in Obsidian but appears as plain text on GitHub.
- Installation examples reference Arch Linux with the Nix package manager. Commands are straightforward to adapt to other distributions.
- This is receive-only. No transmit capability is covered.

## License

[CC BY 4.0](LICENSE) — free to use, share, and adapt with attribution.
