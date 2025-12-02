# ESPHome HeatpumpIR with Mitsubishi PLA Protocol

Custom ESPHome external component that adds the `mitsubishi_pla` protocol for Mitsubishi PLA series ceiling cassettes using the W001CP remote.

## Why?

The upstream `mitsubishi_sez` protocol has incorrect fan speed byte position and values for PLA series units with W001CP remotes:

| Issue | mitsubishi_sez (wrong) | mitsubishi_pla (correct) |
|-------|------------------------|--------------------------|
| Fan speed byte | Byte 7 | Byte 8 |
| Low | 0x32 | 0x04 |
| Med-Low | 0x34 | 0x24 |
| Medium | 0x36 | 0x44 |
| High | - | 0x64 |

## Usage

```yaml
external_components:
  - source:
      type: git
      url: https://github.com/troykelly/esphome-heatpumpir
      ref: main
    components: [heatpumpir]

climate:
  - platform: heatpumpir
    protocol: mitsubishi_pla
    horizontal_default: auto
    vertical_default: auto
    name: "AC"
    transmitter_id: ir_transmitter
    min_temperature: 16
    max_temperature: 31
```

## Dependencies

This component uses a forked version of the arduino-heatpumpir library:
https://github.com/troykelly/arduino-heatpumpir

## Credits

- Original HeatpumpIR library: [ToniA/arduino-heatpumpir](https://github.com/ToniA/arduino-heatpumpir)
- Original ESPHome component: [esphome/esphome](https://github.com/esphome/esphome)
- Protocol analysis and fix: IR captures from W001CP remote (R61Y23391)
