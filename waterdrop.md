# Water Usage Card For Home Assistant 

A visually appealing, customizable water consumption visualization card for Home Assistant that displays water usage readings as an animated water droplet with color-coded usage ranges.

<img width="125" alt="waterdrop1" src="https://github.com/user-attachments/assets/4e1159e3-0171-45a8-a5b4-66d62ef9a322" />

## Features

- **Animated water droplet** that fills and empties based on water consumption
- **Color-coded usage ranges** (green for low, blue for medium, red for high)
- **Customizable thresholds** for usage ranges
- **Clean, modern design** with configurable styling
- **Responsive layout** that works on both desktop and mobile
- **Automatic updates** when water usage changes

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Water usage sensor

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `shutter.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own shutter/blind entity.

## Entity Requirements

The card expects a standard Home Assistant cover entity with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `sensor.water` | Any sensor entity that measures water |

## Customization Options

The card includes several customization options within the code:

### Position and Color Configuration

  - `minState` and `maxState`: Defines the range of values
  - `blockHighValue` and `blockMiddleValue`: Thresholds for color changes 
  - Color values for different states:
  - `color_green`: Color when not alot of water used (eco)
  - `color_red`: Color when normal use
  - `color_blue`: Color when overuse

## Advanced Usage

### Multiple Waterdrops Cards

To display multiple waterdrops on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different sensor
3. Consider using a grid layout to organize them in rows/columns


## Integration with Water Sensors

This card works with any sensor that provides water consumption data in liters. Common integrations include:

- Smart water meters
- Flow sensors
- Utility meter integrations
- Energy management systems

## Troubleshooting

If the card doesn't display correctly:

1. Check if the Button Card custom component is properly installed
2. Verify that your water usage sensor entity exists and provides numerical values
3. Make sure the water usage sensor has a state within the configured min/max range
4. Check the Home Assistant logs for any JavaScript errors

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
