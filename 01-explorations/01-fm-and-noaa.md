# Exploration 01: FM Broadcast + NOAA Weather Radio

## Why Start Here

FM broadcast is the loudest, widest signal you'll see. It's impossible to miss on the waterfall — bright stripes every 200 kHz across 88–108 MHz. It's the "hello world" of SDR: if you can hear music, your setup works.

## Part 1: FM Broadcast

**Tool:** SDR++Brown
**Mode:** WFM (Wideband FM)
**Frequency:** Anywhere in 88–108 MHz

1. Open SDR++Brown → Source → RTL-SDR → click ▶ Play
2. Set center frequency to 98.0 MHz
3. Watch the waterfall — bright vertical stripes = FM stations
4. Click on the brightest stripe; set demodulation mode to WFM
5. Adjust bandwidth slider (~200 kHz for FM)
6. Adjust volume / audio gain

**What you're seeing:** Each stripe is one FM station's carrier. Stereo FM uses a 38 kHz subcarrier (visible as a second stripe close to the main one). RDS data rides on 57 kHz (barely visible as shimmer).

**Try:** Tune to WKNO 91.1 (NPR Memphis). Note the signal is stable and clean at full extension of the whip.

## Part 2: NOAA Weather Radio — 162.550 MHz

**Tool:** SDR++Brown
**Mode:** NFM (Narrowband FM)
**Frequency:** 162.550 MHz

1. Tune to 162.550 MHz
2. Switch mode to NFM
3. Set bandwidth to ~10–15 kHz

**What's different:** Compare the waterfall here to FM. NOAA is a narrow stripe (10 kHz vs. FM's 200 kHz). NFM requires tighter bandwidth settings — too wide and you hear noise from adjacent channels; too narrow and audio sounds muffled.

**What you're hearing:** Automated voice reading Memphis-area weather observations, forecasts, and alerts. Station WXL-48 broadcasts 24/7.

**Why this matters:** You've just used two demodulation modes (WFM vs NFM). This distinction — and understanding *why* different signals use different modes — applies to everything else you'll receive.

## What to Try Next
→ [[02-airband-voice]] — AM demodulation at KMEM
→ [[SDR++Brown]] — SDR++Brown settings reference

---
[< Previous: Antenna Guide](../00-foundation/04-antenna-guide.md) | [Next: Exploration 02 — Airband Voice >](./02-airband-voice.md)
