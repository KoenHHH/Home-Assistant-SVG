# Air Purifier Card for Home Assistant

A custom button card for Home Assistant that displays an air purifier with a visual representation showing the current state, fan speed, and air quality metrics.

![purifier](https://github.com/user-attachments/assets/03accde1-1e3d-492a-b2f7-55e06b5538c3)

## Overview

This card creates a visual representation of your air purifier that:
- Shows the current power state (on/off) with a color change
- Displays PM2.5 measurement values with color coding based on air quality
- Shows fan speed indicators with illuminated LEDs based on current fan level
- Features animated airflow lines when the purifier is running
- Displays the entity name below the visualization

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Fan entities (air purifiers with appropriate attributes)
- Optional: Dedicated sensors for PM2.5 and air quality

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `air_purifier.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity ID with your own air purifier entity.

## Entity Requirements

The card works best with the following entity types:

| Entity Type | Purpose |
|-------------|---------|
| `fan.air_purifier` | Main air purifier entity (required) |
| `sensor.air_purifier_pm25` | PM2.5 measurement sensor (optional) |
| `sensor.air_purifier_air_quality` | Air quality status sensor (optional) |

The card will automatically check for:
1. The main fan entity's state (on/off)
2. Fan speed/percentage from entity attributes
3. PM2.5 values from either a dedicated sensor or from the main entity's attributes
4. Air quality status from either a dedicated sensor or from the main entity's attributes

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a dynamic air purifier visualization:

### SVG Components

1. **Air Purifier Body**: The main housing of the device with a subtle gradient
2. **Control Panel**: A darker section at the top of the purifier
3. **Status LEDs**: Three illuminated indicators that show current fan speed
4. **Filter Section**: A white rectangular area representing the filter
5. **Airflow Lines**: Animated lines that show air movement when the device is on
6. **PM2.5 Display**: Shows the current particulate matter reading with appropriate color coding
7. **Device Name**: Shows the entity's friendly name below the visualization

### Dynamic Elements

- **LED Indicators**: Light up based on fan speed level (1-3)
- **Airflow Animation**: Vertical lines animate when the purifier is on
- **PM2.5 Color Coding**:
  - Green: Good air quality (PM2.5 ≤ 15)
  - Yellow: Moderate air quality (PM2.5 between 15-35)
  - Orange: Unhealthy air quality (PM2.5 between 35-50)
  - Red: Very unhealthy air quality (PM2.5 > 50)
- **Power Status**: Changes color scheme when turned off

### Technical Implementation

The JavaScript code:
- Retrieves the current state and attributes of the air purifier
- Calculates appropriate colors based on air quality readings
- Determines LED status based on fan speed/percentage
- Animates airflow lines when the device is running
- Formats and positions all SVG elements
- Returns the SVG code which is rendered by Home Assistant

## Customization Options

The card includes several customization options within the code:

### Color Configuration
- `purifierBaseColor`: Color of the purifier body (default: light gray)
- `purifierBorderColor`: Color of the device outline (default: dark gray)
- `statusColor`: Color when device is on (default: green)
- Color thresholds for PM2.5 readings (adjustable based on local air quality standards)

### Visual Configuration
- Font sizes for various text elements
- Visibility options for different components
- Word limit for multi-line display of entity names

### Animation Settings
- Animation speed via CSS keyframes
- Staggered animation delays for a more natural flow effect

## Troubleshooting

- If PM2.5 values aren't showing, check that your entity provides this data or create a separate sensor
- For air purifiers with different fan speed scales, adjust the `speedToUse` calculation
- If the animation doesn't work, verify that your entity state changes are correctly detected
- For custom air quality terminology, adjust the condition checks in the air quality color calculations

## Advanced Usage

### Adding Tap Actions

You can enhance the card with tap actions for controlling the air purifier:

```yaml
tap_action:
  action: toggle
  entity: fan.air_purifier
```

Or for more complex control:

```yaml
tap_action:
  action: call-service
  service: fan.turn_on
  service_data:
    entity_id: fan.air_purifier
    percentage: 66  # Medium speed
```

### Multiple Air Purifier Cards

To display multiple air purifiers on your dashboard:

1. Copy the card configuration multiple times
2. Change the entity for each card to point to different air purifiers
3. Consider using a grid layout to organize them in rows/columns

### Showing Air Quality Text

To display the text description of air quality (good, moderate, etc.):

1. Change `displayAirQuality` from `'none'` to `'visible'`

### Custom PM2.5 Threshold Values

To adjust the PM2.5 thresholds for your local air quality standards:

```javascript
// Modify these values based on your local standards
if (air_quality === 'poor' || air_quality === 'very_poor' || pm25 > 75) {
  pm25Color = '#ff0000';  // Red (very unhealthy) - adjusted threshold
} else if (air_quality === 'fair' || pm25 > 50) {
  pm25Color = '#ff9900';  // Orange (unhealthy) - adjusted threshold
} else if (air_quality === 'moderate' || pm25 > 25) {
  pm25Color = '#ffcc00';  // Yellow (moderate) - adjusted threshold
}
```

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
