# Digital Clock Card for Home Assistant

A custom button card for Home Assistant that displays a sleek 7-segment LED digital clock showing the current time based on the `sensor.time` entity with timezone support.

<img width="125" alt="digitalclock1" src="https://github.com/user-attachments/assets/e65758a6-17e0-4d1c-8f9d-10f5665d1f86" />

<img width="125" alt="digitalclock2" src="https://github.com/user-attachments/assets/d359372c-fcb4-47d6-b66e-2f74c9a31a0e" />

## Overview

This card creates a realistic 7-segment LED digital clock that:
- Shows the current time with hour, minute format (HH:MM)
- Supports both 12-hour and 24-hour time formats
- Features realistic LED-style display with active and dimmed segments
- Shows timezone information
- Updates automatically with the Home Assistant time entity
- Features clean black background with red LED segments

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- `sensor.time` entity (automatically available in Home Assistant)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `digital-clock.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. If desired, adjust the timezone variable in the code to match your location.

## Entity Requirements

The card primarily works with the built-in Home Assistant time sensor:

| Entity Type | Purpose |
|-------------|---------|
| `sensor.time` | Provides the current time in format HH:MM |

## Customization Options

The card includes several customization options within the code:

### Time Configuration

- `timezone`: Set your timezone (default: "Europe/London")
- `use_24h_format`: Toggle between 12-hour and 24-hour format (default: false for 12-hour)

### Color Configuration

- `backgroundColor`: Background color of the clock (default: black)
- `digitColor`: Color of active LED segments (default: #ff0000 red)
- `dimmedColor`: Color of inactive LED segments (default: #330000 dark red)
- `textColor`: Color of the timezone text (default: white)

### Visual Configuration

- `fontSizeTimezone`: Size of the timezone text (default: 32px)
- `fontWeight`: Font weight for text elements (default: bold)
- `textTransform`: Text transformation for text elements (default: uppercase)
- `digitWidth`: Width of each digit (default: 40)
- `digitHeight`: Height of each digit (default: 75)
- `digitSpacing`: Spacing between digits (default: 10)
- `segmentThickness`: Thickness of LED segments (default: 8)

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a realistic 7-segment LED digital clock:

1. **Background Rectangle**: A black background for the display
2. **7-Segment Digits**: Each digit is composed of 7 segments (labeled a-g)
3. **Active Segments**: Segments lit in bright red for the current time
4. **Inactive Segments**: Segments dimmed in dark red when not in use
5. **Colon Separator**: Separates hours and minutes
6. **Timezone Display**: Shows the configured timezone below the clock

The JavaScript code:
- Retrieves the current time from the `sensor.time` entity
- Formats the time according to the selected 12/24 hour format
- Determines which segments should be active for each digit
- Renders each segment as a polygon with proper angled joints for a realistic LED look
- Special handling for the digit "1" to ensure consistent appearance
- Updates automatically when the time changes
- Returns the SVG code which is rendered by Home Assistant

## SVG Digit Rendering

The digital clock uses a true 7-segment display technique:
- Each digit is composed of 7 polygons (labeled a-g)
- The segments use angled 45-degree corners for a realistic LED appearance
- Segment states are defined for each possible digit (0-9)
- Active segments are shown in bright red, inactive in dark red
- The number "1" receives special treatment to maintain visual balance

## Advanced Usage

### Customizing the Clock Size

You can adjust the size of the clock by:
1. Modifying the `digitWidth` and `digitHeight` variables
2. Adjusting the `segmentThickness` for thicker or thinner segments
3. Changing the SVG viewBox dimensions for overall scaling

### Customizing the LED Colors

To change the LED appearance:

```javascript
// Blue LED display
let backgroundColor = 'black';
let digitColor = '#3399ff';      // Bright blue
let dimmedColor = '#0c2d4d';     // Dark blue

// Green LED display
let backgroundColor = 'black';
let digitColor = '#33ff33';      // Bright green
let dimmedColor = '#0c4d0c';     // Dark green

// Amber LED display (classic calculator look)
let backgroundColor = 'black';
let digitColor = '#ffaa00';      // Amber
let dimmedColor = '#4d3300';     // Dark amber
```

### Multiple Time Zones

To display multiple clocks with different time zones:

1. Copy the card configuration multiple times
2. Change the timezone variable for each instance
3. Consider using a grid layout to organize them in rows/columns

## Troubleshooting

- If the clock digits don't appear correctly, ensure your time entity is reporting in the expected format
- For time zone issues, verify that the timezone string is valid (e.g., "America/New_York", "Europe/London")
- If digits appear misaligned, check that the `rectX`, `rectY`, `rectWidth`, and `rectHeight` values are appropriate for your layout
- For the number "1", special rendering is used to maintain visual balance with other digits

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
