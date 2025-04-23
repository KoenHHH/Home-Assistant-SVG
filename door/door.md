# Door Sensor Card for Home Assistant

A custom button card for Home Assistant that displays door sensors with a visual representation showing the current state (open or closed).

## Overview

This card creates a visual representation of your door that:
- Shows the current state with an animated door display
- Animates the door opening and closing based on sensor state
- Updates with a smooth transition when the door state changes
- Displays the door state (OPEN/CLOSED) prominently
- Shows the entity name below the visualization

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Binary sensor for door contact (any door sensor that reports open/closed or on/off)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `door.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own door sensor entity.

## Entity Requirements

The card expects a standard Home Assistant binary sensor entity with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `binary_sensor.door_sensor_contact` | Any binary sensor that reports open/closed or on/off state |

The card works with entities that provide:
- Standard binary sensor states (on/off, open/closed)

## Customization Options

The card includes several customization options within the code:

### Color Configuration

- `color_open`: Color for the door when open (default: blue-grey #506587)
- `color_closed`: Color for the door when closed (default: blue-grey #506587)
- `colorFrame`: Color of the door frame (default: white)
- `doorColor`: Base color of the door (default: blue-grey #506587)
- `nameColor`: Color of the entity name text (default: white)

### Visual Configuration

- `fontSizeState`: Size of the state text (default: 32px)
- `fontSizeName`: Size of the entity name text (default: 32px)
- `fontWeight`: Font weight for text elements (default: bold)
- `textTransform`: Text transformation (default: uppercase)
- `transitionDuration`: Animation speed for state changes (default: 0.6s)
- `displayName1`, `displayName2`, `displayState`: Visibility options for text elements

### Name Display Configuration

- `wordLimit`: Number of words to display on the first line (default: 2)

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a door visualization:

1. **Door Frame**: Light blue rectangle with white outline
2. **Door**: Dynamic path that changes position based on state (open or closed)
3. **Door Handle**: White circle that moves with the door
4. **State Display**: Shows OPEN or CLOSED text based on the current state
5. **Entity Name**: Displays in one or two lines below the visual

The JavaScript code:
- Retrieves the current state of the door sensor
- Determines if the door is open based on the state value
- Selects the appropriate door path and handle position based on door state
- Formats the entity name into two lines (if needed)
- Applies smooth transitions when state changes
- Returns the SVG code which is rendered by Home Assistant

## SVG Door Animation

The door animation is created through these SVG elements:
- A fixed door frame that stays in place
- A door path that uses different coordinates for open and closed states:
  - Closed: Rectangle positioned within the frame
  - Open: Angled quadrilateral showing the door opened outward
- A door handle that moves position with the door
- All moving elements have the "door-element" class that enables smooth transitions

## Advanced Usage

### Multiple Door Cards

To display multiple door sensors on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different door sensor
3. Consider using a grid layout to organize them in rows/columns

### Adding Tap Actions

You can enhance the card with tap actions to show more information:

```yaml
tap_action:
  action: more-info
```

Or to navigate to a specific view:

```yaml
tap_action:
  action: navigate
  navigation_path: /lovelace/door_view
```

## Troubleshooting

- If the animation doesn't work smoothly, check that your entity reports state changes properly
- If the door visualization looks incorrect, verify that your entity uses standard state conventions (on/off or open/closed)
- For entities with non-standard naming, the automatic name parsing may need adjustment
- Make sure your entity correctly reports open/closed states in Home Assistant

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
