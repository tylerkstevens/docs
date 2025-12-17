# Canaan Avalon Mini 3 in Home Assistant

The Avalon Mini 3 is a compact bitcoin miner designed for home heating applications.

## Miner Specifications

| Spec | Value |
|------|-------|
| Hashrate (Super) | ~37 TH/s |
| Hashrate (Eco) | ~28 TH/s |
| Power (Super) | ~850W |
| Power (Eco) | ~450W |
| Heat Output (Super) | ~2,900 BTU/hr |
| Heat Output (Eco) | ~1,536 BTU/hr |
| Noise Level | ~50 dB (Eco mode) |
| Dimensions | 300 x 140 x 195mm |
| Weight | ~5.5 kg |

## Avalon Mini 3 Work Modes

The Mini 3 supports multiple operating modes via the Exergy integration:

### Heating Mode
- Optimized for heat output
- Full fan speed for maximum air circulation
- Consistent hashrate
- Turns off at the temperature limit set in the Avalon Home App

### Mining Mode
- Optimized for hashrate/efficiency
- Standard operation
- Operates independent of temperature limit

### Night Mode
- Reduced noise operation
- Lower fan speeds
- Reduced hashrate and heat output
- Turns off miner display screen

## Avalon Mini 3 Work Levels

### Eco
- Reduced power consumption (~450W)
- Lower heat output
- Quieter operation
- Lower hashrate

### Super
- Maximum performance
- Full power consumption (~850W)
- Maximum heat output
- Highest hashrate

## Available Sensors

When connected via the Exergy Canaan integration, these sensors are available:

| Sensor | Entity Example | Description |
|--------|----------------|-------------|
| Ambient Temperature | `sensor.avalon_mini_3_ambient_temperature` | Intake air temp |
| Output Temperature | `sensor.avalon_mini_3_output_temperature` | Exhaust air temp |
| Hashboard Temperature | `sensor.avalon_mini_3_hash_board_temperature` | Internal chip temp |
| Hashrate | `sensor.avalon_mini_3_hashrate` | Current TH/s |
| Power | `sensor.avalon_mini_3_power` | Current wattage |
| Fan Speed | `sensor.avalon_mini_3_fan_speed` | Fan RPM % |
| Device State | `sensor.avalon_mini_3_state` | Operating status (Idle/Initializing/Working/Fault) |
| Work Level | `sensor.avalon_mini_3_work_level` | Current Operating Level (Super/Eco) |
| Work Mode | `sensor.avalon_mini_3_work_mode` | Current Operating Mode (Mining/Heating/Night) |

## Available Controls

| Control | Entity Example | Options |
|---------|----------------|---------|
| Power | `switch.avalon_mini_3_power` | On/Off |
| Work Mode | `select.avalon_mini_3_work_mode` | Heating, Mining, Night |
| Work Level | `select.avalon_mini_3_work_level` | Eco, Super |
| Update | `button.avalon_mini_3_update` | Trigger Manual Sensor Update |
| Reboot | `button.avalon_mini_3_reboot` | Trigger reboot |

## Heating Capacity

The Mini 3 produces approximately **2,900 BTU/hr** at full power, comparable to a medium-sized space heater.

**Suitable for:**
- Single room heating (200-400 sq ft)
- Supplemental heating in larger spaces
- Home office or bedroom

**Not suitable for:**
- Whole-home heating (single unit)
- Spaces requiring silent operation

## Network Setup

The Mini 3 connects to your network via WiFi:

1. Insert USB WiFi adapter and power on the miner
2. Use the Avalon Home app for initial miner set up
3. Find the miner IP address via the Avalon Home app or router admin
4. Add to Home Assistant via Exergy Canaan integration

## Tips for Best Performance

### Airflow
- Keep intake and exhaust areas clear
- Point exhaust into the room you want to heat
- Don't set items on miner as it gets hot

### Electrical
- Dedicated 15A circuit recommended
- Avoid extension cords if possible
- Use surge protector

### Network
- Static IP or DHCP reservation helps reliability

## Resources

- [Canaan Official Site](https://www.canaan.io/)
- [Avalon Home App](https://www.canaan.io/avalon-home)
- [Exergy Canaan Integration](./exergy-canaan.md)
