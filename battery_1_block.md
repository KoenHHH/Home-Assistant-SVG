# Battery State of Charge (SoC) Card for Home Assistant

A custom, visually appealing battery indicator card for Home Assistant that displays battery percentage with dynamic coloring and filling based on charge level.

<img width="125" alt="battery" src="https://github.com/user-attachments/assets/55582039-ad6c-4f2c-a361-22b881e2ee5d" />

## Overview

This card creates a battery icon that:
- Shows the current battery percentage
- Fills proportionally to the battery level
- Changes color based on configurable thresholds
- Displays the entity name below the battery
- Updates dynamically as the battery level changes

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- A battery level sensor that reports percentage (0-100)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Go to your dashboard, enter edit mode, and add a new card.

3. Choose "Manual" card and paste the YAML configuration from battery_1_block.yaml.

4. Replace `sensor.battery_soc` with your actual battery level sensor.

## Customization Options

The card includes several customization options. Here are the key parameters you can modify:

### Entity Configuration

- `entity`: Your battery level sensor (must report a percentage from 0-100)
- `entity_id`: Should match the entity value

### Threshold Configuration

- `blockHighValue`: Above this percentage, the battery shows as green (default: 70)
- `blockMiddleValue`: Between high and this value, the battery shows as orange (default: 30)
- Below the middle value, the battery shows as red

### Color Configuration

- `color_green`: Color for high battery level (default: #4caf50)
- `color_orange`: Color for medium battery level (default: #ff9800)
- `color_red`: Color for low battery level (default: #f44336)
- `colorPercentage`: Color of the percentage text (default: same as battery fill color)
- `colorName`: Color of the entity name text (default: white)

### Visual Configuration

- `rotateSVG`: Rotation of the battery (default: 0deg for vertical)
- `fontSizePercentage`: Font size for the percentage display (default: 32px)
- `fontSizeName`: Font size for the entity name (default: 32px)
- `fontWeight`: Font weight for text (default: bold)
- `textTransform`: Text transformation (default: uppercase)
- `displayName`: Show/hide the entity name (default: visible)
- `displayPercentage`: Show/hide the percentage (default: visible)
- `wordLimit`: Number of words on the first line for entity name (default: 1)

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a dynamic battery visualization:

1. **Battery Container**: A rectangular outline represents the battery casing
2. **Battery Connector**: A small rectangle at the top represents the battery terminal
3. **Battery Fill**: A dynamically sized rectangle that fills from bottom to top based on percentage
4. **Text Elements**: Displays the percentage and entity name

The JavaScript code:
- Retrieves the current state of the battery sensor
- Calculates the appropriate color based on thresholds
- Determines the size of the battery fill based on percentage
- Formats and positions all elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the card doesn't appear correctly, ensure your battery sensor is properly reporting a numeric value between 0-100
- Check that the entity ID is correct and accessible
- Verify that button-card is properly installed
- If the text appears cut off, adjust the `fontSizePercentage` and `fontSizeName` values

## Advanced Usage

### Multiple Battery Cards

To display multiple batteries on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different battery sensor
3. Consider adjusting sizes or adding a grid layout to organize them

### Horizontal Battery

To display the battery horizontally:

1. Change `rotateSVG` to `90deg`
2. You may need to adjust the viewBox attributes of the SVG for proper sizing

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Inspired by various battery visualizations in the Home Assistant community
- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
