---
layout: post
title: Moving to LAN
summary: Use nmcli to move the Pi to your WiFi, then update MatrixPortal wifi.txt.
order: 2
pinned: true
---

The Pi and MatrixPortal must be on the same network. The Pi can create its own setup AP, but normal running is easier when both devices join your LAN. The web configurator can do this for you when the MatrixPortal CIRCUITPY drive is mounted on the Pi. This page documents the manual flow.

<div class="warning">If you are SSHed into the Pi through the <code>deskradar</code> AP, switching WiFi will disconnect you. Use a local keyboard/monitor, serial console, or be ready to reconnect through the LAN IP once the Pi joins your router.</div>

## 1. Check the Current Network State

```sh
nmcli device status
nmcli connection show --active
nmcli device wifi list
```

The setup AP connection is named `deskradarAP`. The SSID it broadcasts is `deskradar`.

## 2. Connect the Pi to Your LAN WiFi

Replace `YourSSID` and `YourPassword` with your router's WiFi credentials. If a saved connection with the same name already exists, delete it first so NetworkManager uses the new password.

```sh
sudo nmcli connection delete "YourSSID"
sudo nmcli device disconnect wlan0
sudo nmcli device wifi rescan
sudo nmcli device wifi connect "YourSSID" password "YourPassword" ifname wlan0
```

If `connection delete` reports that the connection does not exist, that is fine. Run the remaining commands.

Confirm the Pi is connected and has an IP:

```sh
nmcli connection show --active
hostname -I
```

## 3. If It Fails, Bring Back the AP

If the Pi fails to join your LAN, bring the setup AP back up:

```sh
sudo nmcli connection up deskradarAP
```

You can then reconnect to SSID `deskradar` with password `deskradaradsb` and try again.

## 4. Mount the MatrixPortal CIRCUITPY Drive

Connect the MatrixPortal S3 to the Pi by USB so its CircuitPython storage appears under `/media/deskradar/`. It may be named `CIRCUITPY`, `CIRCUITPY1`, or similar.

```sh
ls /media/deskradar
findmnt
```

Use the active mounted CIRCUITPY path in the next step.

## 5. Update MatrixPortal wifi.txt

Only update `wifi.txt` after the Pi has successfully joined the LAN WiFi. The file must contain only two lines: SSID, then password. No labels, quotes, or extra text.

```sh
printf '%s\n%s' 'YourSSID' 'YourPassword' | sudo tee /media/deskradar/CIRCUITPY/wifi.txt >/dev/null
sync
```

If your mounted volume is `CIRCUITPY1` or another suffix, change the path:

```sh
printf '%s\n%s' 'YourSSID' 'YourPassword' | sudo tee /media/deskradar/CIRCUITPY1/wifi.txt >/dev/null
sync
```

## 6. Restart the MatrixPortal and Refresh the Pi Config

Reset or power-cycle the MatrixPortal. It should join the same LAN WiFi and advertise `deskradar-portal.local`. Then run the Pi boot check and restart the main app so `MATRIX_HTTP_URL` points to the MatrixPortal's LAN IP:

```sh
sudo systemctl start deskradar-bootstrap
sudo systemctl restart deskradar
```

Check the resolved URL in the config:

```sh
grep MATRIX_HTTP_URL /etc/deskradar/config.json
```

The value should look like `http://192.168.x.x:80` or another address from your LAN.

## What the Web Configurator Does

The configurator route `/switch-to-lan` follows the same idea in code: delete any existing connection named after the SSID, disconnect `wlan0`, connect with `nmcli device wifi connect`, and write MatrixPortal `wifi.txt` only after the Pi has connected. On failure it attempts to bring `deskradarAP` back and reboots without changing the MatrixPortal credentials.
