---
layout: post
title: Build Guide
summary: "Everything you need to build a DeskRadar64, from parts to first boot."
order: -1
pinned: true
---

This guide walks you through the full build in order. Follow each step, then continue to the next — no need to jump between pages.

## Before You Start

You will need:

- Raspberry Pi (4 or 5)
- Adafruit MatrixPortal S3
- 64x64 HUB75 RGB LED matrix
- FlightAware Pro Stick SDR receiver
- 16x2 I2C LCD display
- Enclosure (printed or purchased)
- Power supply and wiring (see power options on the hardware page)
- Cables: USB-A to USB-C (Pi → MatrixPortal), HUB75 ribbon

The full parts list with suppliers and quantities is below. The <a href="{{ '/hardware/' | relative_url }}">Hardware page</a> also covers the two power options in detail.

<a href="https://docs.google.com/spreadsheets/d/1Lz8ZiZV83O61dhBWZ0qu6fqzqWgGCzJ0g4K8_wqb5GY/" target="_blank" rel="noopener noreferrer">Open the sheet in Google Sheets</a>

<div class="sheet-embed">
  <iframe
    src="https://docs.google.com/spreadsheets/d/1Lz8ZiZV83O61dhBWZ0qu6fqzqWgGCzJ0g4K8_wqb5GY/preview"
    title="DeskRadar bill of materials">
  </iframe>
</div>

## 1. Get the Enclosure

You can print or buy the enclosure.

- **Print it:** Download the STL files from <a href="https://www.printables.com/model/1704248-deskradar64-full-housing" target="_blank" rel="noopener noreferrer">Printables</a>.
- **Buy it:** Order from the <a href="https://shop.deskradar.io" target="_blank" rel="noopener noreferrer">DeskRadar Etsy store</a>.

## 2. Flash the Pi Image

Download and flash the DeskRadar Pi image. All software is pre-installed and configured — no manual setup needed.

Go to the <a href="{{ '/pi_image/' | relative_url }}">DeskRadar Pi Image</a> page for the download link and flashing instructions. The default credentials are:

| | |
|---|---|
| Username | `deskradar` |
| Password | `adsb` |
| Hostname | `deskradar.local` |

## 3. Install the MatrixPortal Firmware

The MatrixPortal S3 runs CircuitPython firmware that accepts pixel data over HTTP and drives the LED matrix. You need to install CircuitPython first, then copy the DeskRadar firmware onto the device.

Follow the <a href="{{ '/guides/install-circuitpython/' | relative_url }}">Install CircuitPython</a> guide, which covers both steps.

## 4. Assemble

With parts in hand and both devices flashed, assemble the hardware. Follow the <a href="{{ '/guides/construction-instructions/' | relative_url }}">Construction Instructions</a> from start to finish.

Before you begin assembly, decide which power option you are using — the construction instructions note where the steps differ. The power options are described on the <a href="{{ '/hardware/' | relative_url }}">Hardware page</a>.

## 5. Initial Setup

Power on DeskRadar. The Pi broadcasts a WiFi access point named `deskradar`.

Follow the <a href="{{ '/guides/initial-setup/' | relative_url }}">Initial Setup guide</a> to connect, open the configurator, and set your location and display preferences. Once saved, aircraft in range should start appearing on the matrix.

If you need help at any point, email <a href="mailto:deskradar@deskradar.io">deskradar@deskradar.io</a>.
