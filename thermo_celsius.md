# Home Assistant Animated Thermometer Card

A stylish, customizable temperature visualization card for Home Assistant that displays temperature readings as an animated thermometer with color-coded temperature ranges.

![Thermometer Card Preview](https://via.placeholder.com/600x400/1a1a1a/ffffff?text=Thermometer+Card+Preview)

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

5. Replace the entity ID with your own shutter/blind entity.

## Entity Requirements

The card expects a standard Home Assistant cover entity with these characteristics:

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

- If the animation doesn't work smoothly, check that your entity reports position changes properly
- For shutters that use an inverted scale (0 = closed, 100 = open), adjust the minState and maxState values
- If the shutter cover looks wrong, verify that your entity's current_position attribute follows standard conventions
- Make sure your entity reports position as a number between 0-100

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
