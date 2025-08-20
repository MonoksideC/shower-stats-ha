# Wiring Notes

- **Flow sensors**: connect signal pins to ESP32 `GPIO35` (hot) and `GPIO34` (cold) with 5V->3.3V safe logic (most sensors are open‑collector with pull‑ups on 5V boards; prefer 3.3V pull‑ups or level shifting). Ground all commons.
- **Temp sensor (DS18B20)**: OneWire on `GPIO4` with a 4.7k pull‑up to 3.3V.
- **Power**: Stable 5V supply to ESP32; avoid noisy pump circuits.
- **Mounting**: DS18B20 probe pressed flush to brass manifold with a thin layer of thermal paste under a clamp; route cable away from hot surfaces.