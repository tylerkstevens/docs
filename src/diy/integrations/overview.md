# Exergy Home Assistant Integrations

Custom integrations for connecting mining hardware to Home Assistant.

## Available Integrations

| Integration | Purpose | Status |
|-------------|---------|--------|
| [Exergy Canaan](./exergy-canaan.md) | Control Canaan Avalon miners (Mini 3, Q, Nano 3s) | Available |
| [Ocean Mining Pool](./ocean-pool.md) | Monitor mining earnings and pool stats | Available |

## What Integrations Do

Home Assistant integrations connect external devices to HA, providing:

- **Entities** - Sensors, switches, and controls
- **Services** - Actions you can call
- **Events** - Triggers for automations

## Exergy Canaan Integration

Our primary integration for Canaan Avalon miners:

### Supported Models

- [Avalon Mini 3](./avalon-mini-3.md) - Compact home miner, ~37 TH/s, ~1,100W
- [Avalon Q](./avalon-q.md) - Higher performance, ~90 TH/s, ~2,800W
- [Avalon Nano 3s](./avalon-nano-3s.md) - Desktop miner, ~3 TH/s, ~150W

### Features

- Power on/off control
- Work mode selection (Heating, Mining, Night)
- Work level adjustment (Eco, Super)
- Temperature monitoring (ambient, output, hashboard)
- Hashrate and power consumption sensors
- Update and reboot controls

[Full Documentation →](./exergy-canaan.md)

## Ocean Mining Pool Integration

Monitor your mining earnings directly in Home Assistant:

- Pool hashrate and luck
- Estimated daily earnings
- Unpaid balance
- Payout history

[Full Documentation →](./ocean-pool.md)

## Installation (All Integrations)

All Exergy integrations are installed via HACS:

1. Ensure HACS is installed in Home Assistant
2. Go to HACS → Integrations
3. Search for the integration name
4. Download and install
5. Restart Home Assistant
6. Add the integration via Settings → Devices & Services

## Other Useful Integrations

These built-in or community integrations complement hashrate heating:

### ZHA (Zigbee Home Automation)

Built into Home Assistant. Used for:
- Zigbee temperature sensors
- Smart plugs
- Motion sensors
- etc.

[HA ZHA Documentation](https://www.home-assistant.io/integrations/zha/)

### Weather Integrations

For weather-based automations:
- OpenWeatherMap
- Met.no (default)
- National Weather Service

### Energy Monitoring

Track energy usage:
- Utility meter integration
- Energy dashboard
- Cost tracking

## Development & Contributing

All integrations are open source:

**[github.com/exergyheat](https://github.com/exergyheat)**

Contributions welcome:
- Bug reports
- Feature requests
- Code contributions
- Documentation improvements
