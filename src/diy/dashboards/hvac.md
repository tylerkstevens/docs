# HVAC Integrated Wall+Digital Thermostat - Exergy HA Dashboard

A dashboard for monitoring your hybrid heating system - combining wall thermostat control with miner status and bitcoin earnings.

## Overview

This dashboard provides:
- Traditional thermostat interface (matches your wall unit)
- Miner status and controls
- Stage 1 (miner) vs Stage 2 (furnace) indicators
- System efficiency and earnings tracking

## System Layout

```
┌─────────────────────────────────────────────────────┐
│  HVAC System Dashboard                              │
├─────────────────────┬───────────────────────────────┤
│                     │                               │
│   ┌───────────┐     │   Stage 1: Miner      ● ON   │
│   │           │     │   Stage 2: Furnace    ○ OFF  │
│   │   72°F    │     │                               │
│   │   ───     │     │   ┌───────────────────────┐  │
│   │   70°F    │     │   │ Miner Stats           │  │
│   │  target   │     │   │ Hashrate: 90 TH/s     │  │
│   │           │     │   │ Power: 2,800W         │  │
│   └───────────┘     │   │ Est. Daily: 12,500 sat│  │
│                     │   └───────────────────────┘  │
└─────────────────────┴───────────────────────────────┘
```

## Installation

### Method 1: Import Full Dashboard

