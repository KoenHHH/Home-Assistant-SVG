# Shutter/Blind Card for Home Assistant

A custom button card for Home Assistant that displays window shutters or blinds with a visual representation showing the current position.

<img width="125" alt="shutter" src="https://github.com/user-attachments/assets/fc9d26ed-a1c4-4c84-882f-9c680edc12e0" />

![shutter_down](https://github.com/user-attachments/assets/8391d396-c982-4f2d-a08d-d7d6ee89c02b)

![shutter_up](https://github.com/user-attachments/assets/4fb8d35c-2270-48c3-9c4b-fc381ca6840b)

## Overview

This card creates a visual representation of your window shutters or blinds that:
- Shows the current position with an animated shutter display
- Changes window background color based on position (lighter when open)
- Displays percentage open/closed
- Updates with a smooth animation when position changes (this only works if your entity has a position attribute, check your entity in home assistant developer tools)
- Shows the entity name below the visualization

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Cover entities (shutters, blinds, or roller covers)

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
| `cover.shutter` | Any cover entity that supports position (0-100%) |

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
  - `colorShutter`: Color of the shutter slats (default: dark grey-blue)

### Visual Configuration

- Text colors and visibility
- Font sizes and weights
- Animation speed (via `transitionDuration`)
- Window grid layout

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a window and shutter visualization:

1. **Window Frame**: White outline representing the window frame
2. **Window Background**: Color changes depending on how open the shutters are
3. **Shutter Representation**: Grey-blue overlay that covers part of the window based on position
4. **Visual Grid**: Window panes represented by grid lines
5. **Position Display**: Shows the precise percentage value
6. **Entity Name**: Displays in one or two lines below the visual

The JavaScript code:
- Retrieves the current position of the shutter
- Calculates the appropriate background color based on openness
- Determines the size of the shutter cover based on percentage
- Applies smooth transitions when position changes
- Formats and positions all elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the animation doesn't work smoothly, check that your entity reports position changes properly
- For shutters that use an inverted scale (0 = closed, 100 = open), adjust the minState and maxState values
- If the shutter cover looks wrong, verify that your entity's current_position attribute follows standard conventions
- Make sure your entity reports position as a number between 0-100

## Advanced Usage

### Multiple Shutter Cards

To display multiple shutters on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different shutter
3. Consider using a grid layout to organize them in rows/columns

### Adding Tap Actions

You can enhance the card with tap actions for controlling the shutters:

```yaml
tap_action:
  action: call-service
  service: cover.set_cover_position
  service_data:
    entity_id: cover.shutter
    position: 100  # Fully open position
```

### Custom Inverted Logic

Some shutter/blind systems use inverted position logic. If yours uses 0 for open and 100 for closed, adjust the min/max settings:

```
let minState = 0;    # For systems where 0 = closed
let maxState = 100;  # For systems where 100 = open
```

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
