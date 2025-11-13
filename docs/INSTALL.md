# Installation Guide

## Prerequisites

You must complete the [Pi Imager Setup](PI_IMAGER_SETUP.md) **BEFORE** running this installer.

Required settings from Pi Imager:
- **OS:** Raspberry Pi OS (Legacy, 32-bit) Bookworm
- **Hostname:** aerojudge
- **Username:** resultskiosk
- **Password:** ScoreKiosk#2025
- **WiFi:** AeroJudgeNET
- **Password** 2Pr1v@TE
- **SSH:** Enabled

---

## Installation Steps

### 1. Boot Your Pi

Insert the SD card and power on your Raspberry Pi. Wait 2-3 minutes for first boot.

### 2. Connect via SSH

From your computer:

```bash
ssh resultskiosk@aerojudge.local
# Password: ScoreKiosk#2025
```

### 3. Clone Repository

```bash
git clone https://github.com/IMAC-ORG/score_results_kiosk.git
cd score_results_kiosk
```

### 4. Run Installer

```bash
chmod +x install.sh
./install.sh
```

The installer will:
- Install required packages (wtype, chromium-browser)
- Copy splash screen and scripts
- Configure Wayfire window manager
- Hide mouse cursor
- Set up auto-login
- Configure display rotation (portrait mode)
- Automatically reboot

**Total time:** ~2 minutes (plus reboot)

### 5. Verify

After reboot, your kiosk should automatically:
- Display splash screen for 3 seconds
- Switch to results page
- Rotate between splash and results continuously

---

## What Gets Installed

The installer creates/modifies:
- `~/splashv/splash.png` - Splash screen image
- `~/switchtab.sh` - Tab rotation script
- `~/.config/wayfire.ini` - Window manager config
- `~/.config/lxsession/LXDE-pi/autostart` - Auto-start config
- `/etc/systemd/system/getty@tty1.service.d/autologin.conf` - Auto-login

---

## Troubleshooting

### Installer Fails

**Package installation errors:**
```bash
sudo apt update
sudo apt upgrade
```
Then re-run installer.

**Permission denied:**
```bash
chmod +x install.sh
./install.sh
```

### Kiosk Not Starting After Reboot

**Check if Wayfire is running:**
```bash
ps aux | grep wayfire
```

**Check if Chromium is running:**
```bash
ps aux | grep chromium
```

### Results Not Showing

**Verify Score server:**
- Score must be running at 192.168.8.100
- Web server feature must be enabled in Score
- Results must be published to `reports\kiosk` folder

**Test URL directly:**
```bash
curl http://192.168.8.100/kiosk/report_results.html
```

### Re-run Installer

Safe to re-run installer multiple times:
```bash
cd score_results_kiosk
./install.sh
```

---

## Getting Help

If you encounter issues:

1. Check the troubleshooting steps above
2. Verify Pi Imager settings were applied correctly
3. Confirm you're using Raspberry Pi OS Legacy 32-bit
4. Check GitHub issues for similar problems
5. Create a new issue with error details

---

## Next Steps

Once installed and verified:

- Position display at your event within WiFi network range
- Test with actual Score results

Your kiosk is now ready for competition use!
