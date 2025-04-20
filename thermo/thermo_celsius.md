# Thermometer Card For Home Assistant 

A stylish, customizable temperature visualization card for Home Assistant that displays temperature readings as an animated thermometer with color-coded temperature ranges.

<img width="125" alt="thermo" src="https://github.com/user-attachments/assets/e3bbea88-e8d4-4977-884b-2e2032dce88b" />

## Overview

- **Animated thermometer** that rises and falls with temperature changes
- **Color-coded temperature ranges** (blue for cold, green for comfortable, red for hot)
- **Customizable thresholds** for temperature ranges
- **Clean, modern design** with configurable styling
- **Responsive layout** that works on both desktop and mobile
- **Automatic updates** when temperature changes

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Temperature sensor entities

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `thermo_celsius.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own entity.

## Entity Requirements

The card expects a standard Home Assistant temperature entity with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `sensor.temperature` | Any sensor entity that measures temperature |

## Customization Options

The card includes several customization options within the code:

### Position and Color Configuration

  - `minState` and `maxState`: Defines the range of values
  - `blockHighValue` and `blockMiddleValue`: Thresholds for color changes
  - Color values for different states:
  - `color_green`: Color when temperature is comfortable
  - `color_red`: Color when warm
  - `color_blue`: Color cold

## Troubleshooting

### If the card doesn't display correctly:

  - Check if the Button Card custom component is properly installed
  - Verify that your temperature sensor entity exists and provides numerical values
  - Make sure the temperature sensor has a state within the configured min/max range OR change the thresholds.
  - Check the Home Assistant logs for any JavaScript errors

## Advanced Usage

### Multiple Temperature Cards

To display multiple temperature cards on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different shutter
3. Consider using a grid layout to organize them in rows/columns

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
