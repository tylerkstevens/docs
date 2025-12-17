<!--explain high level overview of building a raspberry pi based HA home brain-->
# Raspberry Pi + Home Assistant

Build a Home Assistant controller on Raspberry Pi - the same platform used in Exergy kits.

This guide is split into two parts:

1. **[Hardware Setup](./rpi-ha-hardware.md)** - Components you need and how to assemble them
2. **[System Configuration](./rpi-ha-config.md)** - Installing and configuring Home Assistant OS

## Quick Start

If you're ready to dive in:
- Already have hardware? Skip to [System Configuration](./rpi-ha-config.md)
- Starting from scratch? Begin with [Hardware Setup](./rpi-ha-hardware.md)

---

## Hardware Requirements

### Required

| Component | Recommendation | Notes |
|-----------|----------------|-------|
| Raspberry Pi | Pi 5 (4GB or 8GB) | Pi 4 also works |
| Power Supply | Official 27W USB-C | Adequate power critical |
| Storage | 64GB+ microSD or NVMe SSD | SSD recommended for reliability |
| Case | Any compatible | Argon One, Flirc, etc. |
| Ethernet | Cat5e cable | WiFi possible but not recommended |

### Optional (for Zigbee/Kit 2 equivalent)

| Component | Recommendation | Notes |
|-----------|----------------|-------|
| Zigbee Coordinator | Sonoff ZBDongle-E | USB dongle style |
| Temperature Sensor | Sonoff SNZB-02 or Aqara | Zigbee sensor |

## Installation Steps

### Step 1: Flash Home Assistant OS

1. Download [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
2. Insert microSD card (or NVMe via adapter)
3. In Imager, select:
   - Device: Your Raspberry Pi model
   - OS: Other specific-purpose OS → Home assistants → Home Assistant OS
   - Storage: Your SD card
4. Click Write and wait for completion

### Step 2: First Boot

1. Insert storage into Raspberry Pi
2. Connect ethernet cable to router
3. Connect power
4. Wait 5-10 minutes for initial setup

### Step 3: Access Home Assistant

1. Open browser to: `http://homeassistant.local:8123`
2. If that doesn't work, check your router for the Pi's IP address
3. Complete the onboarding wizard:
   - Create your user account
   - Set your location (for weather/sun automations)
   - Choose what to share with HA analytics

### Step 4: Install HACS

HACS (Home Assistant Community Store) is required for Exergy integrations:

1. In Home Assistant, go to **Settings → Add-ons → Add-on Store**
2. Search for "Terminal & SSH" and install it
3. Start the add-on and open the terminal
4. Run the HACS installation command from [hacs.xyz](https://hacs.xyz/docs/setup/download)
5. Restart Home Assistant
6. Go to **Settings → Devices & Services → Add Integration**
7. Search for "HACS" and complete setup

### Step 5: Install Exergy Canaan Integration

1. In HACS, go to **Integrations**
2. Click **+ Explore & Download Repositories**
3. Search for "Exergy Canaan"
4. Download and install
5. Restart Home Assistant
6. Go to **Settings → Devices & Services → Add Integration**
7. Search for "Exergy Canaan" and configure

See [Exergy Canaan Integration](../integrations/exergy-canaan.md) for detailed configuration.

### Step 6: (Optional) Set Up Zigbee

If using a Zigbee coordinator for temperature sensing:

1. Plug in USB Zigbee coordinator
2. Go to **Settings → Devices & Services → Add Integration**
3. Search for "ZHA" (Zigbee Home Automation)
4. Follow prompts to configure the coordinator
5. Pair sensors by putting them in pairing mode

## Storage Recommendations

### microSD Card

- Works, but SD cards can fail over time
- Use high-endurance cards (Samsung Pro Endurance, SanDisk Max Endurance)
- Keep backups of your configuration

### NVMe SSD (Recommended)

- More reliable than SD cards
- Faster performance
- Requires NVMe hat or case with M.2 slot
- Argon One V3 M.2 case is popular choice

## Backup Your Configuration

Regular backups are critical:

1. **Settings → System → Backups**
2. **Create Backup**
3. Download and store somewhere safe
4. Consider automated backup add-ons (Google Drive, etc.)

## Next Steps

- [Import Automation Blueprints](../blueprints/overview.md)
- [Set Up Dashboards](../dashboards/overview.md)
- [Configure Your Miner](../integrations/exergy-canaan.md)

## Troubleshooting

### Can't access homeassistant.local

- Try the IP address directly (check router admin panel)
- Ensure Pi has completed initial boot (wait 10+ minutes)
- Verify ethernet connection

### HACS installation fails

- Ensure you're using Terminal & SSH add-on (not basic SSH)
- Check internet connectivity
- Review HACS documentation at hacs.xyz

### Zigbee devices won't pair

- Move coordinator and sensor closer together for pairing
- Put sensor in pairing mode (usually hold button 5+ seconds)
- Check ZHA logs for errors
