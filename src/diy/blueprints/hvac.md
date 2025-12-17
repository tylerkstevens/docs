# HVAC Integrated Thermostat Control - Exergy HA Blueprint

Integrate your bitcoin miner into your home's HVAC system as "Stage 1" heating, with your existing furnace as backup.

## How It Works

This setup uses your miner as the primary heat source:

1. **Stage 1 (Miner)**: When heating is needed, miner turns on first
2. **Stage 2 (Furnace)**: If miner can't keep up, furnace activates
3. **Miner produces bitcoin** while providing base heating
4. **Furnace only runs** when additional heat is needed

## Prerequisites

### Hardware

- Bitcoin miner (Avalon Q recommended for HVAC integration)
- Miner output ducted to HVAC supply plenum
- Multi-stage thermostat connected to Home Assistant
- HVAC system with accessible stage wiring

### Home Assistant

- Miner connected via Exergy Canaan integration
- Thermostat connected (Z-Wave, Zigbee, or WiFi)
- Thermostat reports current stage

### Electrical Work

**Professional installation recommended** for:
- Ducting miner into HVAC system
- Rewiring thermostat to separate Stage 1 from Stage 2
- Ensuring proper airflow and safety

## System Architecture

```
                    ┌─────────────────┐
                    │   Thermostat    │
                    │  (Smart/Multi)  │
                    └────────┬────────┘
                             │
         ┌───────────────────┼───────────────────┐
         │                   │                   │
         ▼                   ▼                   ▼
  ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
  │  Stage 1     │   │  Stage 2     │   │  Cooling     │
  │  (Miner)     │   │  (Furnace)   │   │  (AC)        │
  │  via HA      │   │  Direct wire │   │  Direct wire │
  └──────────────┘   └──────────────┘   └──────────────┘
```

## Blueprint Installation

### Method 1: Import from GitHub

1. Go to **Settings → Automations & Scenes → Blueprints**
2. Click **Import Blueprint**
3. Paste the URL:
   ```
   https://github.com/exergyheat/ha-blueprints/blob/main/hvac-integrated-thermostat.yaml
   ```
4. Click **Preview Blueprint**
5. Click **Import Blueprint**

### Method 2: Manual YAML

1. Download from [GitHub](https://github.com/exergyheat)
2. Place in `/config/blueprints/automation/exergy/hvac-integrated-thermostat.yaml`
3. Restart Home Assistant

## Configuration

### Required Inputs

| Input | Description |
|-------|-------------|
| Miner Entity | Your miner's power switch |
| Thermostat Entity | Your HVAC thermostat |
| Stage Sensor | Entity that reports which heating stage is active |

### Optional Inputs

| Input | Default | Description |
|-------|---------|-------------|
| Stage 1 Delay | 30 sec | Wait time before turning on miner after Stage 1 call |
| Shutdown Delay | 60 sec | Wait time before turning off miner after call ends |

## Wiring Considerations

### Traditional Thermostat Wiring

Standard HVAC wiring:
- **W1**: Stage 1 heat (becomes miner via HA)
- **W2**: Stage 2 heat (remains wired to furnace)
- **Y**: Cooling
- **G**: Fan
- **C**: Common (power)

### Modification Approach

1. Disconnect W1 from furnace control board
2. W1 now only signals Home Assistant (via smart thermostat)
3. W2 remains connected to furnace
4. HA controls miner based on W1 signal

**Consult an HVAC professional for your specific system.**

## Example Configuration

```yaml
automation:
  - alias: "HVAC Stage 1 - Miner On"
    trigger:
      - platform: state
        entity_id: climate.home_thermostat
        attribute: hvac_action
        to: "heating"
    condition:
      - condition: numeric_state
        entity_id: sensor.thermostat_heating_stage
        below: 2  # Only Stage 1
    action:
      - delay: "00:00:30"  # Delay to confirm call
      - service: switch.turn_on
        target:
          entity_id: switch.avalon_q_power

  - alias: "HVAC Stage 1 - Miner Off"
    trigger:
      - platform: state
        entity_id: climate.home_thermostat
        attribute: hvac_action
        from: "heating"
    action:
      - delay: "00:01:00"  # Delay before shutdown
      - service: switch.turn_off
        target:
          entity_id: switch.avalon_q_power
```

## Airflow Requirements

### Duct Sizing

- Match miner CFM output to duct capacity
- Avalon Q: ~200 CFM typical
- Ensure no backpressure on miner fans

### Plenum Connection

- Connect to supply plenum (after furnace heat exchanger)
- Use insulated flex duct
- Include damper for isolation when miner is off

### Safety Considerations

- Install high-limit safety switch
- Ensure proper condensate drainage
- CO detector near furnace (as always)

## Performance Expectations

### Typical Savings

With an Avalon Q (~9,500 BTU/hr):
- Covers ~30-50% of heating needs in moderate climates
- Furnace runs significantly less
- Bitcoin earnings offset electricity costs

### Best Results

- Well-insulated homes
- Moderate heating climates
- Time-of-use electricity rates (mine during cheap hours)

## Troubleshooting

### Miner not turning on with Stage 1

- Verify thermostat is reporting stage to HA
- Check automation triggers are correct
- Confirm miner is available in HA

### Furnace activating too often

- Miner may not provide enough heat
- Increase target temperature differential
- Consider additional miner or higher power mode

### Short cycling

- Add delays to automations
- Increase thermostat hysteresis
- Check airflow through miner

## Dashboard Integration

See [HVAC Integrated Wall+Digital Thermostat](../dashboards/hvac.md) for a matching dashboard to monitor this setup.
