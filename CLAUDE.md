# SDR Assistant Context

## Hardware
- Dongle: RTL-SDR Blog V3 (RTL2832U + Rafael Micro R820T2)
  - Note: stock `rtl-sdr` driver (v2.0.2) misidentifies tuner as R820T; confirmed V3 via `rtl_biast`
  - TCXO, bias-T, and HF direct sampling available
- Tuning range: ~24–1766 MHz (hardware limit; software may show wider)
- Current antenna: stock telescoping whip
- Incoming antenna: ADS-B mag mount, 6 dBi, 900–1800 MHz + 978 MHz compatible (arriving ~2026-04-01)
  - Use for: 1090 MHz ADS-B (primary), 978 MHz UAT (best-effort)
  - Keep stock whip for: FM, airband, APRS, 433 MHz

## Software Stack (Arch Linux + Nix)
| Tool | Purpose | Used In |
|------|---------|---------|
| SDR++Brown | Primary wideband receiver + waterfall GUI | All explorations |
| GQRX | Secondary receiver; better for IQ recording | 05-signal-analysis |
| rtl_fm | CLI tuner; used in pipe-based decode pipelines | 03-aprs |
| rtl_433 | Decoder for 433 MHz ISM sensors | 04-iot-sensors, 02-iot-dashboard |
| readsb | ADS-B Mode S decoder (1090 MHz aircraft) | 01-adsb-aircraft-map |
| multimon-ng | Multi-protocol decoder (APRS, POCSAG, DTMF) | 03-aprs, 03-aprs-station |
| inspectrum | IQ file visual signal analysis | 05-signal-analysis |
| Home Assistant | Existing HA instance; has Mosquitto MQTT broker | 02-iot-dashboard |

Note: inspectrum installed via pacman, not Nix — invoke from standard shell, not Nix shell.

## Memphis, TN Context
- Notable: KMEM is FedEx global superhub — constant aircraft traffic 24/7
- Key signals: see reference/memphis-signals.md
- Nearest NOAA NWS: Memphis on 162.550 MHz

## How to Help in This Directory

You are assisting a developer learning SDR from scratch. They accelerate quickly once they grasp patterns.

**Response style:**
- Terse. Brief "why" context is welcome; hand-holding is not.
- Commands go in code blocks always.
- Frequency lookups → table format.
- Assume Linux proficiency; no need to explain pipes, sudo, file paths.

**Common requests:**
- "What frequency is X?" → look up, return table with freq + mode + notes
- "How do I decode X?" → provide exact pipeline command
- "What's this signal?" → describe characteristics, suggest identification approach
- "Why does X happen in SDR?" → brief conceptual explanation
- Debugging SDR pipelines → check: device in use? wrong mode? gain too high/low? PPM offset?

**SDR debugging checklist:**
1. Is `dvb_usb_rtl28xxu` kernel module loaded? (`lsmod | grep dvb`) — blacklist it if so
2. Is another app holding the device? (only one app can use the dongle at a time)
3. Is gain appropriate? (auto gain is fine to start; too high = noise floor rises)
4. Is PPM correction set? (run `rtl_test -p` to measure; typical range -20 to +20)
