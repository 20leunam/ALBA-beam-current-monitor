# ALBA Beam Current Monitor

A lightweight browser dashboard that polls the ALBA Synchrotron public machine-status image, extracts the beam current (0–300 mA) with Tesseract.js OCR, and raises a configurable low-current alarm with a live gauge, status preview, and source-failure warning.

## Features

- Starts monitoring automatically when the page opens; the public `msGUI.html` status page is fetched every 30 seconds and OCR runs on the linked `msGUI.png` image.
- Displays the latest reading in mA with an interactive 0–300 mA gauge. Default alarm threshold: 125 mA.
- The **Low-current alarm** is its own card, using the same panel style as the other cards. The first row is the sliding **Enable alarm** switch; below it is **Alert if current is below:** with the threshold field. There is no Armed/Disabled badge and no test button.
- The gear icon opens a closable pop-up for alarm settings: by default the sound plays a fixed 3 cycles; it can also repeat until silenced or use 1–10 cycles, where each cycle is exactly three beeps.
- Temporal hysteresis: require 1, 2, or 3 consecutive low readings before sounding the alarm. While unconfirmed, the readout is steady red; once confirmed it flashes red and the alarm sounds.
- Silencing the alarm (or finishing the fixed-cycle mode) stops the sound and the flashing, but keeps the red low-current state until the reading recovers.
- The image preview keeps the source 16:9 aspect ratio. Amber is reserved for failures to load the image or when a loaded image contains no valid reading; in those cases the alarm does not sound.
- Alarm settings persist in `localStorage`.

## Live demo

https://20leunam.github.io/ALBA-beam-current-monitor/

## Usage

Just open the page: monitoring starts automatically. Keep the tab open — all OCR runs in the browser and there is no backend. Use **Stop** to pause and **Start monitoring** to resume. The alarm uses the Web Audio API, so the first user interaction may be required to enable audio.

Use the gear icon in the **Low-current alarm** panel to change the sound mode and the number of readings required to confirm a drop. Close the pop-up with the × button, **Done**, the Escape key, or by clicking outside it. Use the link at the bottom of the page to suggest changes or report issues.

## Notes

- The ALBA status page and image are served with `Access-Control-Allow-Origin: *`, so browser-side fetching works from GitHub Pages.
- Tesseract.js is loaded from the jsDelivr CDN.
- If the layout of the ALBA status page changes, image detection or OCR value selection may need adjustment.
