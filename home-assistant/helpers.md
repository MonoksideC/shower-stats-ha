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

## `input_number.shower_duration`

Purpose: Tracks if a shower session is currently running.

- **UI**: Create a *Number* in the Helpers section.  
- **Minimum value:** 2
- **Maximum value:** Your choice (I used 3600)
- **Display mode:** Input field
- **Step size:** 1
- **Unit of measurement:** s

## `sensor.shower_duration_display`

Purpose: Formats the duration (in seconds) for display (00m 00s)

- **UI**: Create a *Template -> Sensor* in the Helpers section.  
- **YAML** (add under `State template*:`):

```yaml
{% set total_seconds = states('input_number.shower_duration') | int %}
{% set minutes = total_seconds // 60 %}
{% set seconds = total_seconds % 60 %}
{{ minutes }}m {{ seconds }}s

## `input_number.shower_water_total`

Purpose: Tracks if a shower session is currently running.

- **UI**: Create a *Number* in the Helpers section.  
- **Minimum value:** 2
- **Maximum value:** Your choice (I used 1000)
- **Display mode:** Input field
- **Step size:** 0.01
- **Unit of measurement:** gal (or L if you use liters)