# Prusa 3D Printer Status Card

A compact, single-card Home Assistant dashboard for monitoring and controlling a Prusa MK4 (other Prusa printers should also work; I only have a MK4 to test) 3D printer via PrusaLink. Combines status, temperatures, print preview, progress bar, and control buttons into one clean card.

![3D Printer Card full Screenshot](https://raw.githubusercontent.com/qtmo0/3D-Printer-Card/refs/heads/main/screenshot_1.png)

## Features

- **Live status** with colored indicator (Printing, Paused, Ready, Error, …)
- **Status chips** for nozzle, heatbed, enclosure temperature, material, and power draw
- **Print preview** image from PrusaLink alongside filename
- **Animated progress bar** with elapsed time, remaining time, start time, and estimated finish time
- **Smart control buttons** — Cancel, Pause/Resume (toggles automatically), Power — visible only when relevant
- **Two-tap confirmation** on destructive actions, with customizable timeout
- **Mobile-friendly** — proper touch event handling for iOS and Android
- **Card tap** navigates to a detail dashboard

## Requirements

- [Home Assistant](https://www.home-assistant.io/) 2024.2 or newer
- [PrusaLink integration](https://www.home-assistant.io/integrations/prusalink/) (built-in)
- [`button-card`](https://github.com/custom-cards/button-card) via HACS

### Optional

- Tasmota-flashed smart plug for power control and consumption tracking
- BLE thermometer for enclosure temperature

## Installation

1. Install `button-card` via HACS if you haven't already
2. Copy the contents of [`printer_card_en.yaml`](./printer_card_en.yaml) into a Manual card on your dashboard
3. Adjust the entity IDs in the `variables:` block at the top to match your setup

## Configuration

All settings live in the `variables:` block at the top of the YAML. No need to touch the template logic below.

### Display options

| Variable | Default | Description |
|---|---|---|
| `show_buttons` | `true` | Show control buttons during a print |
| `show_power_button` | `true` | Show power button when printer is idle |
| `show_confirmations` | `true` | Require two-tap confirmation for actions |
| `confirmation_text` | `Really?` | Text shown on first tap |
| `confirmation_timeout` | `3` | Seconds before confirmation resets |
| `navigation_path` | `/lovelace/printer` | Where card tap navigates to |
| `printer_name` | `MK4` | Display name shown in the card header |

### Entities

All entity IDs are defined as variables and can be reassigned individually. Most users only need to change the entity prefix if their PrusaLink integration uses a non-default name. See the YAML for the full list.

Two entities are fully optional — if you don't have the hardware, simply leave the variable empty and the corresponding chip will not be shown:
VariableChipRequired hardwareentity_enclosure_tempEnclosure temperatureBLE thermometer inside the enclosureentity_power_wattsPower draw in wattsSmart plug with energy monitoring

| Variable | Chip | Required hardware |
|---|---|---|
| `entity_enclosure_temp` | Enclosure temperature | BLE thermometer inside the enclosure |
| `entity_power_watts` | Power draw in watts | Smart plug with energy monitoring |


## Customization

- **Disable a section** by setting its `show_*` boolean to `false`
- **Reuse for a second printer** by copying the card and updating the `entity_*` variables
- **Translate labels** by editing the `statusMap` and button labels in the template

## Screenshots

![3D Printer Card without buttons](https://raw.githubusercontent.com/qtmo0/3D-Printer-Card/refs/heads/main/screenshot_2.png)

![3D Printer Card Print Finished](https://raw.githubusercontent.com/qtmo0/3D-Printer-Card/refs/heads/main/screenshot_3.png)

![3D Printer Card Print Finished](https://raw.githubusercontent.com/qtmo0/3D-Printer-Card/refs/heads/main/screenshot_4.png)

The last screenshot is from the German version, which might suit you if you speak German. However, feel free to choose the English version instead.

## Artificial Intelligence

Artificial intelligence tools were used in the development of this card, including assistance with YAML templating, feature design, and documentation. All functionality has been tested on a Prusa MK4 printer.

## License

GPL-3.0 license
