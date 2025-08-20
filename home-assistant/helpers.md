# Helpers

You’ll need a few helpers to track shower sessions.  
Create them in **Settings → Devices & Services → Helpers**.  

---

## `binary_sensor.shower_active`

Purpose: Tracks if a shower session is currently running.

- **UI**: Create a *Template Binary Sensor* in the Helpers section.  
- **YAML** (add under `State template*:`):

```yaml
{{ states('sensor.esphome_shower_temp_hot_water_flow')|float > 0.3 or states('sensor.esphome_shower_temp_cold_water_flow')|float > 0.3 }}

- `input_number.shower_duration`
- `sensor.shower_duration_display`
- `input_number.shower_water_total`