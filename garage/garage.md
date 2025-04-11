# Garage Door Cover Card for Home Assistant

A custom button card for Home Assistant that displays garage doors with a visual representation showing the current position.

for images see `shutter.md`

## Overview

This card creates a visual representation of your garage door that:
- Shows the current position with an animated garage door display
- Changes background color based on position (lighter when open)
- Displays status text (open, closed, opening, closing)
- Updates with a smooth animation when position changes
- Shows the entity name below the visualization

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Cover entities (garage doors)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `garage.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own garage door entity.

## Entity Requirements

The card expects a standard Home Assistant cover entity with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `cover.garage` | Any garage door cover entity that supports position (0-100%) |

The card will work with entities that provide:
- A `current_position` attribute (0-100%)
- OR at minimum the standard cover states (open/closed)

## Customization Options

The card includes several customization options within the code:

### Position and Color Configuration

  - `minState` and `maxState`: Defines the range of values
  - `blockHighValue` and `blockMiddleValue`: Thresholds for color changes (defaults to 70 and 20)
  - Color values for different states:
  - `color_light`: Color when mostly open (default: light blue)
  - `color_day`: Color when partially open (default: medium blue)
  - `color_dark`: Color when mostly closed (default: dark blue)
  - `colorShutter`: Color of the garage door (default: dark grey-blue)

### Visual Configuration

- Text colors and visibility
- Font sizes and weights
- Animation speed (via `transitionDuration`)
- Garage door layout

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a garage door visualization:

1. **Garage Structure**: White outline representing the garage structure with roof and walls
2. **Garage Door Opening**: Color changes depending on how open the door is
3. **Garage Door Representation**: Grey-blue overlay that covers part of the opening based on position
4. **Status Display**: Shows the current state (open, closed, opening, closing)
5. **Entity Name**: Displays in one or two lines below the visual

The JavaScript code:
- Retrieves the current position of the garage door
- Calculates the appropriate background color based on openness
- Determines the coverage of the garage door based on percentage
- Applies smooth transitions when position changes
- Formats and positions all elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the animation doesn't work smoothly, check that your entity reports position changes properly
- For garage doors that use an inverted scale (0 = closed, 100 = open), adjust the minState and maxState values
- If the garage door looks wrong, verify that your entity's current_position attribute follows standard conventions
- Make sure your entity reports position as a number between 0-100

## Advanced Usage

### Multiple Garage Door Cards

To display multiple garage doors on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different garage door
3. Consider using a grid layout to organize them in rows/columns

### Adding Tap Actions

You can enhance the card with tap actions for controlling the garage door:

```yaml
tap_action:
  action: call-service
  service: cover.toggle
  service_data:
    entity_id: cover.garage
```

### Custom Inverted Logic

Some garage door systems use inverted position logic. If yours uses 0 for open and 100 for closed, adjust the min/max settings:

```
let minState = 0;    # For systems where 0 = open
let maxState = 100;  # For systems where 100 = closed
```

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
