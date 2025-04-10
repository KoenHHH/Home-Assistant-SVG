# MPPT Controller Card for Home Assistant

A custom, visually appealing card for Home Assistant that displays Victron MPPT solar charge controller information with an intuitive interface.

<img width="164" alt="mppt" src="https://github.com/user-attachments/assets/3ffd1a95-15a0-4520-8fec-da39a38b28af" />

## Overview

This card creates a visual representation of your Victron MPPT solar charge controller that:
- Displays daily solar yield with an interactive progress bar
- Shows charging state indicators (BULK, ABSORPTION, FLOAT)
- Displays BMS and VE CAN connection status
- Updates dynamically as values change
- Provides intuitive navigation to detailed views

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Victron Energy integration with your MPPT controller

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Go to your dashboard, enter edit mode, and add a new card.

3. Choose "Manual" card and paste the YAML configuration from mppt.yaml.

4. Replace the entity IDs with those from your Victron system.

## Entity Requirements

The card expects the following entities:

| Entity | Purpose |
|--------|---------|
| `sensor.mppt_yield_today` | Main yield sensor (kWh produced today) |
| `sensor.mppt_state` | Charging state (BULK, ABSORPTION, FLOAT) |
| `binary_sensor.mppt_bms` | BMS connection status (on/off) |
| `binary_sensor.mppt_ve_can` | VE CAN connection status (on/off) |
| `sensor.mppt_power` | Current power output (W) |
| `sensor.mppt_current` | Current output (A) |

## Customization Options

The card includes several customization options within the SVG code:

### Visual Configuration

- Colors for different states and indicators
- Maximum yield value (default: 15 kWh)
- Layout and positioning of elements
- Text labels and sizes

### Style Configuration

- Card dimensions and positioning
- Background color and border styling
- Interactive elements behavior

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a dynamic visualization:

1. **Controller Frame**: Replicates the look of a physical Victron MPPT controller
2. **Status Indicators**: Shows charging state and connection status
3. **Yield Bar**: Visual progress bar showing daily production
4. **Power/Current Display**: Real-time values from your controller

The JavaScript code:
- Retrieves current states from various sensors
- Calculates the appropriate visual indicators based on values
- Determines the size of the yield progress bar based on production
- Formats and positions all elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the card doesn't appear correctly, ensure all required entities are properly reporting values
- Check that the entity IDs are correct and accessible
- Verify that button-card is properly installed
- If some indicators don't update, check the `triggers_update` list includes all needed entities

## Advanced Usage

### Multiple MPPT Controllers

To display multiple MPPT controllers on your dashboard:

1. Copy the card configuration multiple times
2. Change the entities for each card to match different controllers
3. Consider adjusting sizes or adding a grid layout to organize them

### Custom Actions

You can add custom actions to different parts of the visualization:

1. Add tap actions to the card configuration
2. Create navigation to more detailed views
3. Set up controls for manual mode changes

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Inspired by the physical appearance of Victron MPPT controllers
- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Victron Energy and Home Assistant communities
