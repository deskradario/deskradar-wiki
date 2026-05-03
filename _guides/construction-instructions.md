---
layout: post
title: Construction Instructions
summary: Assemble the DeskRadar housing, electronics, matrix, and power wiring.
order: 3
pinned: true
---

These instructions cover the physical DeskRadar build: fitting the electronics into the housing, wiring the display and power, closing the case, and making the final external connections.

<div class="warning">Check power wiring before applying power. If you are using a buck converter or custom power rail, verify the output voltage before connecting it to the Raspberry Pi, MatrixPortal, or LED matrix.</div>

## Before You Start

You should have the main housing parts, 64x64 LED matrix, Raspberry Pi, MatrixPortal S3, LCD, USB pass-through, USB cable, FlightAware Pro Stick, HUB75 ribbon cable, rear power jack, buck converter, power rail, Wago connectors, screws, inserts, washers, and antenna ready.

<div class="note">These steps describe the internal power-rail build. If you are using the simpler Pi USB-C plus direct matrix power option, follow the power notes on the <a href="{{ '/hardware/' | relative_url }}">hardware page</a> for the power wiring.</div>

## 1. Prepare the Bottom Housing

Place the bottom housing on the bench with the internal mounting points facing upward. Keep the rear plate, top housing, matrix, and screws nearby so you can route cables before closing the case.

## 2. Attach the LCD

Fit the LCD before the other electronics make access tight.

1. Feed the LCD cable into position first.
2. Seat the bottom edge of the LCD in the housing.
3. Press the top edge in until it clicks into place.

## 3. Mount the Pi and MatrixPortal

Mount the Raspberry Pi in its housing position, then mount the MatrixPortal S3. Leave enough slack around both boards for the USB, LCD, HUB75, and power wiring that will be added later.

## 4. Fit the USB Pass-through and Internal USB Cable

Connect the panel-mount USB pass-through, then route the internal USB cable between the Pi and MatrixPortal.

1. Plug the internal USB cable into the lower USB 3 port on the Pi.
2. Route it over the other USB port.
3. Leave the loose end hanging out toward the rear until the MatrixPortal connection is ready.

## 5. Fit the ADS-B Receiver

Prepare and install the FlightAware Pro Stick.

1. Remove the receiver casing.
2. Place two washers over the antenna end.
3. Plug the receiver into the top USB 3 port on the Pi.

## 6. Prepare the Rear Plate and Power Input

Fit the rear power jack into the backplate before attaching the backplate to the model. Once the jack is secure, attach the backplate to the housing.

## 7. Add the Buck Converter and Power Rail

Wire the power system before the matrix is fitted.

1. Connect the rear power jack to the buck converter using the Wago connectors from the bill of materials.
2. Connect the power rail to the buck converter.
3. Connect the LCD wires and tuck them down at the front of the housing.
4. Connect the power rail output to the Pi.
5. Let the rail hang out toward the front while you position and stick down the buck converter.

## 8. Connect the MatrixPortal and HUB75 Cable

Plug the HUB75 ribbon cable into the MatrixPortal. Leave the matrix end of the cable accessible at the front of the housing so it can be connected after the top housing is in place.

## 9. Fit the Matrix and Close the Housing

Prepare the LED matrix and close the main housing.

1. Install the two long screws into the bottom of the LED matrix.
2. Fit the top housing onto the bottom housing.
3. Leave the power and HUB75 connections hanging out of the front.
4. Attach the power and HUB75 cable to the LED matrix.
5. Drop the matrix into the housing.
6. Install the rear screws.

## 10. Finish the Build

Attach the antenna to the receiver, then connect power. Watch the display and LCD during first boot so you can catch wiring, power, or MatrixPortal connection issues before closing up any remaining access points.
