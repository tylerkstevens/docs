# Canaan Avalon Home - Exergy Home Assistant Integration

Full control of Canaan Avalon miners through Home Assistant.

## Supported Hardware

- [Canaan Avalon Mini 3](./avalon-mini-3.md) - Compact home miner, ~37 TH/s
- [Canaan Avalon Q](./avalon-q.md) - Higher performance, ~90 TH/s
- [Canaan Avalon Nano 3s](./avalon-nano-3s.md) - Desktop miner, ~6 TH/s

Click each model for detailed specifications, sensors, and controls.

## Features

### Controls

| Entity Type | Function |
|-------------|----------|
| Switch | Power on/off |
| Select | Work mode (Heating, Mining, Night) |
| Select | Work level (Eco, Super) |
| Button | Reboot device |
| Button | Check for updates |

### Sensors

| Sensor | Description |
|--------|-------------|
| Temperature (Ambient) | Intake air temperature |
| Temperature (Output) | Exhaust air temperature |
| Temperature (Hashboard) | Internal chip temperature |
| Hashrate | Current mining hashrate |
| Power | Current power consumption |
| Fan Speed | Fan RPM percentage |
| Device State | Operating status |

## Installation

### Prerequisites

- Home Assistant with HACS installed
- Miner on same network as Home Assistant
- Miner's IP address

### Step 1: Install via HACS

1. Open Home Assistant
2. Navigate to **HACS → Integrations**
3. Click **+ Explore & Download Repositories**
4. Search for "Exergy Canaan"
5. Click **Download**
6. Restart Home Assistant

### Step 2: Add Integration

1. Go to **Settings → Devices & Services**
2. Click **+ Add Integration**
3. Search for "Exergy Canaan"
4. Enter your miner's IP address
5. Click **Submit**

### Step 3: Verify

The integration should create:
- 1 Device (your miner)
- Multiple entities (controls and sensors)

Check the device page to see all available entities.

## Finding Your Miner's IP Address

### Method 1: Router Admin Panel

1. Log into your router's admin interface
2. Look for connected devices or DHCP leases
3. Find "Avalon" or similar device name
4. Note the IP address

### Method 2: Avalon Home App

1. Open the Avalon Home app
2. Connect to your miner
3. Look in device settings for IP address

### Method 3: Network Scanner

Use a network scanning app:
- Fing (iOS/Android)
- Advanced IP Scanner (Windows)
- nmap (Linux/Mac)

Scan your local network for the miner.

## Configuration Options

### Scan Interval

The integration polls the miner periodically. Default is 30 seconds.

To adjust (in configuration.yaml):

```yaml
# This may vary - check integration documentation
```

### Multiple Miners

Add each miner separately through the integration setup. Each will appear as a separate device.

## Entity Naming

Entities follow the pattern:

- `switch.avalon_mini_3_power`
- `select.avalon_mini_3_work_mode`
- `sensor.avalon_mini_3_hashrate`

If you have multiple miners, names will include identifiers.

## Example Automations

### Turn On When Temperature Drops

```yaml
automation:
  - alias: "Heat when cold"
    trigger:
      - platform: numeric_state
        entity_id: sensor.outdoor_temperature
        below: 50
    action:
      - service: switch.turn_on
        target:
          entity_id: switch.avalon_mini_3_power
```

### Night Mode at Bedtime

```yaml
automation:
  - alias: "Night mode at 10pm"
    trigger:
      - platform: time
        at: "22:00:00"
    action:
      - service: select.select_option
        target:
          entity_id: select.avalon_mini_3_work_mode
        data:
          option: "Night"
```

### Eco Mode During Peak Rates

```yaml
automation:
  - alias: "Eco during peak hours"
    trigger:
      - platform: time
        at: "16:00:00"  # Peak pricing starts
    action:
      - service: select.select_option
        target:
          entity_id: select.avalon_mini_3_work_level
        data:
          option: "Eco"
```

## Troubleshooting

### Integration not finding miner

1. Verify miner is powered on and connected to network
2. Confirm IP address is correct
3. Try accessing miner's web interface directly
4. Check that HA and miner are on same network/VLAN

### Entities unavailable

1. Check miner is online (ping IP address)
2. Restart the integration
3. Check Home Assistant logs for errors

### Slow response

- Normal polling interval is 30 seconds
- Commands should execute within a few seconds
- If persistently slow, check network connectivity

## Source Code

Open source on GitHub:

**[github.com/exergyheat](https://github.com/exergyheat)**

## Support

- **[Software Support Forum](https://support.exergyheat.com/c/sw-support/14)**
- **[GitHub Issues](https://github.com/exergyheat)**
