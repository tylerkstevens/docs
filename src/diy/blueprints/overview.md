# Exergy Home Assistant Automation Blueprints

Pre-made Home Assistant automations you can import and customize for hashrate heating.

## What Are Blueprints?

Blueprints are automation templates. Instead of building automations from scratch, you:

1. Import the blueprint
2. Fill in your specific entities
3. Customize settings
4. Activate

## Available Blueprints

*Blueprint library expanding - check GitHub for latest*

### Time-of-Use Optimization

Run miners during cheap electricity hours, reduce during peak rates.

**Inputs:**
- Miner entity
- Peak start/end times
- Off-peak behavior (full power, eco, off)
- Peak behavior (eco, off)

### Weather-Based Heating

Adjust mining based on outdoor temperature.

**Inputs:**
- Miner entity
- Weather/temperature entity
- Temperature thresholds
- Actions at each threshold

### Room Thermostat Control

Maintain room temperature using a temperature sensor (Kit 2 style).

**Inputs:**
- Miner entity
- Temperature sensor entity
- Target temperature
- Hysteresis (temperature band)

### Scheduled Operation

Run on a weekly schedule with different modes for different times.

**Inputs:**
- Miner entity
- Schedule definition
- Mode for each time period

## GitHub Repository

All blueprints are available on GitHub:

**[github.com/exergyheat](https://github.com/exergyheat)**

## Installing Blueprints

### Method 1: Import URL

1. Go to **Settings → Automations & Scenes → Blueprints**
2. Click **Import Blueprint**
3. Paste the GitHub raw URL of the blueprint YAML
4. Click **Preview Blueprint**
5. Click **Import Blueprint**

### Method 2: Manual YAML

1. Download the blueprint YAML file
2. Place it in `/config/blueprints/automation/exergy/`
3. Restart Home Assistant
4. Blueprint appears in the list

## Creating Automations from Blueprints

1. Go to **Settings → Automations & Scenes**
2. Click **Create Automation**
3. Select **Use a Blueprint**
4. Choose the Exergy blueprint
5. Fill in your entity IDs and settings
6. Save

## Customizing Blueprints

Blueprints provide a starting point. After creating an automation:

- Edit conditions to add exceptions
- Add additional actions
- Modify triggers
- Combine with other automations

## Building Your Own

Don't see what you need? Build custom automations:

### Visual Editor

Home Assistant's automation editor is powerful:
- Triggers: When something happens
- Conditions: Only if criteria are met
- Actions: What to do

### YAML

For more control, write automations in YAML:

```yaml
automation:
  - alias: "Example automation"
    trigger:
      - platform: state
        entity_id: sensor.something
    condition:
      - condition: numeric_state
        entity_id: sensor.something_else
        above: 50
    action:
      - service: switch.turn_on
        target:
          entity_id: switch.miner
```

### Node-RED

For complex logic, consider Node-RED:
- Visual flow-based programming
- Powerful logic capabilities
- HA integration via Node-RED Companion

## Sharing Blueprints

Created a useful blueprint? Share it:

- **[Guides Forum](https://support.exergyheat.com/c/guides/6)** - Post for community
- **[GitHub](https://github.com/exergyheat)** - Submit PR for official inclusion
