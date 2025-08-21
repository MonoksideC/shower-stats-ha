# Smart Shower + Home Assistant

ESP32‑based smart shower monitoring with two hall‑effect flow sensors (hot + cold), a DS18B20 temperature probe attached to the shower manifold, realtime dashboarding on Home Assistant, and a simple “shower session” tracker that totals water used and duration.

## Features
- Tracks hot and cold flow separately (L/min or gal/min) and combined total flow
- Temperature probe on manifold (fast and reliable with thermal compound + clamp)
- Automatic “shower session”: resets stats to 0 when water flow is detected
- Records total water used per session and session duration

## Hardware Overview
This build used a shower with a thermostatic valve feeding **three outputs** (body jets, rainfall head, hand sprayer). [`https://www.amazon.com/dp/B0C2T9R7WP`](link).  Thermostatic valves adjust the hot and cold water allowed through so that it keeps a set temperature.  Pretty nice, but infortunately, it makes it where I can't adjust the temperature from HA.  With that type of valve, if you were to, for example, use a valve and reduce the flow rate of the hot water, the thermostatic valve is just gonna reduce the amount of cold water allowed through.

Also, because of the multi‑output manifold, the temp sensor is **not inline**.  It’s attached to the brass manifold with thermal paste and a pipe‑friendly clamp. Delay to track water temp is minimal once water is flowing so it works pretty well.  With a different shower, you might be able to use a fitting to put the temp sensor directly in the water flow.  

## Frame
For the frame, I modeled a mount in Fusion for the specific monitor that I used, and 3d printed it in white.  That's the "mat" in the center.  Then I just cut and painted some 1x2 for the frame. I've included the 3d model if anyone wants to either use that specific monitor or modify it for a different one. [`models/monitor-mount.f3d`](models/monitor-mount.f3d)

## Shower
[`[hardware/BOM.md](https://www.amazon.com/dp/B0C2T9R7WP)`](Here's the shower that I used).  It has 

### Bill of Materials
See [`hardware/BOM.md`](hardware/BOM.md).

### Wiring
See [`hardware/wiring-notes.md`](hardware/wiring-notes.md) for pin map and installation notes.

## Firmware (ESPHome)
YAML lives in [`esphome/shower.yaml`](esphome/shower.yaml). It defines two `pulse_counter` sensors for flow and a OneWire DS18B20 for temperature, plus template + integration sensors to compute totals.

## Home Assistant Setup
- Create a few helpers (input_boolean & input_numbers) as listed in [`home-assistant/helpers.md`](home-assistant/helpers.md)
- Add the template sensors: [`home-assistant/template_sensors.yaml`](home-assistant/template_sensors.yaml)
- Import the automations for session tracking: [`home-assistant/automations/`](link)

## Calibration
The flow sensors I used are specified at 300 pulses per liter, and the ESP config reflects that.  If you use different sensors, you can calibrate them but filling a 5 gallon bucket and comparing that to what the sensors show in the esphome dashboard.

## License
This project is released under the [CC0 1.0 Public Domain Dedication](LICENSE).
