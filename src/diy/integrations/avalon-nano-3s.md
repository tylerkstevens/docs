# Canaan Avalon Nano 3s in Home Assistant

The Avalon Nano 3s is a compact, low-power bitcoin miner designed for desktop or small space heating.

## Specifications

| Spec | Value |
|------|-------|
| Hashrate | ~3 TH/s (varies by mode) |
| Power | ~150W |
| Heat Output | ~500 BTU/hr |
| Noise Level | ~40 dB |
| Dimensions | 150 x 100 x 100mm |
| Weight | ~1 kg |

## Work Modes

The Nano 3s supports operating modes via the Exergy integration:

### Heating Mode
- Optimized for consistent heat output
- Standard fan operation

### Mining Mode
- Optimized for hashrate/efficiency
- Standard operation

### Night Mode
- Reduced noise operation
- Lower fan speeds
- Reduced hashrate

## Available Sensors

When connected via the Exergy Canaan integration:

| Sensor | Entity Example | Description |
|--------|----------------|-------------|
| Temperature | `sensor.avalon_nano_3s_temperature` | Device temperature |
| Hashrate | `sensor.avalon_nano_3s_hashrate` | Current TH/s |
| Power | `sensor.avalon_nano_3s_power` | Current wattage |
| Device State | `sensor.avalon_nano_3s_state` | Operating status |

## Available Controls

| Control | Entity Example | Options |
|---------|----------------|---------|
| Power | `switch.avalon_nano_3s_power` | On/Off |
| Work Mode | `select.avalon_nano_3s_work_mode` | Heating, Mining, Night |
| Reboot | `button.avalon_nano_3s_reboot` | Trigger reboot |

## Heating Capacity

The Nano 3s produces approximately **500 BTU/hr**, similar to a small personal space heater.

**Suitable for:**
- Desktop/workspace warming
- Small enclosed spaces
- Supplemental heat source
- Learning/educational setups

**Not suitable for:**
- Room heating (too low output)
- Primary heating source

## Use Cases

### Personal Space Heater
- Place under desk or near workspace
- Low noise suitable for office environment
- Warms immediate area

### Entry-Level Mining
- Low power requirements (standard outlet)
- Quiet operation
- Learn bitcoin mining basics

### Multiple Unit Setups
- Combine several Nano units for distributed heating
- Each unit independently controlled

## Electrical Requirements

The Nano 3s has minimal power requirements:

- Standard 120V outlet
- ~1.5A draw
- No dedicated circuit needed
- Can share circuit with other devices

## Network Setup

The Nano 3s can connect via WiFi or ethernet:

### WiFi Setup
1. Power on the Nano 3s
2. Use the Avalon Home app to configure WiFi
3. Find IP address in app or router admin
4. Add to Home Assistant via Exergy Canaan integration

### Ethernet Setup
1. Connect ethernet cable from miner to router
2. Power on the miner
3. Find IP address in router admin
4. Add to Home Assistant

## Resources

- [Canaan Official Site](https://www.canaan.io/)
- [Avalon Home App](https://www.canaan.io/avalon-home)
- [Exergy Canaan Integration](./exergy-canaan.md)
