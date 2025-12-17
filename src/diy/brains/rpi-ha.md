# Raspberry Pi + Home Assistant

Build a Home Assistant controller on Raspberry Pi - the same platform used in Exergy kits.

## Guide Overview

This guide walks you through building a Raspberry Pi-based Home Assistant "brain" - a small home server that controls your bitcoin mining heaters and monitors your home environment.

The guide is split into two parts:

1. **[Hardware Setup](./rpi-ha-hardware.md)** - Assembling your Raspberry Pi and components
2. **[System Configuration](./rpi-ha-config.md)** - Installing and configuring Home Assistant OS

Before diving into those tutorials, review this page to understand what you'll need and why.

---

## Required Components

| Component | Description |
|-----------|-------------|
| **Raspberry Pi 5** | A small single-board computer that runs Home Assistant OS. This is the "brain" of your smart home system. 4GB or 8GB RAM models both work. |
| **Power Supply** | Powers the Raspberry Pi. Use the official 27W USB-C power supply - inadequate power causes instability and crashes. |
| **NVMe M.2 SSD** | Where your data is stored. Home Assistant writes sensor data frequently, so solid-state storage is essential. 128GB-256GB recommended. |
| **NVMe Expansion HAT** | An add-on board that connects the NVMe SSD to the Raspberry Pi. Required since the Pi doesn't have a built-in M.2 slot. |
| **Case with Cooling Fan** | Keeps the Pi cool and quiet. Active cooling (a fan) is recommended since the Pi 5 runs warm under load. |
| **Ethernet Cable** | Cat5e or better. Required for initial setup. |

## Optional Components

| Component | Description |
|-----------|-------------|
| **Zigbee Coordinator** | A USB or radio-to-pi_hat antenna that listens for Zigbee radio signals (not WiFi). Enables communication with Zigbee sensors and devices like temperature sensors. Recommended to minimize Wi-Fi connected devices in the home and increase stability. |

## For Installing Home Assistant OS

You'll need one of the following setups to flash Home Assistant OS onto your NVMe SSD. See [System Configuration](./rpi-ha-config.md) for details on each method.

**Option A: Network Installer (Recommended)**

| Component | Description |
|-----------|-------------|
| **HDMI Cable** | To connect Pi to a display. Some cases/expansion boards include full-size HDMI ports; otherwise you'll need a Micro-HDMI to HDMI cable or adapter. |
| **Monitor or TV** | Any display with HDMI input to see the installer GUI. |
| **USB Keyboard** | To navigate the Network Installer menus. |

**Option B: Raspberry Pi Imager**

| Component | Description |
|-----------|-------------|
| **NVMe-to-USB Adapter** | Allows you to connect your NVMe SSD to a computer for flashing before installing it in the Pi case. |
| **Computer** | Mac, Windows, or Linux computer to run Raspberry Pi Imager. |

---

## Important: Don't Use MicroSD Cards

The Raspberry Pi has a microSD card slot, and Home Assistant OS *can* run from an SD card. **However, this is not recommended.**

Home Assistant continuously writes sensor data, logs, and database updates. This constant read/write activity wears out microSD cards quickly - often within months. When the card fails, you lose your configuration and automation history.

**Always use an NVMe SSD** for reliable, long-term operation. It's faster and will last years instead of months.

---

## Network Requirements

**For initial setup:** You must connect via Ethernet cable. Home Assistant OS needs a wired connection for first-time configuration.

**After setup:** You can switch to WiFi through Home Assistant settings if preferred.

---

## Where to Buy Components
Here's our Recommended Setup

| Component | Recommended Products | Where to Buy |
|-----------|---------------------|--------------|
| Raspberry Pi 5 (8GB) | Raspberry Pi 5 | [Amazon](https://www.amazon.com/Raspberry-Pi-8GB-SC1112-Quad-core/dp/B0CK2FCG1K/), [Micro Center](https://www.microcenter.com/product/673711/raspberry-pi-5), [PiShop](https://www.pishop.us/) |
| Power Supply | Official 27W USB-C | [Amazon](https://www.amazon.com/iUniker-USB-C-Power-Supply-Raspberry/dp/B0FJLDFMF7/), [Micro Center](https://www.microcenter.com/product/671927/raspberry-pi-27w-usb-c-psu-black), [PiShop](https://www.pishop.us/) |
| NVMe SSD | Samsung 970 EVO Plus, WD Blue SN570 | [Amazon](https://www.amazon.com/), [Micro Center](https://www.microcenter.com/), [Newegg](https://www.newegg.com/) |
| NVMe Expansion Card + Case | Argon ONE V5 NVMe Base | [Amazon](https://www.amazon.com/Argon-Case-Raspberry-Aluminum-Single/dp/B0DKWMKBK2/) |
| Zigbee Coordinator | Argon Industria / Sonoff | [Amazon (Works With Argon One V5 Case Only)](https://www.amazon.com/Argon-Forty-Industria-ZigBee-Module/dp/B0DWM9HKQB/), [Amazon](https://www.amazon.com/SONOFF-Gateway-Universal-Assistant-Wireless/dp/B09KXTCMSC/) |

---

## Tools Needed

If you purchased a complete Raspberry Pi kit designed for Home Assistant, you likely have everything ready to assemble.

If you're sourcing components separately, you may need:

- **Small Phillips screwdriver** - For mounting the Pi in the case and attaching the NVMe HAT
- **Thermal paste or thermal pads** - Often included with cases, but verify before assembly

---

## Next Steps

Ready to build? Start with **[Hardware Setup](./rpi-ha-hardware.md)** to assemble your components.
Just need to configure Home Assistant OS? Start with **[System Configuration](./rpi-ha-config.md)** to get things dialed in.
