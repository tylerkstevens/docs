# Space Heater Thermostat Control - Exergy HA Blueprint

Control your bitcoin miner like a traditional space heater with thermostatic temperature control.

## How It Works

This automation turns your miner on and off based on room temperature:

1. Temperature drops below target → Miner turns ON
2. Temperature rises above target → Miner turns OFF
3. Repeat to maintain desired temperature

Just like a space heater with a thermostat, but earning bitcoin while heating.

## Prerequisites

- Miner connected via Exergy Canaan integration
- Temperature sensor in the room (Zigbee, WiFi, or any HA-compatible sensor)
- Both devices configured in Home Assistant

## Blueprint Installation

### Method 1: Import from GitHub

1. Go to **Settings → Automations & Scenes → Blueprints**
2. Click **Import Blueprint**
3. Paste the URL:
   ```
   https://github.com/exergyheat/ha-blueprints/blob/main/space-heater-thermostat.yaml
   ```
4. Click **Preview Blueprint**
5. Click **Import Blueprint**

### Method 2: Manual YAML

1. Download the blueprint from [GitHub](https://github.com/exergyheat)
2. Place in `/config/blueprints/automation/exergy/space-heater-thermostat.yaml`
3. Restart Home Assistant

## Configuration

When creating an automation from this blueprint:

### Required Inputs

| Input | Description |
|-------|-------------|
| Miner Entity | Your miner's power switch (e.g., `switch.avalon_mini_3_power`) |
| Temperature Sensor | Room temperature sensor (e.g., `sensor.living_room_temperature`) |
| Target Temperature | Desired room temperature |

### Optional Inputs

| Input | Default | Description |
|-------|---------|-------------|
| Hysteresis | 1.0°F | Temperature band to prevent rapid cycling |
| Minimum On Time | 5 min | Prevent short cycles |
| Minimum Off Time | 5 min | Allow miner to cool down |

## Understanding Hysteresis

Hysteresis prevents the miner from rapidly turning on and off:

**Example with 70°F target and 1°F hysteresis:**
- Miner turns ON when temp drops to 69°F
- Miner turns OFF when temp rises to 71°F
- 2°F total swing (target ± hysteresis)

Increase hysteresis for longer, less frequent cycles. Decrease for tighter temperature control.

## Example Configuration

```yaml
# Created from blueprint
automation:
  - alias: "Living Room Miner Thermostat"
    use_blueprint:
      path: exergy/space-heater-thermostat
      input:
        miner_switch: switch.avalon_mini_3_power
        temperature_sensor: sensor.living_room_temperature
        target_temp: 70
        hysteresis: 1.5
        min_on_time: 10
        min_off_time: 5
```

## Manual YAML Alternative

If you prefer to create the automation manually:

```yaml
automation:
  - alias: "Miner Heater On"
    trigger:
      - platform: numeric_state
        entity_id: sensor.living_room_temperature
        below: 69  # target - hysteresis
    condition:
      - condition: state
        entity_id: switch.avalon_mini_3_power
        state: "off"
    action:
      - service: switch.turn_on
        target:
          entity_id: switch.avalon_mini_3_power

  - alias: "Miner Heater Off"
    trigger:
      - platform: numeric_state
        entity_id: sensor.living_room_temperature
        above: 71  # target + hysteresis
    condition:
      - condition: state
        entity_id: switch.avalon_mini_3_power
        state: "on"
    action:
      - service: switch.turn_off
        target:
          entity_id: switch.avalon_mini_3_power
```

## Tips

### Sensor Placement

- Place temperature sensor at "living height" (3-5 feet)
- Keep away from direct miner exhaust
- Avoid windows, exterior walls, or direct sunlight

### Multiple Rooms

- Create separate automations for each room/miner pair
- Each automation tracks its own temperature sensor

### Work Mode Considerations

- **Heating Mode**: Full power, maximum heat output
- **Eco Mode**: Reduced power, may not reach target temperature
- **Night Mode**: Quieter but less heat

Consider automations that adjust work mode based on time of day.

## Troubleshooting

### Miner cycling too frequently

- Increase hysteresis value
- Increase minimum on/off times
- Check sensor placement (may be too close to miner)

### Room never reaches target temperature

- Miner may not have enough heat output for space
- Check for drafts or heat loss
- Consider running in higher power mode

### Temperature overshoots

- Miner continues heating during shutdown
- Increase hysteresis slightly
- Normal behavior - mining hardware retains heat

## Dashboard Integration

See [Space Heater Digital Thermostat](../dashboards/space-heater.md) for a matching dashboard to control this automation visually.