1. Download YAML from [GitHub](https://github.com/exergyheat)
2. Go to **Settings → Dashboards → Add Dashboard**
3. Enter dashboard → Three dots → **Raw configuration editor**
4. Paste and update entity IDs
5. Save

### Method 2: Build Card by Card

Add each section to an existing dashboard.

## Dashboard YAML

### Complete Template

```yaml
title: HVAC System
views:
  - title: Climate
    path: climate
    cards:
      # Main Thermostat
      - type: thermostat
        entity: climate.home_thermostat
        name: Home

      # Heating Stage Status
      - type: entities
        title: Heating System
        entities:
          - entity: binary_sensor.hvac_stage_1
            name: "Stage 1: Miner"
            icon: mdi:bitcoin
          - entity: binary_sensor.hvac_stage_2
            name: "Stage 2: Furnace"
            icon: mdi:fire
          - entity: sensor.thermostat_hvac_action
            name: Current Action

      # Miner Status
      - type: entities
        title: Bitcoin Heater
        entities:
          - entity: switch.avalon_q_power
            name: Power
          - entity: select.avalon_q_work_mode
            name: Mode
          - entity: sensor.avalon_q_hashrate
            name: Hashrate
          - entity: sensor.avalon_q_power
            name: Power Draw
          - entity: sensor.avalon_q_temperature_output
            name: Exhaust Temp

      # System Temperatures
      - type: horizontal-stack
        cards:
          - type: gauge
            entity: sensor.thermostat_current_temperature
            name: Home
            min: 50
            max: 85
            needle: true
          - type: gauge
            entity: sensor.avalon_q_temperature_output
            name: Miner Output
            min: 50
            max: 150

      # Mining Economics
      - type: entities
        title: Mining Stats
        entities:
          - entity: sensor.ocean_hashrate_24h
            name: Pool Hashrate
          - entity: sensor.ocean_estimated_daily
            name: Est. Daily Sats
          - entity: sensor.ocean_unpaid_balance
            name: Unpaid Balance

      # Temperature History
      - type: history-graph
        title: Temperature History
        hours_to_show: 24
        entities:
          - entity: sensor.thermostat_current_temperature
            name: Home
          - entity: sensor.outdoor_temperature
            name: Outside
          - entity: sensor.avalon_q_temperature_output
            name: Miner
```

## Creating Stage Sensors

If your thermostat doesn't expose stage sensors, create template sensors:

```yaml
# configuration.yaml
template:
  - binary_sensor:
      - name: "HVAC Stage 1"
        state: >
          {{ is_state('switch.avalon_q_power', 'on') }}
        icon: mdi:bitcoin

      - name: "HVAC Stage 2"
        state: >
          {{ is_state_attr('climate.home_thermostat', 'hvac_action', 'heating')
             and state_attr('climate.home_thermostat', 'stage') == 2 }}
        icon: mdi:fire
```

## Individual Card Examples

### Dual Stage Indicator

Visual indicator for which heating stage is active:

```yaml
type: horizontal-stack
cards:
  - type: custom:button-card
    entity: switch.avalon_q_power
    name: Stage 1
    icon: mdi:bitcoin
    show_state: false
    styles:
      card:
        - background-color: |
            [[[
              return entity.state === 'on'
                ? 'var(--success-color)'
                : 'var(--card-background-color)'
            ]]]
      icon:
        - color: |
            [[[
              return entity.state === 'on'
                ? 'white'
                : 'var(--primary-text-color)'
            ]]]

  - type: custom:button-card
    entity: binary_sensor.furnace_running
    name: Stage 2
    icon: mdi:fire
    show_state: false
    styles:
      card:
        - background-color: |
            [[[
              return entity.state === 'on'
                ? 'var(--warning-color)'
                : 'var(--card-background-color)'
            ]]]
```

### Energy Comparison Card

Show miner vs furnace usage:

```yaml
type: entities
title: Energy Today
entities:
  - entity: sensor.miner_energy_today
    name: Miner (kWh)
    icon: mdi:flash
  - entity: sensor.furnace_runtime_today
    name: Furnace Runtime
    icon: mdi:clock
  - entity: sensor.bitcoin_earned_today
    name: Bitcoin Earned
    icon: mdi:bitcoin
```

### Efficiency Dashboard

Track system efficiency over time:

```yaml
type: custom:mini-graph-card
name: Heating Efficiency
entities:
  - entity: sensor.miner_runtime_percent
    name: Miner %
    color: '#f7931a'
  - entity: sensor.furnace_runtime_percent
    name: Furnace %
    color: '#e74c3c'
hours_to_show: 168
group_by: date
show:
  graph: bar
```

## Thermostat Card Options

### Standard Thermostat

```yaml
type: thermostat
entity: climate.home_thermostat
features:
  - type: climate-hvac-modes
    hvac_modes:
      - "off"
      - heat
      - cool
      - auto
```

### Custom Thermostat Look

Using mushroom cards:

```yaml
type: custom:mushroom-climate-card
entity: climate.home_thermostat
show_temperature_control: true
hvac_modes:
  - heat
  - cool
  - "off"
```

## Mobile View

Optimized for phone access:

```yaml
views:
  - title: Mobile
    path: mobile
    cards:
      - type: vertical-stack
        cards:
          - type: thermostat
            entity: climate.home_thermostat

          - type: glance
            entities:
              - entity: switch.avalon_q_power
                name: Miner
              - entity: binary_sensor.furnace_running
                name: Furnace
              - entity: sensor.ocean_estimated_daily
                name: Sats/Day

          - type: button
            entity: switch.avalon_q_power
            name: Miner Power
            tap_action:
              action: toggle
            show_state: true
```

## Entity ID Reference

Update these placeholders with your actual entities:

| Placeholder | Description |
|-------------|-------------|
| `climate.home_thermostat` | Your smart thermostat |
| `switch.avalon_q_power` | Miner power control |
| `sensor.avalon_q_*` | Miner sensors |
| `sensor.ocean_*` | Ocean pool sensors |
| `binary_sensor.furnace_running` | Furnace status (may need template) |
| `sensor.outdoor_temperature` | Weather integration temp |

## Troubleshooting

### Thermostat card not working

- Verify climate entity exists
- Check thermostat integration is connected
- Some thermostats need specific card types

### Stage indicators incorrect

- Create template sensors if not available natively
- Verify automation is controlling miner properly
- Check thermostat is reporting stage correctly

### Missing outdoor temperature

- Add a weather integration (Met.no, OpenWeatherMap)
- Use `sensor.weather_temperature` or similar

## Resources

- [Home Assistant Climate Docs](https://www.home-assistant.io/integrations/climate/)
- [Thermostat Card](https://www.home-assistant.io/dashboards/thermostat/)
- [Exergy GitHub - Dashboards](https://github.com/exergyheat)
