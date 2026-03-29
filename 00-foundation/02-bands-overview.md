# Bands Overview

Your RTL-SDR covers roughly **24 MHz – 1766 MHz**. The stock whip is best below ~500 MHz; the incoming ADS-B antenna handles 978–1090 MHz. Below 24 MHz and above 1766 MHz requires different hardware.

## Spectrum Map

| Band | Frequency Range | What's There | RTL-SDR | Antenna | Start Here |
|------|----------------|--------------|---------|---------|------------|
| VLF/LF | < 30 MHz | Time signals, naval comms | ❌ | — | — |
| HF (Shortwave) | 3–30 MHz | Shortwave broadcast, ham radio | ❌ | — | — |
| VHF Low | 30–88 MHz | Aviation nav (VOR), some paging | ✅ | Stock whip | — |
| FM Broadcast | 88–108 MHz | Commercial FM radio | ✅ | Stock whip | Exploration 01 |
| VHF High | 108–174 MHz | Airband (108–137), NOAA (162), APRS (144), **2m ham (144–148)** | ✅ | Stock whip | Explorations 01–03, 06 |
| UHF Low | 300–512 MHz | FRS/GMRS, 433 MHz ISM, 315 MHz ISM, **70cm ham (420–450)** | ✅ | Stock whip | Explorations 04, 06 |
| UHF Mid | 512–960 MHz | Cellular (historical), paging, some TV | ✅ | Stock whip | — |
| L-Band | 960–1559 MHz | ADS-B 1090 MHz, GPS 1575 MHz, UAT 978 MHz | ✅ | ADS-B antenna | Project 01 |
| S-Band | 2–4 GHz | Wi-Fi, weather radar | ❌ | — | — |

Note: "❌ RTL-SDR" means below/above hardware range. Direct-sampling mods can extend HF coverage but are out of scope here.

## Memphis-Relevant Highlights

| Frequency | What | Mode | Notes |
|-----------|------|------|-------|
| 88–108 MHz | FM broadcast | WFM | Strongest signals you'll see |
| 121.5 MHz | Airband emergency / guard | AM | International guard frequency |
| 144.390 MHz | APRS | NFM | North American APRS calling freq |
| 162.550 MHz | NOAA Weather Radio | NFM | Memphis NWS |
| 433.92 MHz | ISM sensors | varies | Neighbors' weather stations, doorbells |
| 978 MHz | ADS-B UAT | — | General aviation (best-effort) |
| 1090 MHz | ADS-B Mode S | — | Commercial aircraft; FedEx hub = constant |

Full local frequency index: [[Memphis Signals Reference]]
