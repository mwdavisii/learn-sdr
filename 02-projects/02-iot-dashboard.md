# Project 02: IoT Sensor Dashboard — Home Assistant

## Overview

Build on [[01-explorations/04-iot-sensors]]. Instead of printing decoded sensor data to the terminal, pipe it into the Mosquitto broker on your existing Home Assistant instance. HA auto-discovers the sensors via MQTT discovery — they appear as native HA entities automatically.

**Prerequisites:**
- Home Assistant running with Mosquitto add-on installed (already done)
- Know your HA host IP (e.g., 192.168.1.x)
- MQTT port: 1883 (default)
- If HA MQTT requires auth: HA → Settings → Integrations → MQTT → Configure to find credentials

## Basic Command

```bash
# Close SDR++Brown/GQRX first — exclusive device access
rtl_433 -F mqtt://192.168.1.x:1883 -M homeassistant
```

Replace `192.168.1.x` with your HA host IP.

## With Authentication

If your Mosquitto requires credentials:

```bash
rtl_433 -F mqtt://username:password@192.168.1.x:1883 -M homeassistant
```

Credentials are from HA → Settings → Integrations → MQTT.

## How Auto-Discovery Works

With `-M homeassistant`, rtl_433 publishes two MQTT messages per device:
1. A discovery config payload to `homeassistant/sensor/rtl_433_<device_id>/config`
2. State updates to `rtl_433/<device_model>/<device_id>/...`

HA's MQTT integration watches the `homeassistant/` prefix and auto-creates entities. New sensors appear in: Settings → Devices & Services → MQTT → Devices.

No manual YAML configuration required.

## Also Log to Terminal

Run both MQTT output and JSON terminal output simultaneously:

```bash
rtl_433 -F mqtt://192.168.1.x:1883 -M homeassistant -F json
```

## Running Continuously as a systemd Service

To keep rtl_433 running persistently as a user service:

```ini
# ~/.config/systemd/user/rtl433-ha.service
[Unit]
Description=rtl_433 MQTT bridge to Home Assistant
After=network.target

[Service]
ExecStart=/run/current-system/sw/bin/rtl_433 -F mqtt://192.168.1.x:1883 -M homeassistant
Restart=on-failure
RestartSec=10

[Install]
WantedBy=default.target
```

```bash
# Install and start
systemctl --user daemon-reload
systemctl --user enable rtl433-ha
systemctl --user start rtl433-ha
systemctl --user status rtl433-ha
```

**Important:** The service holds the RTL-SDR device. Stop it before running SDR++Brown or other SDR tools:
```bash
systemctl --user stop rtl433-ha
```

## Gotchas

- `rtl_433` binary path in the service file may differ on your system. Check: `which rtl_433`
- If HA doesn't show new devices, verify the MQTT integration is active (Settings → Integrations → MQTT) and that Mosquitto is accepting connections
- Tire pressure sensors only appear when a vehicle with TPMS is nearby — bursts, not continuous

## See Also

→ [[01-explorations/04-iot-sensors]]
→ [[rtl_433]]

---
[< Previous: Project 01 — ADS-B Aircraft Map](./01-adsb-aircraft-map.md) | [Next: Project 03 — APRS Station >](./03-aprs-station.md)
