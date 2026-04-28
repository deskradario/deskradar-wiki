---
layout: post
title: What Is ADS-B?
summary: The aircraft broadcast data DeskRadar turns into pixels.
order: 1
---

ADS-B stands for Automatic Dependent Surveillance-Broadcast. In simple terms, an aircraft works out its own position, usually from satellite navigation, and broadcasts that position and other flight data by radio. A ground receiver can decode those messages without needing to ask the aircraft directly.

## What DeskRadar Receives

DeskRadar does not decode raw radio messages itself. A local dump1090-style receiver does that job and exposes a JSON file at `/data/aircraft.json`. The main app polls that endpoint and keeps aircraft that include the fields it needs to draw a useful track:

| Field | Use in DeskRadar |
| --- | --- |
| `lat` and `lon` | Converted to matrix `x`/`y` pixels relative to the configured display centre. |
| `alt_geom` | Used for altitude filtering, altitude color, stale-track behavior, and pixel conflict resolution. |
| `flight` | Used as the per-flight store key and shown on the LCD for the closest aircraft. |
| `hex` | Aircraft identifier retained in each point. |
| `seen` | Required by the sanitiser so the block is considered complete. |

## Why Some Aircraft Do Not Appear

ADS-B reception is not the same as an internet flight tracking site. DeskRadar only knows what the local receiver can hear. Aircraft can be missing because the antenna cannot hear them, the message does not include position, the callsign is absent, the aircraft is below `MIN_ALT`, or the aircraft is outside the configured display radius.

## 1090 MHz and dump1090

Most DeskRadar builds are expected to use a 1090 MHz ADS-B receiver with dump1090 or a compatible decoder. dump1090 listens to the SDR, decodes messages, and publishes the live aircraft list. DeskRadar consumes that local JSON API rather than talking to the SDR directly.

## How ADS-B Becomes a Matrix Track

1. The receiver hears aircraft broadcasts and dump1090 publishes JSON.
2. The Pi polls the JSON endpoint once per `POLL_CADENCE`.
3. The app drops incomplete, too-low, or out-of-bounds aircraft.
4. Latitude and longitude are mapped to a 64x64 pixel grid.
5. Altitude is converted to RGB color.
6. Historical points fade, gaps are filled, and duplicate pixels are collapsed.
7. The final pixel list is posted to the MatrixPortal `/draw` endpoint.

<div class="note">DeskRadar is a local display project, not an air traffic control system. It is limited by receiver coverage, ADS-B message content, local config, and the current filtering pipeline.</div>
