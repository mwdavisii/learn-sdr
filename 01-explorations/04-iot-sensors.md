# Exploration 04: IoT Sensors — 433 MHz ISM Band

## Why This Band

The 433.92 MHz ISM band is an unlicensed free-for-all. Consumer devices broadcast temperature, humidity, rain gauge readings, tire pressure, door sensors, pool sensors, and more — unencrypted, at low power, constantly. rtl_433 ships with decoders for 200+ devices; point it at 433 MHz and see what your neighbors are broadcasting.

This is usually the fastest gratification in SDR: within 5 minutes of running rtl_433, you'll typically see real sensor data.

## Basic Scan

```bash
# Close SDR++Brown/GQRX first
rtl_433
```

rtl_433 defaults to 433.92 MHz with all decoders enabled. Watch the terminal — decoded packets appear as they arrive.

## JSON Output

```bash
rtl_433 -F json
```

Sample output:
```json
{"time":"2026-03-29 08:15:02","model":"Acurite-606TX","id":147,
 "channel":1,"battery_ok":1,"temperature_C":18.2,"mic":"CHECKSUM"}
```

JSON is pipe-friendly — useful for logging or later analysis.

## What to Expect

In a residential neighborhood you'll typically see within a few minutes:
- **Acurite / Oregon Scientific / LaCrosse** weather stations (temperature, humidity)
- **TPMS** (tire pressure monitoring) from cars driving past — brief bursts
- **Doorbells** (when pressed nearby)
- **Pool sensors**, remote thermometers, soil moisture sensors

The variety depends on your neighbors' devices. More devices = more decodes.

## 315 MHz Band

Some older US devices use 315 MHz instead of 433.92 MHz — common for certain garage door openers and RF remotes:

```bash
rtl_433 -f 315M
```

## Analyzing Unknown Signals

If rtl_433 shows "PULSE_PCM" or similar but no model name, the signal is unrecognized. Try:

```bash
rtl_433 -A -f 433.92M
```

This shows the raw pulse timing, which can help identify the protocol.

## What to Try Next
→ [[02-projects/02-iot-dashboard]] — push decoded sensors to Home Assistant via MQTT
→ [[rtl_433]] — full rtl_433 flag reference
