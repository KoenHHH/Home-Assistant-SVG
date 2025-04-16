# Window Card for Home Assistant

A custom button card for Home Assistant that displays windows with a visual representation showing the current state (open or closed).

<img width="125" alt="window_open" src="https://github.com/user-attachments/assets/7f8a504d-ef8e-43a8-8f95-abef27f5e16d" />

<img width="125" alt="window_closed" src="https://github.com/user-attachments/assets/2f457ae6-1771-43c7-899c-972cf46b6d5e" />

## Overview

This card creates a visual representation of your windows that:
- Shows the current state with an animated window display
- Animates the entire window when opening/closing based on contact sensor state
- Updates with a smooth animation when state changes
- Shows the entity name below the visualization
- Displays OPEN/CLOSED status text

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Binary sensor entities (window/door contact sensors)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `window.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own window contact sensor entity.

## Entity Requirements

The card expects a standard Home Assistant binary sensor entity with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `binary_sensor.window_sensor_contact` | Any binary sensor reporting window/door state (open/closed) |

The card works with standard binary sensors that report:
- State as "on"/"off" or "open"/"closed"

## Customization Options

The card includes several customization options within the code:

### Color Configuration

- `color_open`: Color of window panes when open (default: #506587)
- `color_closed`: Color of window panes when closed (default: none - transparent)
- `windowColor`: Background color of the window (default: #b3e5fc - light blue)
- `colorFrame`: Color of the window frame (default: white)
- `nameColor`: Color of entity name text (default: white)

### Visual Configuration

- Text colors and visibility
- Font sizes and weights
- Animation speed (via `transitionDuration`)
- Window grid layout
- Word limit for name splitting
- Rotation angle for open window animation

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a window visualization:

1. **Window Frame**: White outline representing the window frame
2. **Window Background**: Light blue background representing the window
3. **Animated Window**: The window rotates on its axis when opening/closing
4. **Visual Grid**: Window panes represented by grid lines
5. **State Display**: Shows "OPEN" or "CLOSED" text
6. **Entity Name**: Displays in one or two lines below the visual

The JavaScript code:
- Retrieves the current state of the window sensor
- Applies rotation transformations to create an opening animation
- Formats and positions all elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the animation doesn't work smoothly, check that your entity reports state changes properly
- Make sure your entity has the correct state attributes ('on'/'off' or 'open'/'closed')
- If the window looks wrong, verify that your entity follows standard conventions
- For entities with different naming patterns, adjust the name formatting code

## Advanced Usage

### Multiple Window Cards

To display multiple windows on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different window sensor
3. Consider using a grid layout to organize them in rows/columns

### Adding Tap Actions

You can enhance the card with tap actions for displaying more information:

```yaml
tap_action:
  action: more-info
```

### Customizing Animation

You can adjust the animation properties for different effects:

```
let leftWindowRotation = isOpen ? 'transform: rotateY(-30deg); transform-origin: left;' : '';
let rightWindowRotation = isOpen ? 'transform: rotateY(30deg); transform-origin: right;' : '';
let transitionDuration = "1.0s";  // Slower animation
```

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
