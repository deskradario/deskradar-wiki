---
layout: post
title: Initial Setup
summary: Join the DeskRadar setup AP, open the web configurator, update settings, and save them.
order: 0
pinned: true
---

Use the setup access point when DeskRadar is running for the first time or has fallen back to AP mode. Keep your phone or laptop connected to the DeskRadar WiFi while you change settings.

## 1. Join the DeskRadar WiFi

Open WiFi settings on your phone or laptop and join:

| Setting | Value |
| --- | --- |
| SSID | `deskradar` |
| Password | `deskradaradsb` |

Wait until the device says it is connected. It may warn that the network has no internet access; that is expected during setup.

## 2. Open the Configurator

Open a browser and go to:

```text
http://deskradar.local:5000
```

If that does not load, try the Pi AP address directly:

```text
http://10.42.0.50:5000
```

## 3. Amend the Settings

Update the settings for your build and location. The most important values are:

| Setting | What to set |
| --- | --- |
| `LAT` | Your display centre latitude in decimal degrees. |
| `LON` | Your display centre longitude in decimal degrees. |
| `DISPLAY_RADIUS_NM` | The radius, in nautical miles, to show around your location. |
| `MIN_ALT` | Minimum altitude in feet before aircraft are drawn. |

Leave system-managed URLs alone unless you are debugging. The configurator hides the main managed URLs in normal use.

## 4. Save the Settings

Use the configurator's save button after making changes. The settings are written to `/etc/deskradar/config.json`.

After saving, allow the DeskRadar services a moment to pick up the new configuration. If you changed network settings, your device may disconnect from the `deskradar` AP and need to reconnect on the new network.

## 5. Check the Display

The LED matrix should resume updates once DeskRadar can read aircraft data and reach the MatrixPortal. The LCD should show status messages and, when aircraft are in range, the current closest aircraft.
