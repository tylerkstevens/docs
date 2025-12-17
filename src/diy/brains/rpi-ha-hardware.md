# Raspberry Pi Home Assistant Hardware Setup

Everything you need to build a Raspberry Pi-based Home Assistant controller.

## Required Components

| Component | Recommendation | Notes |
|-----------|----------------|-------|
| Raspberry Pi | Pi 5 (4GB or 8GB) | Pi 4 also works |
| Power Supply | Official 27W USB-C | Adequate power is critical |
| Storage | 64GB+ microSD or NVMe SSD | SSD recommended for reliability |
| Case | Any compatible | Argon One, Flirc, etc. |
| Ethernet Cable | Cat5e or better | WiFi possible but not recommended |

## Optional Components

For temperature-based automation (thermostat control):

| Component | Recommendation | Notes |
|-----------|----------------|-------|
| Zigbee Coordinator | Sonoff ZBDongle-E | USB dongle style |
| Temperature Sensor | Sonoff SNZB-02 or Aqara WSDCGQ11LM | Zigbee wireless sensor |

## Where to Buy

### Raspberry Pi

- [Raspberry Pi Official Resellers](https://www.raspberrypi.com/resellers/)
- Amazon, Micro Center, Adafruit
- Typically $60-80 USD for Pi 5 4GB

### Power Supply

Use the official Raspberry Pi power supply for your model:
- **Pi 5**: 27W USB-C power supply (~$12)
- **Pi 4**: 15W USB-C power supply (~$8)

Underpowered supplies cause instability.

### Storage Options

**microSD Card (Budget option)**
- Samsung Pro Endurance 64GB (~$12)
- SanDisk Max Endurance 64GB (~$14)
- Use high-endurance cards - regular SD cards fail faster

**NVMe SSD (Recommended)**
- Any M.2 NVMe SSD 128GB+ (~$20-40)
- Requires NVMe HAT or compatible case
- Much more reliable than SD cards

### Cases with NVMe Support

- **Argon ONE V3 M.2** (~$60) - Popular choice, good cooling
- **Pimoroni NVMe Base** (~$20) - Simple NVMe add-on board
- **Geekworm X1001** (~$25) - NVMe HAT

### Zigbee Coordinators

- **Sonoff ZBDongle-E** (~$20) - Recommended, uses EFR32MG21
- **SMLIGHT SLZB-06** (~$35) - Ethernet + USB option
- **ConBee II** (~$40) - Popular alternative

### Temperature Sensors

- **Sonoff SNZB-02** (~$10) - Budget option, works well
- **Aqara WSDCGQ11LM** (~$20) - Includes humidity + pressure
- **Sonoff SNZB-02D** (~$15) - With LCD display

## Assembly

### Basic Setup (SD Card)

1. Insert microSD card into Pi
2. Connect ethernet cable to router
3. Connect power supply
4. Proceed to [System Configuration](./rpi-ha-config.md)

### NVMe Setup

1. Install NVMe SSD into HAT or case
2. Attach to Raspberry Pi per case instructions
3. Connect ethernet cable to router
4. Connect power supply
5. Proceed to [System Configuration](./rpi-ha-config.md)

### Zigbee Coordinator

1. Plug USB coordinator into Pi after initial HA setup
2. Use a USB extension cable if signal is weak
3. Keep away from USB 3.0 ports (can cause interference)

## Network Considerations

### Wired Ethernet (Recommended)

- More reliable than WiFi
- Lower latency for automations
- Required for some advanced setups

### WiFi (If Necessary)

- Works but not recommended for always-on devices
- Configure during Home Assistant onboarding
- Use 2.4GHz for better range

## Next Steps

Once hardware is assembled:

→ [System Configuration](./rpi-ha-config.md) - Install and configure Home Assistant OS
