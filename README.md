
# ASUS Laptop Setup for Arch Linux

A concise guide to power management and hardware control for ASUS ROG and TUF laptops on Arch Linux.

## 1. Power Management (TLP)
Optimize battery life and set charging thresholds.

**Configuration:** Edit `/etc/tlp.conf` to set charging limits (e.g., to prolong battery health):
```bash
START_CHARGE_THRESH_BAT0=75
STOP_CHARGE_THRESH_BAT0=80
```

**Commands:**
```bash
sudo tlp start              # Start TLP
sudo systemctl enable tlp   # Enable on boot
sudo tlp-stat -s            # Check status
```

---

## 2. ASUS & Graphics Control
Utilities for keyboard backlighting, fan profiles, and GPU switching.

### Enable Services
```bash
sudo systemctl enable --now asusd.service
sudo systemctl enable --now supergfxd.service
```

### Kernel Modules
Ensure the necessary ASUS WMI modules are loaded:
```bash
# Check if loaded
lsmod | grep asus

# If missing, load them manually
sudo modprobe asus_nb_wmi
sudo modprobe asus_wmi

# Make changes permanent
echo -e "asus_nb_wmi\nasus_wmi" | sudo tee /etc/modules-load.d/asus.conf
```

---

## 3. Usage & Modes

### Keyboard & Profiles (`asusctl`)
*   `asusctl` — View help and available modes.
*   `asusctl -k auto` — Set keyboard brightness to auto.
*   `asusctl aura static` — Set a static color for the keyboard backlight.

### GPU Switching (`supergfxctl`)
Switch between integrated and dedicated graphics:

| Mode | Description |
| :--- | :--- |
| `Integrated` | iGPU only. Best for battery life. |
| `Hybrid` | Default. Uses iGPU, switches to dGPU when needed. |
| `Dedicated` | dGPU only. Best for performance/gaming. |
| `VFIO` | Passes the dGPU to a Virtual Machine (QEMU/KVM). |

**Command:** `supergfxctl -m <mode>`

---

## 4. GUI Interface
For a visual control center, install the **ROG Control Center** from the AUR:

```bash
# Example using yay
yay -S rog-control-center
```

## Troubleshooting
If services are unresponsive:
```bash
sudo systemctl daemon-reload
sudo systemctl restart asusd
```
Verify hardware detection with `lsusb` (Look for `ASUSTek Computer, Inc. N-KEY Device`).
