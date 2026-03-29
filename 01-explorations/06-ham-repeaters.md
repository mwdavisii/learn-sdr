# Exploration 06: Ham FM Repeaters — 2m and 70cm

## Why This Band

The 2m (144–148 MHz) and 70cm (420–450 MHz) ham bands are full of local FM repeaters — community infrastructure built and maintained by amateur radio operators. You can receive them with no license. They're a good window into local emergency comms, weekly nets, and everyday ham radio activity.

**HF ham bands (40m, 20m, 80m, etc. — below 24 MHz) are not reachable with the RTL-SDR without a hardware modification.** Stick to VHF/UHF.

## Tuning In

**Tool:** SDR++Brown
**Mode:** NFM (Narrowband FM)
**Bandwidth:** ~10–15 kHz (same as NOAA weather radio)

Key Memphis-area repeaters to start with:

| Callsign | Output Freq | Offset | PL Tone | Notes |
|----------|-------------|--------|---------|-------|
| W4BS | 146.820 MHz | −600 kHz | 110.9 Hz | Primary W4BS group; most active |
| W4BS | 147.195 MHz | +600 kHz | 110.9 Hz | W4BS group, alternate machine |
| W5CUB | 147.345 MHz | +600 kHz | 131.8 Hz | 50W output |
| WA4GYF | 442.725 MHz | +5 MHz | 100.0 Hz | 70cm; good for testing UHF range |

Full list: [[Memphis Signals Reference#ham-radio-vhfuhf-repeaters]]

**Start here:** Tune to **146.520 MHz** — the national 2m FM simplex calling frequency. Any ham within RF range calling CQ will be heard here. Then try local repeater output frequencies from the reference.

## How Repeaters Work

A repeater listens on its *input* frequency and simultaneously re-transmits on its *output* frequency at higher power. You tune to the output (what you hear). When someone transmits on the input, the repeater activates and you hear them on the output.

- **2m offset:** −600 kHz (output is 600 kHz lower than input)
- **70cm offset:** −5 MHz (output is 5 MHz lower than input)

Repeaters are often quiet for long stretches. Traffic peaks during:
- Scheduled weekly nets (check individual repeater listings)
- Severe weather (ham operators activate for weather spotting)
- Public events (Memphis in May, St. Jude Marathon)
- Emergencies (ARES/RACES activations)

## PL Tones (CTCSS)

Most repeaters require a sub-audible PL (Private Line / CTCSS) tone to open the squelch. **PL is Motorola's trademark name; CTCSS (Continuous Tone-Coded Squelch System) is the generic term — same thing.**

The tone numbers (e.g., 110.9 Hz, 131.8 Hz) are literal audio frequencies in Hz — specific sine waves below the human voice range (~300 Hz+). The transmitter sends that tone continuously underneath the voice audio the entire time they key up. The repeater's receiver has a filter tuned to that exact frequency; it only opens squelch when it detects the right tone. This keeps the repeater quiet from accidental triggers — other FM carriers, intermod, distant signals — since normal speech and noise don't contain a steady pure tone at, say, 110.9 Hz. Think of it as a hardware key.

The specific frequencies were chosen to fall between harmonics of common voice fundamentals, minimizing false triggers from speech.

**You don't need to transmit one to *receive*.** Since we're just listening on the output frequency, the PL requirement is irrelevant — it only gates the repeater's input. Just tune to the output and listen.

If a repeater seems dead, it may just be quiet rather than broken. Try monitoring during peak hours (evening drive time, 17:00–19:00 local).

In SDR++Brown you can sometimes see the PL tone as a very low-frequency component (<300 Hz) in the audio spectrum — it won't affect your listening.

## Digital Modes on Ham VHF/UHF

Some repeaters carry digital voice modes:
- **DMR** — Digital Mobile Radio (sounds like buzzing static on NFM)
- **D-STAR** — Icom's digital voice (similar buzzing)
- **Fusion / C4FM** — Yaesu's system

These require separate software to decode (DSD+, DVMega, etc.) and are out of scope for this exploration. When you hear buzzing instead of voice on a repeater frequency, it's probably digital voice.

APRS at 144.390 MHz is also a ham VHF signal — covered in [[03-aprs]].

## What to Try Next

→ [[Memphis Signals Reference]] — full repeater frequency table
→ [[03-aprs]] — another 2m band signal (data instead of voice)
→ [[01-fm-and-noaa]] — NFM mode refresher (same demodulation used here)
