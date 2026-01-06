# AMD BC-250 Steam Machine Guide

> 🎮 A  guide for building a Steam Machine from an AMD BC‑250 mining board

---

## 📦 3D Printed Case

Get a custom 3D printed case from [Thingiverse](https://www.thingiverse.com/thing:7165679).

> **Note:** You may need to use TinkerCAD to enlarge the space for the PSU in the `Shell_Back_FLEX_ATX.stl` file depending on the PSU you're using.

I've also added a modified `Shell_Back_Dell.stl` to the repo that I'm using with a Dell server PSU.

---

## ⚡ Power Supply Requirements

You will need a **400W PSU**.

If you're using a Dell server PSU, you'll need to:
1. Make a custom cable for it
2. Short pins **S13**, **S14**, and **S16** on the PSU

> 📌 A pinout diagram has been added to the repo for reference.

---

## 🌀 Cooling Setup

If using the mentioned case, you'll need to straighten the radiator fins. Options:
- **Print a tool:** [BC-250 Scooper on Printables](https://www.printables.com/model/1282906-bc-250-scooper)
- **Buy a fin straightener online**

The case uses **Arctic 12 Pro fans** for cooling. You can use one or two of these fans.

---

## 📡 Wireless Connectivity

You will probably need dongles for WiFi and Bluetooth. Here are my recommendations:

| Type | Model |
|------|-------|
| WiFi | D-LINK DWA-181 |
| Bluetooth | TP-LINK UB500 Plus |

---

## 💾 Storage

You will need an **M.2 NVMe 2280 SSD** (the board supports PCIe 2.0).

---

## 🐧 Operating System

Download **Bazzite** (SteamOS-based distro):  
👉 [bazzite-deck-stable-live.iso](https://download.bazzite.gg/bazzite-deck-stable-live.iso)

---

## ⚙️ Performance Tuning

### GPU Governor

By default, the GPU clock will always stay at 1500MHz. To enable dynamic GPU clocking up to 2000MHz:

```bash
sudo copr enable filippor/bazzite
sudo rpm-ostree install oberon-governor
systemctl reboot
systemctl enable --now oberon-governor
```

### GPU Overclocking

Edit `/etc/oberon-config.yaml` to tune frequency and voltage:
- **Max frequency:** up to 2230MHz
- **Voltage:** 1129mV

> ⚠️ My board overheated at 2230MHz, so I went with **2100MHz** and undervolted it slightly.

After making changes, restart the governor:

```bash
systemctl restart oberon-governor
```

### Disable Mitigations (Optional)

For extra performance (at the cost of security):

```bash
sudo rpm-ostree kargs --append-if-missing="mitigations=off"
```

> ⚠️ **Warning:** This makes your board vulnerable to some well-known exploits.

### Increase ZRAM

To increase ZRAM to 16GB, edit `/etc/systemd/zram‑generator.conf`:

```
zram-size=16384
```

### Fan Control

To control fan speed from desktop, install CoolerControl:

```bash
ujust install-coolercontrol
```

---

**Happy building!** 🛠️
