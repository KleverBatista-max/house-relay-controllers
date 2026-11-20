# House relay controllers (ESPHome + Zigbee + Home Assistant)

Everyday house automation, independent of the solar system: relay boards with physical switches that keep working without Home Assistant, plus a few small utilities.

| Path | What |
|---|---|
| `esphome/bedroomcontroller.yaml` | 3 relays + 3 wall switches (relay 3 powers a smart bulb) |
| `esphome/yardcontroller.yaml` | 3 relays + switches for the yard |
| `homeassistant/packages/house_controllers.yaml` | Lights on at sunset / off before sunrise, **fridge water-pump guard** (cuts it if it draws too much), **router auto-reboot** when the internet is down for 5 min (Zigbee plug, 15 min lock), relay energy sensors |
| `zigbee2mqtt/configuration.yaml` | Zigbee2MQTT config (network key redacted) |

## How the relay boards work
Both boards use the same pattern: **3 relays on GPIO 13, 12 and 14, and 3 wall switches on GPIO 26, 27 and 25** (pull-up, inverted, 30 ms debounce). A switch press toggles its relay *inside the ESP32*, so the lights keep working with Home Assistant or the Wi‑Fi down. Relays start **OFF** after a power cut.
- **Bedroom:** relay 3 starts **ON and stays on** because it powers a smart bulb; switch 3 instead asks Home Assistant to toggle that bulb (`light.toggle`).
- **Yard:** all three relays are plain on/off.

Part of the same house as [solar-inverter-modbus-monitor](https://github.com/KleverBatista-max/solar-inverter-modbus-monitor), [solar-ac-controller](https://github.com/KleverBatista-max/solar-ac-controller) and [bluetti-solar-charger](https://github.com/KleverBatista-max/bluetti-solar-charger), but it works on its own. Overview: [solar-home-overview](https://github.com/KleverBatista-max/solar-home-overview).

Created by **John Batista** ([@KleverBatista-max](https://github.com/KleverBatista-max)). Built with AI assistants (ChatGPT, Claude) as tools. MIT licensed. Secrets are not included; replace `!secret` values and regenerate ESPHome keys.
