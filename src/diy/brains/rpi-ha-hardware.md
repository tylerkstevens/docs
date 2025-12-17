# Hardware Setup

This guide walks through physically assembling and connecting your Raspberry Pi hardware in preparation for installing Home Assistant OS.

If you haven't gathered your components yet, see [Raspberry Pi + Home Assistant](./rpi-ha.md) for the full list of required and optional hardware.

---

## Pre-Assembled Brain

If you purchased a pre-assembled Raspberry Pi Home Assistant brain (or already have yours built), skip to [Step 2: Connect to Ethernet](#step-2-connect-to-ethernet).

---

## Step 1: Assemble Your Hardware

There are many Raspberry Pi cases, NVMe expansion boards, and cooling solutions available. Assembly varies by kit, so **follow the instructions that came with your specific components**.

General assembly typically involves:

1. **Install the NVMe SSD** into your expansion HAT or case's M.2 slot
2. **Mount the Raspberry Pi** into the case or onto the expansion board
3. **Attach cooling** - install heatsinks, thermal pads, or connect the cooling fan
4. **Close the case** and secure any screws

**Tip:** If your case includes a Zigbee module (like the Argon ONE V5 with Industria), install it now per the manufacturer's instructions. USB Zigbee dongles can be plugged in later.

---

## Step 2: Connect to Ethernet

Plug an Ethernet cable into:
- The Ethernet port on your Raspberry Pi
- An available port on your router or network switch

Ethernet is required for the initial Home Assistant setup. You can switch to WiFi later if needed.

---

## Step 3: Connect Power

Plug the power supply into your Raspberry Pi.

Ensure your power supply is switched on if it has a switch.

The device will likely boot automatically - Many raspberry pi cases have no power button. If your case has a power button, press it once. You'll see indicator lights come on, and the fan (if equipped) will spin up.

**Wait 2-3 minutes** for the initial boot to complete before proceeding.

---

## Next Steps

Your hardware is ready. Continue to **[System Configuration](./rpi-ha-config.md)** to install and set up Home Assistant OS.
