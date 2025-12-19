<!--explain in detail how to interact with, interperet sensor data, send commands, and view information for an avalon mini Q in ha using our canaan integration-->
# Canaan Avalon Q in Home Assistant

The Avalon Q is a higher-performance bitcoin miner suitable for larger heating applications.

## Specifications

| Spec | Value |
|------|-------|
| Hashrate | ~90 TH/s (varies by mode) |
| Power | ~1,650W |
| Heat Output | ~5,630 BTU/hr |
| Noise Level | ~65 dB |
| Dimensions | 400 x 200 x 290mm |
| Weight | ~12 kg |

## Work Levels

The Avalon Q supports multiple operating levels via the Exergy integration:

### Super Level
- ~1,700W
- Optimized for heat output
- Full power consumption
- Maximum performance
- Maximum heat output
- Full fan speed for maximum air circulation
- Highest hashrate

### Standard Level
- ~1,300W
- Optimized for hashrate/efficiency
- Standard operation
- Slightly reduced fan speed and heat output
- Medium level hashrate

### Eco Level
- ~800W
- Reduced noise operation
- Lower fan speeds
- Reduced hashrate and heat output

## Available Sensors

When connected via the Exergy Canaan integration:

| Sensor | Entity Example | Description |
|--------|----------------|-------------|
| Ambient Temperature | `sensor.avalon_q_ambient_temperature` | Intake air temp |
| Output Temperature | `sensor.avalon_q_output_temperature` | Exhaust air temp |
| Hashboard Temperature | `sensor.avalon_q_hash_board_temperature` | Internal chip temp |
| Hashrate | `sensor.avalon_q_hashrate` | Current TH/s |
| Power | `sensor.avalon_q_power` | Current wattage |
| Fan Speed | `sensor.avalon_q_fan_speed` | Fan RPM % |
| Device State | `sensor.avalon_q_state` | Operating status |

## Available Controls

| Control | Entity Example | Options |
|---------|----------------|---------|
| Power | `switch.avalon_q_power` | On/Off |
| Work Level | `select.avalon_q_work_level` | Eco, Standard, Super |
| Reboot | `button.avalon_q_reboot` | Trigger reboot |

![Avalon Q Sensor Dashboard](../../assets/exergy-canaan-integration/avalon-q-dashboard.png)

## Heating Capacity

The Avalon Q produces approximately **5,630 BTU/hr** at full power, comparable to a large space heater or small HVAC system.

**Suitable for:**
- Large room heating (400-800 sq ft)
- Basement or garage heating
- HVAC duct integration

**Considerations:**
- Requires 15A circuit
- Slightly higher noise level
- More significant heat output
- Dedicated circuit recommended


## HVAC Integration

The Avalon Q is well-suited for integration with existing HVAC systems:

- Output can be ducted into supply plenum
- Acts as "Stage 1" heating with fossil fuel as "Stage 2"
- Requires proper airflow management

See [HVAC Integrated Thermostat Control](../blueprints/hvac.md) for automation setup.

## Network Setup

1. Connect ethernet cable from miner to router or use USB WiFi adapter.
2. Power on the miner
3. Use the Avalon Home app or router admin to find the IP address
4. Add to Home Assistant via Exergy Canaan integration

## Resources

- [Canaan Official Site](https://www.canaan.io/)
- [Avalon Home App](https://www.canaan.io/avalon-home)
- [Exergy Canaan Integration](./exergy-canaan.md)
