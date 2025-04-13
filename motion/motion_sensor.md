# Motion Sensor Card for Home Assistant

A custom button card for Home Assistant that displays motion sensors with a visually appealing 3D representation that changes appearance based on motion detection state.

![motion](https://github.com/user-attachments/assets/332c1079-e13a-48ce-a39e-088c95f71122)

## Overview

This card creates a visual representation of your motion sensor that:
- Shows the current state with a color-changing dome visualization
- Applies a blinking animation effect when motion is detected
- Displays "detected" or "not detected" status text
- Uses 3D effects and gradients for a modern, realistic appearance
- Shows the entity name below the visualization in a customizable format

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Binary sensor entities (motion sensors)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `motion_sensor.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own motion sensor entity.

## Entity Requirements

The card expects a standard Home Assistant binary sensor entity with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `binary_sensor.motion_sensor` | Any binary sensor that reports motion (on/off states) |

The card will work with any binary sensor that provides:
- Standard binary states (on/off)
- Optional friendly_name attribute (for display purposes)

## Customization Options

The card includes several customization options within the code:

### Visual Configuration

- `divDisplay`, `widthSVG`, `heightSVG`, `paddingDIV`: Layout configuration
- `fontSizeMotion`, `fontSizeName`, `fontWeight`, `textTransform`: Text styling
- `color_inactive`, `color_active`, `sensorBaseColor`: Color scheme
- `nameColor`, `displayName1`, `displayName2`, `displayStatus`: Text visibility options
- `wordLimit`: Controls how entity names are split for multi-line display

### Color Configuration

- `color_inactive`: Light gray color when no motion is detected (default: #f0f0f0)
- `color_active`: Red color when motion is detected (default: #f44336)
- `sensorBaseColor`: Base color of the sensor body (default: #e0e0e0)

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a realistic motion sensor visualization:

1. **Sensor Base**: Rectangular base with rounded corners
2. **Dome Housing**: A circular dome that changes color based on sensor state
3. **3D Effects**: Applied using SVG filters for shadows, highlights, and gradients
4. **Animation**: Blinking effect activates when motion is detected
5. **Status Display**: Shows "detected" or "not detected" text
6. **Entity Name**: Displays in one or two lines below the visualization

The JavaScript code:
- Retrieves the current state of the motion sensor
- Applies the appropriate styling and animation based on state
- Formats the entity name into multiple lines if needed
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the animation doesn't work smoothly, check your browser's SVG animation support
- If the entity name display looks strange, verify that your entity has a proper friendly_name attribute
- For performance issues, try reducing the complexity of SVG filters
- Make sure your entity follows standard binary sensor conventions (on = active, off = inactive)

## Advanced Usage

### Multiple Motion Sensor Cards

To display multiple motion sensors on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different motion sensor
3. Consider using a grid layout to organize them in rows/columns

### Adding Tap Actions

You can enhance the card with tap actions for additional functionality:

```yaml
tap_action:
  action: more-info
  entity: binary_sensor.motion_sensor
```

### Customizing SVG Effects

The card uses advanced SVG filters and gradients that can be modified for different visual effects:

- Modify the `dome3D` filter parameters to change the 3D effect
- Adjust the gradient stops in `activeGradient` and `inactiveGradient` for different color transitions
- Change the animation keyframes to create different motion effects

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
