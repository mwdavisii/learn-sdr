# Exploration 02: Airband Voice — KMEM Memphis International

## Why Airband

Aviation voice is 108–137 MHz and uses AM, not FM. This is a useful conceptual milestone: different services use different modulation for engineering reasons. Airband standardized on AM in the 1930s–40s because AM receivers were simpler and AM handled multipath interference better for the era.

KMEM is the FedEx global superhub — there is constant cargo aircraft traffic 24/7, day and night. You will never have to wait for a transmission.

## Frequencies to Monitor

| Service | Frequency (MHz) | Mode | Notes |
|---------|-----------------|------|-------|
| ATIS (D-ATIS) | 127.75 | AM | Automated terminal info; listen first |
| Clearance Delivery | 125.2 | AM | IFR clearances before pushback |
| Ground — RWY 09/27 | 121.65 | AM | North complex ground control |
| Ground — RWY 18/36 | 121.9 | AM | South/center complex ground control |
| Tower — RWY 09/27 | 118.3 | AM | Main tower frequency |
| Tower — RWY 18L/36R & 18C/36C | 128.425 | AM | South runway complex tower |
| Approach — hdg 176–355° (N) | 119.1 | AM | Memphis TRACON north sector |
| Approach — hdg 356–175° (S) | 125.8 | AM | Memphis TRACON south sector |
| Departure — hdg 356–175° | 124.15 | AM | TRACON departure north |
| Departure — hdg 176–355° | 124.65 | AM | TRACON departure south |
| UNICOM | 122.95 | AM | General aviation advisory |
| Guard (Emergency) | 121.5 | AM | International distress; always monitored |

**Start with ATIS.** It's a looping automated broadcast — always transmitting, no waiting.

## Tuning In

**Tool:** SDR++Brown
**Mode:** AM
**Bandwidth:** ~8–10 kHz

1. Tune to the ATIS frequency (127.75 MHz)
2. Switch demodulation mode to AM
3. Set bandwidth to ~8 kHz
4. Listen — you'll hear the automated weather/runway briefing

**What you're hearing on ATIS:** Current weather, active runways, altimeter setting, NOTAM summary. Updates hourly (or when conditions change); each iteration is assigned an alphabet letter ("information Bravo").

**What you're hearing on Approach:** Controllers vectoring inbound aircraft to the ILS final approach. Listen for FedEx callsigns: "FDX" + 3-digit flight number (e.g., "FedEx 210, turn left heading 180, descend and maintain 3,000").

**What you're hearing on Tower:** Takeoff and landing clearances. Busiest between roughly 22:00–06:00 local (FedEx sort operations).

## AM vs FM — Why It Matters

In SDR++Brown, try switching the same airband signal between AM and NFM modes. AM sounds clear; NFM sounds wrong (clipped, distorted). This is because:
- AM encodes information in amplitude variation
- FM encodes it in frequency deviation
- The demodulator has to match the modulation or you get garbage

## What to Try Next
→ [[03-aprs]] — decode data packets on 144.390 MHz
→ [[Memphis Signals Reference]] — full frequency table

---
[< Previous: Exploration 01 — FM & NOAA](./01-fm-and-noaa.md) | [Next: Exploration 03 — APRS >](./03-aprs.md)
