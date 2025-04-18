# Smoke Detector Card for Home Assistant

A custom button card for Home Assistant that displays smoke detectors with a realistic visual representation showing the current state and battery level.

![smoke](https://github.com/user-attachments/assets/872fbe9e-81f9-474d-97ce-ba7050b43865)

<img width="125" alt="smoke" src="https://github.com/user-attachments/assets/7ee3af61-28c4-47a0-a6f0-f9b418f3a280" />

## Overview

This card creates a visual representation of your smoke detector that:
- Shows the current state with a realistic smoke detector display
- Displays animated smoke effects when smoke is detected
- Shows battery status with color-coded LED indicator (green/orange/red)
- Updates instantly when smoke is detected or battery level changes
- Shows the entity name below the visualization

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Binary sensor entities for smoke detection
- Sensor entities for battery level

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `smoke.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own smoke detector entity.

## Entity Requirements

The card expects standard Home Assistant entities with these characteristics:

| Entity Type | Purpose |
|-------------|---------|
| `binary_sensor.smoke_detector` | Smoke detection state (on = smoke detected, off = no smoke) |
| `sensor.smoke_detector_battery` | Battery level as a percentage (0-100%) |

## Customization Options

The card includes several customization options within the code:

### Color Configuration

- `color_inactive`: Color when no smoke is detected (default: light gray)
- `color_active`: Color when smoke is detected (default: orange)
- `batteryColor`: Dynamically changes based on battery level:
  - Green: 70-100%
  - Orange: 30-69%
  - Red: 0-29%

### Visual Configuration

- Text colors and visibility
- Font sizes and weights
- Animation speed for smoke effects
- Smoke particle density and movement patterns

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a smoke detector visualization:

1. **Base Plate**: Circular base with subtle 3D effect
2. **Central Dome**: Changes color and pulses when smoke is detected
3. **Battery LED**: Color-coded indicator for battery status
4. **Ventilation Lines**: Decorative elements for realism
5. **Animated Effects**:
   - Spinning light rays when smoke is detected
   - Floating and drifting smoke particles
   - Semi-transparent smoke overlay
6. **Status Display**: Shows "detected" or "not detected"
7. **Entity Name**: Displays in one or two lines below the visual
8. **Battery Percentage**: Shows current battery level in the corner

The JavaScript code:
- Retrieves the current state of the smoke detector
- Checks the battery level and determines appropriate indicator color
- Creates and animates smoke particles when smoke is detected
- Formats and positions all visual elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If the battery indicator doesn't work, check that your battery entity is properly named or adjust the code to point to the correct entity
- If animations seem choppy, try reducing the number of smoke particles or animation complexity
- For smoke detectors that don't have a battery sensor, you can remove those elements from the code
- If the card doesn't update when smoke is detected, verify that your entity is reporting state changes properly

## Advanced Usage

### Multiple Smoke Detector Cards

To display multiple smoke detectors on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to a different smoke detector
3. Consider using a grid layout to organize them in rows/columns

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
