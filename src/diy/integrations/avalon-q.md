# Canaan Avalon Q in Home Assistant

The Avalon Q is a higher-performance bitcoin miner suitable for larger heating applications.

## Specifications

| Spec | Value |
|------|-------|
| Hashrate | ~90 TH/s (varies by mode) |
| Power | ~2,800W |
| Heat Output | ~9,500 BTU/hr |
| Noise Level | ~65 dB |
| Dimensions | 400 x 200 x 290mm |
| Weight | ~12 kg |

## Work Modes

The Avalon Q supports multiple operating modes via the Exergy integration:

### Heating Mode
- Optimized for heat output
- Full fan speed for maximum air circulation
- Consistent hashrate

### Mining Mode
- Optimized for hashrate/efficiency
- Standard operation

### Night Mode
- Reduced noise operation
- Lower fan speeds
- Reduced hashrate and heat output

## Work Levels

### Eco
- Reduced power consumption (~2,000W)
- Lower heat output
- Quieter operation
- Lower hashrate

### Super
- Maximum performance
- Full power consumption
- Maximum heat output
- Highest hashrate

## Available Sensors

When connected via the Exergy Canaan integration:

| Sensor | Entity Example | Description |
|--------|----------------|-------------|
| Ambient Temperature | `sensor.avalon_q_temperature_ambient` | Intake air temp |
| Output Temperature | `sensor.avalon_q_temperature_output` | Exhaust air temp |
| Hashboard Temperature | `sensor.avalon_q_temperature_hashboard` | Internal chip temp |
| Hashrate | `sensor.avalon_q_hashrate` | Current TH/s |
| Power | `sensor.avalon_q_power` | Current wattage |
| Fan Speed | `sensor.avalon_q_fan_speed` | Fan RPM % |
| Device State | `sensor.avalon_q_state` | Operating status |

## Available Controls

| Control | Entity Example | Options |
|---------|----------------|---------|
| Power | `switch.avalon_q_power` | On/Off |
| Work Mode | `select.avalon_q_work_mode` | Heating, Mining, Night |
| Work Level | `select.avalon_q_work_level` | Eco, Super |
| Reboot | `button.avalon_q_reboot` | Trigger reboot |

## Heating Capacity

The Avalon Q produces approximately **9,500 BTU/hr** at full power, comparable to a large space heater or small HVAC system.

**Suitable for:**
- Large room heating (400-800 sq ft)
- Basement or garage heating
- HVAC duct integration

**Considerations:**
- Requires 30A circuit (240V recommended)
- Higher noise level
- More significant heat output

## HVAC Integration

The Avalon Q is well-suited for integration with existing HVAC systems:

- Output can be ducted into supply plenum
- Acts as "Stage 1" heating with fossil fuel as "Stage 2"
- Requires proper airflow management

See [HVAC Integrated Thermostat Control](../blueprints/hvac.md) for automation setup.

## Electrical Requirements

**Important:** The Avalon Q has higher power requirements:

- 240V recommended (can run 120V at reduced power)
- 30A circuit minimum
- Dedicated circuit required
- Professional installation recommended

## Network Setup

1. Connect ethernet cable from miner to router
2. Power on the miner
3. Use the Avalon Home app or router admin to find the IP address
4. Add to Home Assistant via Exergy Canaan integration

## Resources

- [Canaan Official Site](https://www.canaan.io/)
- [Avalon Home App](https://www.canaan.io/avalon-home)
- [Exergy Canaan Integration](./exergy-canaan.md)
