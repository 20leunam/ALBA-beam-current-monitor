# ALBA Beam Current Monitor

A lightweight browser dashboard that polls the ALBA Synchrotron public machine-status image, extracts the beam current (0–300 mA) with Tesseract.js OCR, and raises a configurable low-current alarm with a live gauge, status preview, and diagnostics log.

## Features

- Fetches the public `msGUI.html` status page every 30 seconds and runs OCR on the linked `msGUI.png` image.
- Displays the latest reading in mA with an interactive 0–300 mA gauge.
- Configurable low-current alarm: threshold, enable/disable, audio test, and silence button.
- Live machine-status image preview and an OCR diagnostics log.
- Alarm settings persist in `localStorage`.

## Live demo

https://20leunam.github.io/ALBA-beam-current-monitor/

## Usage

Open the page and click **Start monitoring**. Keep the tab open — all OCR runs in the browser and there is no backend. The alarm uses the Web Audio API, so the first user interaction is required to enable audio.

## Notes

- The ALBA status page and image are served with `Access-Control-Allow-Origin: *`, so browser-side fetching works from GitHub Pages.
- Tesseract.js is loaded from the jsDelivr CDN.
- If the layout of the ALBA status page changes, image detection or OCR value selection may need adjustment.
