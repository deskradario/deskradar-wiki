---
layout: post
title: Build Guide
summary: "Everything you need to build a DeskRadar64, from parts to first boot."
order: -1
pinned: true
---

This guide covers the full build in order. Each step links to further detail where needed — follow them in sequence.

---

## What You Need

### Enclosure

Buy from the store or print yourself.

**[shop.deskradar.io](https://shop.deskradar.io) — recommended options:**

| Item | Price |
|------|-------|
| Full Housing With Threads and Fixings | £60 |
| Frosted Acrylic Diffuser (optional) | £10 |

The full housing is the easiest option — both shells, the rear panel, brass heat-insert threads, and all fixings in one order. The frosted acrylic diffuser sits over the matrix and softens the display.

Individual parts are also available if you only need specific pieces: Lower Housing with Threads (£15), Upper Housing (£15), Rear Housing Panel (£5), Full Fixings Set (£5), Brass Heat-Insert Threads (£5), Lower Housing Only (£10).

**Print yourself:**  
STL files are free on <a href="https://www.printables.com/model/1704248-deskradar64-full-housing" target="_blank" rel="noopener noreferrer">Printables</a>. A paid download (£36) is available from the store if you'd like to support the project.

---

### Electronics

Source from the <a href="{{ '/hardware/' | relative_url }}">Bill of Materials</a>. You will need:

- Raspberry Pi 4 or 5
- Adafruit MatrixPortal S3
- 64×64 HUB75 RGB LED matrix
- FlightAware Pro Stick SDR receiver
- 16×2 I2C LCD display
- USB-A to USB-C cable (Pi → MatrixPortal, internal)
- HUB75 ribbon cable
- Power supply — see Power Options below

<a href="https://docs.google.com/spreadsheets/d/1Lz8ZiZV83O61dhBWZ0qu6fqzqWgGCzJ0g4K8_wqb5GY/" target="_blank" rel="noopener noreferrer">Open the full BOM in Google Sheets</a>

<div class="sheet-embed">
  <iframe
    src="https://docs.google.com/spreadsheets/d/1Lz8ZiZV83O61dhBWZ0qu6fqzqWgGCzJ0g4K8_wqb5GY/preview"
    title="DeskRadar bill of materials">
  </iframe>
</div>

---

### Power Options

Decide which power option you're using before you start — the assembly steps differ.

**Option 1 — Pi USB-C + direct matrix power (simpler)**  
Power the Pi via its USB-C port through the side opening on the enclosure. A separate 12 V barrel jack supply runs to the LED matrix via the rear jack and Wago connectors. The MatrixPortal is powered from the Pi over USB. Simple and reliable, but a cable exits the side of the case.

**Option 2 — Custom power rail (cleaner)**  
A single 12 V supply through the rear jack powers everything internally — no cables exit through the side. See the <a href="{{ '/guides/custom-power-rail/' | relative_url }}">Custom Power Rail guide</a> for wiring details. This option is coming to the store.

---

## Step 1 — Flash the Pi Image

Download the DeskRadar Pi image and flash it to your SD card. All software is pre-installed — no manual setup needed on the Pi.

Go to the <a href="{{ '/pi_image/' | relative_url }}">DeskRadar Pi Image</a> page for the download link and flashing instructions. Default credentials:

| | |
|---|---|
| Username | `deskradar` |
| Password | `adsb` |
| Hostname | `deskradar.local` |

---

## Step 2 — Install the MatrixPortal Firmware

The MatrixPortal S3 runs CircuitPython firmware that receives pixel data over HTTP and drives the LED matrix. You need to install CircuitPython first, then copy the DeskRadar firmware onto the device.

Follow the <a href="{{ '/guides/install-circuitpython/' | relative_url }}">Install CircuitPython</a> guide — it covers both steps.

---

## Step 3 — Assemble

With your enclosure and both devices flashed, build the hardware. Follow the <a href="{{ '/guides/construction-instructions/' | relative_url }}">Construction Instructions</a> from start to finish.

Make a note of which power option you're using before you start — the construction instructions call out where the steps differ.

---

## Step 4 — Initial Setup

Power on DeskRadar. The Pi broadcasts a WiFi access point named `deskradar`.

Follow the <a href="{{ '/guides/initial-setup/' | relative_url }}">Initial Setup guide</a> to connect, open the web configurator, and set your location and display preferences. Once saved, aircraft in range will start appearing on the matrix.

---

Need help? Email <a href="mailto:deskradar@deskradar.io">deskradar@deskradar.io</a>.
