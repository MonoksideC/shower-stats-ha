# Wiring Notes

- **Flow sensors**: connect signal pins to your choice of pins on the ESP32.  I used `GPIO35` (hot) and `GPIO34` (cold), powered by the 5v side.
- **Temp sensor (DS18B20)**: OneWire on `GPIO4` (again, your choice, just change in the esphome yaml as needed) with a 4.7k pull‑up to 3.3V.  The temp probed linked in the BOM has the 4.7k pull-up resistor included.
- **Mounting**: DS18B20 probe pressed flush to brass manifold with a thin layer of thermal paste under a clamp; cable routed through wall and back to the ESP32 via a conduit (I just used some pex since I was already running it)

You can either solder the wires, or you can use dupont jumper wire (that's what I did) and just plug it in to the gpio header on the esp32, and then into the connectors on the sensors.