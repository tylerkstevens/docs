# Exergy Home Assistant Dashboard Templates

Pre-built Home Assistant dashboards for monitoring and controlling your hashrate heating system.

## Available Dashboards

*Dashboard templates expanding - check GitHub for latest*

### Single Miner Overview

Monitor one miner with all key metrics:
- Power status and controls
- Temperature readings (intake, exhaust, hashboard)
- Hashrate and power consumption
- Work mode and level controls

### Multi-Miner Fleet View

Monitor multiple miners at a glance:
- Status grid for all miners
- Total hashrate and power
- Alert indicators
- Quick controls

### Room Thermostat Interface

Kit 2 style thermostat control:
- Large temperature display
- Set point adjustment
- Current vs. target comparison
- Heating status indicator

### Energy Dashboard

Track mining economics:
- Power consumption over time
- Energy costs
- Mining revenue (if integrated)
- Net cost/savings

## Live Demo

See a fully configured system:

**[demo.exergyheat.com](https://demo.exergyheat.com)**

*Note: Demo is view-only to protect our office heating system.*

## GitHub Repository

All dashboard YAML configurations:

**[github.com/exergyheat](https://github.com/exergyheat)**

## Installing Dashboards

### Method 1: Copy YAML

1. Download dashboard YAML from GitHub
2. In Home Assistant, go to **Settings → Dashboards**
3. Create a new dashboard (or edit existing)
4. Click three dots → **Raw configuration editor**
5. Paste the YAML
6. Update entity IDs to match your system
7. Save

### Method 2: Card by Card

1. View the dashboard template as reference
2. In your dashboard, add cards one at a time
3. Configure each card with your entity IDs
4. Arrange as desired

## Customizing Dashboards

### Change Entity IDs

Templates use placeholder entity IDs. Replace with yours:

```yaml
# Template might have:
entity: switch.avalon_mini_3_power

# Change to your actual entity:
entity: switch.living_room_miner_power
```

### Adjust Layout

- Drag cards to rearrange
- Change card sizes in YAML
- Add/remove sections as needed

### Add Custom Cards

Popular additions:
- Mini-graph-card for history
- Mushroom cards for clean UI
- Button-card for custom controls
- Apex charts for advanced graphs

Install custom cards via HACS.

## Dashboard Cards Used

Our templates may use these card types:

### Built-in Cards

- **Entities** - List of entity states
- **Gauge** - Circular gauge display
- **Thermostat** - Climate control interface
- **Button** - Action buttons
- **Sensor** - Single sensor display
- **History graph** - Entity history

### Custom Cards (via HACS)

- **mini-graph-card** - Compact graphs
- **mushroom** - Modern card set
- **button-card** - Advanced button customization

Install these via HACS → Frontend before using templates that require them.

## Building Your Own

### Start Simple

Begin with basic cards showing your entities, then enhance:

1. Add an entities card with your miner sensors
2. Add gauge cards for temperatures
3. Add buttons for controls
4. Add graphs for history

### Design Principles

- **Glanceable** - Key info visible at a glance
- **Actionable** - Controls easily accessible
- **Informative** - Details available when needed
- **Responsive** - Works on phone and desktop

### Inspiration

- [Home Assistant Dashboard Gallery](https://www.home-assistant.io/dashboards/)
- [Reddit r/homeassistant](https://www.reddit.com/r/homeassistant/)
- [Exergy Demo](https://demo.exergyheat.com)

## Sharing Dashboards

Created a great dashboard? Share it:

- **[Guides Forum](https://support.exergyheat.com/c/guides/6)** - Screenshots and YAML
- **[GitHub](https://github.com/exergyheat)** - Submit PR for official templates
