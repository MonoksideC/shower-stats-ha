# Smart Shower + Home Assistant

ESP32‑based smart shower monitoring with two hall‑effect flow sensors (hot + cold), a DS18B20 temperature probe attached to the shower manifold, realtime dashboarding on Home Assistant, and a simple “shower session” tracker that totals water used and duration.

## Features
- Tracks hot and cold flow separately (L/min or gal/min) and combined total flow
- Temperature probe on manifold (fast and reliable with thermal compound + clamp)
- Automatic “shower session”: starts after 5s of flow, ends after 10s of no flow
- Records total water used per session and session duration
- Optional MQTT logging to external systems
- Lovelace dashboard for at‑a‑glance status and history

## Hardware Overview
This build used a thermostatic shower valve feeding **three outputs** (body jets, rainfall head, hand sprayer). Because of the multi‑output manifold, the temp sensor is **not inline**—it’s clamped to the brass manifold with thermal paste and a pipe‑friendly clamp. Delay to track water temp is minimal once water is flowing.

### Bill of Materials
See [`hardware/BOM.md`](hardware/BOM.md) and add your exact product links.

### Wiring
See [`hardware/wiring-notes.md`](hardware/wiring-notes.md) for pin map and installation notes.

## Firmware (ESPHome)
YAML lives in [`esphome/shower.yaml`](esphome/shower.yaml). It defines two `pulse_counter` sensors for flow and a OneWire DS18B20 for temperature, plus template + integration sensors to compute totals.

## Home Assistant Setup
- Create a few helpers (input_boolean & input_numbers) as listed in [`home-assistant/helpers.md`](home-assistant/helpers.md)
- Add the template sensors: [`home-assistant/template_sensors.yaml`](home-assistant/template_sensors.yaml)
- Import the automation for session tracking: [`home-assistant/automations/shower_session.yaml`](home-assistant/automations/shower_session.yaml)
- (Optional) Add the Lovelace view/cards: [`home-assistant/lovelace/shower-dashboard.yaml`](home-assistant/lovelace/shower-dashboard.yaml)

## Calibration
Do a bucket test to find the exact pulses‑per‑liter (or per‑gallon) for your specific flow sensors. Instructions in [`docs/calibration.md`](docs/calibration.md).

## FAQ
Common questions and fixes live in [`docs/faq.md`](docs/faq.md).

## License
This project is released under the [CC0 1.0 Public Domain Dedication](LICENSE).