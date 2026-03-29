# Hardware Setup

## 1. Blacklist the TV Driver

The Linux kernel loads `dvb_usb_rtl28xxu` by default — this is the DVB-T TV driver that claims the dongle before SDR software can. Blacklist it:

```bash
echo 'blacklist dvb_usb_rtl28xxu' | sudo tee /etc/modprobe.d/rtlsdr.conf
sudo modprobe -r dvb_usb_rtl28xxu  # unload without reboot
```

Why: the dongle is a generic ADC, not a TV receiver. The TV driver locks it into a specific mode and blocks the raw IQ access that rtl-sdr needs.

## 2. udev Rule (Non-Root Access)

```bash
sudo tee /etc/udev/rules.d/20-rtlsdr.rules <<'EOF'
SUBSYSTEM=="usb", ATTRS{idVendor}=="0bda", ATTRS{idProduct}=="2838", GROUP="plugdev", MODE="0664"
EOF
sudo udevadm control --reload-rules && sudo udevadm trigger
# Replug the dongle
```

Check your user is in `plugdev`: `groups $USER`. If not: `sudo usermod -aG plugdev $USER` and relog.

## 3. Verify

```bash
rtl_test -t
```

Expected output:
```
Found 1 device(s):
  0:  Realtek, RTL2838UHIDIR, SN: ...
Using device 0: Generic RTL2832U OEM
Found Rafael Micro R820T tuner
...
No errors
```

If you see `usb_open error -3`: udev rule not applied yet, or not in plugdev group.
If you see `No supported devices found`: TV driver is still loaded.

## 4. PPM Calibration (Optional but Recommended)

The dongle's crystal oscillator drifts slightly from the stated frequency. Run:

```bash
rtl_test -p
```

Let it run for 1–2 minutes. Note the reported PPM error. Enter this value in SDR++Brown: Settings → General → PPM. Typical range: −20 to +20 ppm. Matters most for narrow signals like APRS and NOAA; FM doesn't care.

## Note: inspectrum

inspectrum is installed via `pacman`, not Nix. If you invoke it from a Nix shell, it may not be on PATH. Open a regular terminal (not `nix-shell`) to launch it.
