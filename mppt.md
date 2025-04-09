# MPPT Controller Card for Home Assistant

A custom button card for Home Assistant that displays Victron MPPT solar charge controller information in a visually appealing interface.

![mppt](https://github.com/user-attachments/assets/57a3c052-b81e-4e5b-84b6-035603203883)

## Features

- Visual representation of your Victron MPPT solar charge controller
- Displays daily solar yield with progress bar
- Shows charging state indicators (BULK, ABSORPTION, FLOAT)
- Displays BMS and VE CAN connection status
- Customizable layout with SVG graphics
- Interactive navigation to detailed view

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Victron energy integration with your MPPT controller

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed
2. Add this card configuration to your dashboard

## Usage

Add the mppt.yaml to your Lovelace configuration:

## Configuration Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| entity | string | **Required** | Main entity ID of the MPPT's yield sensor |
| show_name | boolean | false | Whether to show the entity name |
| show_icon | boolean | false | Whether to show the entity icon |
| triggers_update | list | **Required** | List of entities that should trigger update of the card |
| custom_fields | object | **Required** | Contains the mppt_controller SVG definition |
| styles | object | **Required** | CSS styling for the card |

## Entity Requirements

The card expects the following entities:

- `sensor.mppt_yield_today` - Main yield sensor (change to match your entity)
- `sensor.mppt_state` - Charging state (BULK, ABSORPTION, FLOAT)
- `binary_sensor.mppt_bms` - BMS connection status (on/off)
- `binary_sensor.mppt_ve_can` - VE CAN connection status (on/off)

## Customization

The card is highly customizable through the SVG code. You can modify:

- Colors (main blue, orange accents, indicator colors)
- Maximum yield value (default 15 kWh)
- Layout and positioning of elements
- Text labels and sizes

## Troubleshooting

- If the card doesn't update, make sure all required entities are available
- Check the browser console for JavaScript errors
- Ensure the entity IDs match your system

## Credit

This card was inspired by the physical appearance of Victron MPPT controllers and created to provide at-a-glance information about solar production.

## License

MIT
