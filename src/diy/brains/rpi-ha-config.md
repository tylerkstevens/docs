# Raspberry Pi Home Assistant System Configuration

Install Home Assistant OS and configure it for hashrate heating control.

## Prerequisites

- Assembled Raspberry Pi hardware ([Hardware Setup](./rpi-ha-hardware.md))
- Computer with SD card reader (for flashing)
- Router with available ethernet port

## Step 1: Flash Home Assistant OS

### Download Raspberry Pi Imager

1. Go to [raspberrypi.com/software](https://www.raspberrypi.com/software/)
2. Download and install Raspberry Pi Imager for your OS

### Flash the Image

1. Insert microSD card (or NVMe via USB adapter)
2. Open Raspberry Pi Imager
3. Click **Choose Device** → Select your Pi model
4. Click **Choose OS** → **Other specific-purpose OS** → **Home assistants** → **Home Assistant OS**
5. Select the correct variant for your Pi
6. Click **Choose Storage** → Select your SD/NVMe
7. Click **Next** → **No** (don't customize settings)
8. Click **Yes** to confirm write
9. Wait for write and verification to complete

## Step 2: First Boot

1. Insert storage into Raspberry Pi
2. Connect ethernet cable to router
3. Connect power supply
4. **Wait 10-20 minutes** for initial setup

The first boot takes longer as Home Assistant:
- Resizes partitions
- Downloads latest updates
- Initializes database

## Step 3: Access Home Assistant

### Find Home Assistant

Open a browser and try:

1. **http://homeassistant.local:8123** (works on most networks)
2. If that fails, check your router's admin panel for the Pi's IP address
3. Try **http://[IP_ADDRESS]:8123**

### Complete Onboarding

1. **Create Account** - This is your admin account
2. **Name Your Home** - And set your location
3. **Privacy Settings** - Choose what to share with HA analytics
4. **Discovered Devices** - Skip for now, we'll add miners separately

## Step 4: Install HACS

HACS (Home Assistant Community Store) is required for Exergy integrations.

### Enable Advanced Mode

1. Click your profile (bottom left)
2. Enable **Advanced Mode**

### Install Terminal Add-on

1. Go to **Settings** → **Add-ons**
2. Click **Add-on Store** (bottom right)
3. Search for **Terminal & SSH**
4. Click **Install**
5. After install, click **Start**
6. Enable **Show in sidebar**

### Install HACS

1. Click **Terminal** in sidebar
2. Paste and run:
   ```bash
   wget -O - https://get.hacs.xyz | bash -
   ```
3. Wait for completion
4. **Restart Home Assistant**: Settings → System → Restart

### Configure HACS

1. Go to **Settings** → **Devices & Services**
2. Click **+ Add Integration**
3. Search for **HACS**
4. Follow the GitHub authorization flow
5. Complete setup

## Step 5: (Optional) Set Up Zigbee

If using a Zigbee coordinator for temperature sensors:

### Add ZHA Integration

1. Plug in USB Zigbee coordinator
2. Go to **Settings** → **Devices & Services**
3. Click **+ Add Integration**
4. Search for **ZHA** (Zigbee Home Automation)
5. Select the correct serial port (usually `/dev/ttyUSB0` or `/dev/ttyACM0`)
6. Complete setup

### Pair Temperature Sensor

1. In ZHA, click **Add Device**
2. Put sensor in pairing mode:
   - **Sonoff SNZB-02**: Hold button 5+ seconds until LED blinks
   - **Aqara**: Hold button 5+ seconds until LED blinks
3. Wait for discovery
4. Name your sensor (e.g., "Living Room Temperature")

## Step 6: Backup Configuration

Set up regular backups before proceeding:

1. Go to **Settings** → **System** → **Backups**
2. Click **Create Backup**
3. Download the backup file
4. Store it safely (cloud storage, another computer, etc.)

Consider automating backups with the Google Drive Backup add-on.

## Troubleshooting

### Can't access homeassistant.local

- Wait longer (first boot can take 20+ minutes)
- Try the IP address directly (check router admin)
- Ensure ethernet cable is connected
- Try a different browser

### HACS installation fails

- Ensure you're using **Terminal & SSH** add-on (not basic SSH)
- Check internet connectivity
- Review [HACS documentation](https://hacs.xyz)

### Zigbee devices won't pair

- Move coordinator and sensor closer during pairing
- Use USB extension cable to reduce interference
- Check ZHA logs: Settings → System → Logs

## Next Steps

Your Home Assistant is ready. Continue with:

→ [Install Exergy Integrations](../integrations/overview.md) - Connect your bitcoin miners
