Personal SDR frequency reference for Memphis, TN.
RTL-SDR dongle. Receive-only — no transmit license required to listen.

---

## Aviation — KMEM Memphis International

All airband voice is **AM mode**. KMEM is a Class B airport and one of the
world's busiest cargo hubs (FedEx World Hub). Activity is heavy 24/7.

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
| Guard (Military) | 243.0 | AM | Military UHF guard; RTL-SDR max ~1.7 GHz |

**LiveATC stream for KMEM:** https://www.liveatc.net/search/?icao=KMEM

**Tip:** Start with 127.75 (ATIS) to learn active runways, then switch to the
corresponding tower. FedEx flights use callsign FDX + flight number (e.g., FDX1234).

---

## NOAA Weather Radio

| Station | Frequency (MHz) | Mode | Call Sign | Coverage |
|---------|-----------------|------|-----------|----------|
| Memphis NWS | 162.550 | NFM | WXL-48 | Mid-South (TN/MS/AR) |

**Tip:** WXL-48 broadcasts continuous weather, watches, and warnings. Strong
signal in most of Shelby County — one of the easiest first receptions on RTL-SDR.

---

## APRS

| Service | Frequency (MHz) | Mode | Notes |
|---------|-----------------|------|-------|
| APRS North America | 144.390 | NFM | 1200 baud AFSK; packet bursts every few seconds |
| APRS Digipeater (W4BS) | 144.390 | NFM | W4BS system has a digipeater at Methodist North Hospital |

**Decoding:** Use `direwolf` or `multimon-ng` piped from `rtl_fm`.

**Find local digipeaters and mobile stations:** https://aprs.fi — search `W5MEM`
or `W4BS` to see Memphis-area activity. A busy FedEx parking lot or highway will
show constant pings.

---

## ADS-B / Aircraft Transponders

| Service | Frequency (MHz) | Mode | Notes |
|---------|-----------------|------|-------|
| Mode S / ADS-B (1090ES) | 1090 | — | All commercial aircraft; FedEx hub = constant traffic |
| UAT (ADS-B 978) | 978 | — | General aviation only; sparser traffic |

**RTL-SDR notes:**
- 1090 MHz is near the upper limit of RTL-SDR v3; use a dedicated ADS-B antenna
  (simple 1/4-wave ground plane or FlightAware antenna) for best range.
- Decode with `readsb` or `dump1090-fa`; visualize with tar1090 or FlightAware.
- Memphis FedEx hub means 100+ aircraft can be visible simultaneously overnight.
- 978 MHz UAT requires RTL-SDR at 978 MHz center; decode with `dump978-fa`.

---

## ISM / IoT Sensors

| Band | Frequency (MHz) | Mode | Common Devices |
|------|-----------------|------|----------------|
| 433 MHz ISM | 433.92 | OOK/ASK | Weather stations, doorbells, tire pressure monitors, remotes |
| 315 MHz ISM | 315.00 | OOK/ASK | Older garage door openers, some car key fobs, remotes |

**Decoding:** `rtl_433` supports both bands automatically.
```
rtl_433 -f 433920000 -f 315000000 -M time -F json
```
Neighbors' weather stations and tire pressure sensors will appear immediately.
See the [rtl_433 device list](https://github.com/merbanan/rtl_433/tree/master/conf)
for supported protocols.

---

## FM Broadcast

Scan **88–108 MHz**, NFM, ~200 kHz bandwidth. The waterfall will reveal all
active stations faster than any list. A few known Memphis anchors:

| Callsign | Frequency (MHz) | Format |
|----------|-----------------|--------|
| WQOX | 88.5 | Oxford/Ole Miss Public Radio |
| WYPL | 89.3 | Memphis Public Library / Jazz |
| WEVL | 90.1 | Volunteer/community variety |
| WKNO | 91.1 | NPR / PBS affiliate |
| WMC | 100.1 | Hot AC |
| KJMS | 101.1 | Gospel / Urban |
| WEGR | 102.7 | Classic Rock ("Rock 103") |
| WRVR | 104.5 | Contemporary Christian |
| WGKX | 106.1 | Country ("KIX 106") |
| KXHT | 107.1 | Hip-Hop / R&B ("Hot 107") |

**Tip:** FM stereo pilot tone is at 19 kHz above carrier — visible in the
waterfall as a thin line. SDR++ and GQRX both decode stereo automatically.

---

## Ham Radio — VHF/UHF Repeaters

All are **NFM mode**. Receive-only — no license needed to listen.
Transmitting on repeaters requires a Technician class license or higher.

### Memphis-Area Repeaters

| Output (MHz) | Offset | PL Tone | Callsign | Notes |
|--------------|--------|---------|----------|-------|
| 146.820 | −600 kHz | 107.2 Hz | W4BS | Delta ARC anchor repeater; WATN TV tower, Brunswick TN (~500 ft); Skywarn primary; nightly info net 8 PM |
| 146.625 | −600 kHz | 107.2 Hz | W4BS | Germantown water tower; AllStar/Echolink linked; good south-county coverage |
| 147.360 | +600 kHz | 107.2 Hz | W4BS | Methodist North Hospital; "no frills" Icom FR3000 |
| 443.200 | +5 MHz | 107.2 Hz | W4BS | University of Memphis area; 440 drive-time machine; Icom FR4000 |
| 443.700 | +5 MHz | DMR CC1 | W4BS | WATN tower; DMR digital (Motorola SLR5700); not audible on analog NFM |
| 146.730 | −600 kHz | 107.2 Hz | — | MedMERS primary; medical emergency communications |
| 146.880 | −600 kHz | 107.2 Hz | — | ARES #1; Shelby County emergency net |
| 146.850 | −600 kHz | no tone | — | ARES #2; open repeater |
| 147.090 | +600 kHz | 107.2 Hz | — | CUSEC #1; Central US Earthquake Consortium |
| 145.210 | −600 kHz | 107.2 Hz | — | MARA (Memphis Amateur Radio Assn) |
| 444.700 | +5 MHz | 107.2 Hz | — | Memphis area; verify current status on repeaterbook.com |

### National Calling Frequencies (Simplex)

| Frequency (MHz) | Mode | Use |
|-----------------|------|-----|
| 146.520 | NFM | 2m FM simplex national calling frequency; no PL tone |
| 446.000 | NFM | 70cm FM simplex national calling frequency; no PL tone |

**Finding more repeaters:**
- https://www.repeaterbook.com — search Tennessee, filter by Shelby County
- https://deltaclub.org/repeaters — Delta Amateur Radio Club Memphis listing
- W4BS system info: https://deltaclub.org

---

## FedEx Operations

FedEx World Hub at KMEM is the largest cargo airport hub on earth by volume.
FedEx uses licensed commercial aviation frequencies not publicly documented
in FAA databases.

**What you can do:** Monitor KMEM tower and approach frequencies (listed above)
and listen for FedEx callsigns — format is **FDX** followed by flight number
(e.g., *FedEx 1234*, spoken as *"FedEx twelve thirty-four"* or *"FedEx one
two three four"*).

Overnight sort operations (roughly 23:00–05:00 local) produce the highest
traffic density. You may hear 30+ FedEx aircraft in sequence on a single
tower frequency during the sort window.

---

*Frequencies verified against OurAirports, AirNav (KMEM), Delta Amateur Radio
Club repeater list, and W5HAR Memphis Metro net listings. Verify current status
for repeaters at repeaterbook.com. Last researched: March 2026.*
