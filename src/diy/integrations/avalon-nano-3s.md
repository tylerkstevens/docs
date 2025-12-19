<!--explain in detail how to interact with, interperet sensor data, send commands, and view information for an avalon nano3s in ha using our canaan integration-->
# Canaan Avalon Nano 3s in Home Assistant

The Avalon Nano 3s is a compact, low-power bitcoin miner designed for desktop or small space heating.

## Specifications

| Spec | Value |
|------|-------|
| Hashrate | ~6 TH/s (varies by mode) |
| Power | ~150W |
| Heat Output | ~500 BTU/hr |
| Noise Level | ~40 dB |
| Dimensions | 150 x 100 x 100mm |
| Weight | ~1 kg |

## Work Modes

The Nano 3s supports operating modes via the Exergy integration:

### High Mode
- Optimized for consistent heat output
- Standard fan operation

### Mid Mode
- Optimized for hashrate/efficiency
- Standard operation

### Low Mode
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
| Work Mode | `select.avalon_nano_3s_work_mode` | High, Medium, Low |
| Light Control | `light.avalon_nano_3s_led` | LED Light Color Selection |
| Light Effects | `light.avalon_nano_3s_led_effect` | LED Light Effect Selection (Off, On, Flash, Breath, Loop) |
| Reboot | `button.avalon_nano_3s_reboot` | Trigger reboot |

Unfortunantely, the Nano 3s API doesn't support basic power controls. We suggest pairing this with a smart outlet (WiFi, Zigbee, etc.) to completely turn it on and off.

![Avalon Mini 3s Dashboard](../../assets/exergy-canaan-integration/avalon-nano3s-dashboard.png)
![Nano 3s Light Control](../../assets/exergy-canaan-integration/nano-3s-light-control.png)

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

1. Insert WiFi USB adapter
2. Power on the Nano 3s
3. Use the Avalon Home app to configure WiFi
4. Find IP address in app or router admin
5. Add to Home Assistant via Exergy Canaan integration

## Resources

- [Canaan Official Site](https://www.canaan.io/)
- [Avalon Home App](https://www.canaan.io/avalon-home)
- [Exergy Canaan Integration](./exergy-canaan.md)
