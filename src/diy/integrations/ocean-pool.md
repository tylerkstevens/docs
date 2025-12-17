# Ocean Mining Pool - Exergy Home Assistant Integration

Monitor your Ocean mining pool earnings and statistics directly in Home Assistant.

## What is Ocean?

[Ocean](https://ocean.xyz) is a bitcoin mining pool focused on decentralization and transparency. Key features:

- **Non-custodial** - Payouts directly to your wallet
- **Transparent** - Block template selection visible
- **No KYC** - Privacy-respecting
- **TIDES payout** - Fair reward distribution

## Integration Features

The Exergy Ocean integration provides:

### Sensors

| Sensor | Description |
|--------|-------------|
| Hashrate (24h) | Your average hashrate over 24 hours |
| Estimated Daily Earnings | Projected daily sats based on current hashrate |
| Unpaid Balance | Current unpaid earnings |
| Last Payout | Amount and time of last payout |
| Pool Hashrate | Total Ocean pool hashrate |
| Pool Luck | Current pool luck percentage |

## Installation

### Prerequisites

- Home Assistant with HACS installed
- Ocean mining account with wallet address
- Your Ocean wallet address

### Step 1: Install via HACS

1. Open Home Assistant
2. Navigate to **HACS → Integrations**
3. Click **+ Explore & Download Repositories**
4. Search for "Exergy Ocean"
5. Click **Download**
6. Restart Home Assistant

### Step 2: Add Integration

1. Go to **Settings → Devices & Services**
2. Click **+ Add Integration**
3. Search for "Exergy Ocean"
4. Enter your Ocean wallet address
5. Click **Submit**

### Step 3: Verify

The integration creates sensors for your mining statistics. Check the device page to see all available entities.

## Dashboard Integration

Display your mining earnings alongside miner status:

```yaml
type: entities
title: Mining Stats
entities:
  - entity: sensor.ocean_hashrate_24h
    name: My Hashrate
  - entity: sensor.ocean_estimated_daily
    name: Est. Daily Sats
  - entity: sensor.ocean_unpaid_balance
    name: Unpaid Balance
```

## Automation Ideas

### Low Hashrate Alert

Notify when your pool hashrate drops (indicates miner issues):

```yaml
automation:
  - alias: "Low hashrate alert"
    trigger:
      - platform: numeric_state
        entity_id: sensor.ocean_hashrate_24h
        below: 30  # TH/s threshold
        for:
          hours: 2
    action:
      - service: notify.mobile_app
        data:
          message: "Mining hashrate dropped below threshold"
```

### Daily Earnings Summary

Send a daily summary of mining earnings:

```yaml
automation:
  - alias: "Daily mining summary"
    trigger:
      - platform: time
        at: "20:00:00"
    action:
      - service: notify.mobile_app
        data:
          message: >
            Today's mining: ~{{ states('sensor.ocean_estimated_daily') }} sats
            Unpaid: {{ states('sensor.ocean_unpaid_balance') }} sats
```

## Finding Your Ocean Wallet Address

Your Ocean wallet address is the bitcoin address you configured when setting up your miner to point to Ocean:

1. This is the address in your miner's pool configuration
2. It's also visible at `ocean.xyz/[your-address]`

## Multiple Miners, One Pool

If you have multiple miners pointing to the same Ocean wallet address, the integration shows combined statistics for all miners.

To track individual miner contributions:
- Use the Exergy Canaan integration for per-device hashrate
- Ocean integration shows pool-reported totals

## Troubleshooting

### No data appearing

1. Verify wallet address is correct
2. Ensure miners are actively mining to Ocean
3. Wait for data to populate (can take a few hours for new setups)
4. Check Ocean website directly to verify mining activity

### Hashrate discrepancy

- Pool-reported hashrate is averaged over time
- Local miner hashrate is real-time
- Some variation is normal
- Significant differences may indicate connectivity issues

## Resources

- [Ocean Pool](https://ocean.xyz)
- [Ocean Documentation](https://ocean.xyz/docs)
- [Exergy GitHub](https://github.com/exergyheat)
