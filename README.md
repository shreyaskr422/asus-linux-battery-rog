# ASUS Arch Linux Guide

Quick setup for power management and hardware control on ASUS ROG/TUF laptops.

---

### 1. Power Management (TLP)
Edit `/etc/tlp.conf` for battery health:
```conf
START_CHARGE_THRESH_BAT0=75
STOP_CHARGE_THRESH_BAT0=80
```
**Apply settings:**
```bash
sudo tlp start && sudo systemctl enable tlp
```

### 2. ASUS Control & GPU Switching
**Enable Services:**
```bash
sudo systemctl enable --now asusd.service supergfxd.service
```

**Ensure Kernel Modules Load:**
```bash
echo -e "asus_nb_wmi\nasus_wmi" | sudo tee /etc/modules-load.d/asus.conf
```

---

### 3. Core Commands

#### **asusctl** (Profiles & RGB)
- `asusctl -k auto` — Auto keyboard brightness.
- `asusctl aura static` — Static RGB backlight.
- `asusctl --help` — List all modes.

#### **supergfxctl** (GPU Modes)
| Command | Mode | Use Case |
| :--- | :--- | :--- |
| `supergfxctl -m Integrated` | **iGPU** | Maximum battery life. |
| `supergfxctl -m Hybrid` | **Both** | Standard balanced use. |
| `supergfxctl -m Dedicated` | **dGPU** | Gaming / Performance. |
| `supergfxctl -m VFIO` | **Pass** | Virtual Machines (QEMU). |

---

### 4. GUI & Troubleshooting
- **GUI:** Install `rog-control-center` from the AUR.
- **Reload:** If settings don't apply, run:
  `sudo systemctl daemon-reload && sudo systemctl restart asusd`
