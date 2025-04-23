# Analog Clock Card for Home Assistant

A custom button card for Home Assistant that displays a beautiful analog wall clock showing the current time based on the `sensor.time` entity with timezone support.

<img width="125" alt="clock" src="https://github.com/user-attachments/assets/15adeda4-37a7-472c-baf5-fccf9cf0dbc5" />

## Overview

This card creates a visual representation of an analog clock that:
- Shows the current time with hour, minute (HH:MM)
- Updates with smooth animations as time changes
- Displays hour markers and numbers for easy reading
- Shows digital time display below the analog clock face
- Includes timezone information
- Updates automatically with the Home Assistant time entity

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- `sensor.time` entity (automatically available in Home Assistant)

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `clock.yaml` to your configuration.

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
- Time format automatically displays as 12-hour with AM/PM

### Color Configuration

- `clockFaceColor`: Background color of the clock face (default: blue-grey #506587)
- `clockBorderColor`: Color of the clock rim (default: white)
- `hourHandColor`: Color of the hour hand (default: white)
- `minuteHandColor`: Color of the minute hand (default: white)
- `markerColor`: Color of hour markers and numbers (default: white)
- `textColor`: Color of the digital time and name text (default: white)

### Visual Configuration

- `fontSizeTime`: Size of the digital time display (default: 20px)
- `fontSizeName`: Size of the entity name (default: 16px)
- `fontSizeTimezone`: Size of the timezone text (default: 14px)
- `fontWeight`: Font weight for text elements (default: bold)
- `textTransform`: Text transformation for text elements (default: uppercase)
- `transitionDuration`: Animation speed for clock hands (default: 0.5s)
- `clockRadius`: Size of the clock face (default: 100)

### Clock Hand Configuration

- `hourHandLength`: Length of hour hand as percentage of radius (default: 50%)
- `minuteHandLength`: Length of minute hand as percentage of radius (default: 70%)

## How It Works

The card uses SVG (Scalable Vector Graphics) to create an interactive analog clock:

1. **Clock Face**: A circular background with border
2. **Hour Markers**: Lines at each hour position (longer at 12, 3, 6, and 9)
3. **Hour Numbers**: Numeric labels from 1-12 around the face
4. **Clock Hands**: Three hands (hour, minute, second) rotating from the center
5. **Center Pivot**: A small circle in the center where hands meet
6. **Digital Display**: Shows the time in digital format below the analog clock
7. **Entity Name & Timezone**: Shows the entity name and timezone at the bottom

The JavaScript code:
- Retrieves the current time from the `sensor.time` entity
- Calculates the correct angles for each clock hand based on the time
- Generates hour markers and numbers around the clock face
- Applies smooth CSS transitions for hand movements
- Updates automatically when the time changes
- Returns the SVG code which is rendered by Home Assistant

## SVG Clock Animation

The clock animation is created through these techniques:
- CSS transform rotation is applied to each hand based on the time
- The transform-origin is set to the center of the clock
- Different transition styles are used for each hand:
  - Hour and minute hands use smooth cubic-bezier transitions
  - Second hand uses a step transition for more realistic ticking
- All hands rotate around the central pivot point

## Advanced Usage

### Customizing the Clock Size

The clock is designed to be responsive. You can adjust the size by:
1. Modifying the `clockRadius` variable
2. Adjusting the SVG viewBox dimensions
3. Using the aspect-ratio style to maintain a perfect circle

### Multiple Time Zones

To display multiple clocks with different time zones:

1. Copy the card configuration multiple times
2. Change the timezone variable for each instance
3. Update the entity name to reflect the timezone shown
4. Consider using a grid layout to organize them in rows/columns

### Adding Color Themes

You can customize the colors to match your Home Assistant theme:

```
// Light theme
let clockFaceColor = '#FFFFFF';
let clockBorderColor = '#4CAF50';
let hourHandColor = '#212121';

// Dark theme
let clockFaceColor = '#121212';
let clockBorderColor = '#BB86FC';
let hourHandColor = '#EEEEEE';
```

## Troubleshooting

- If the clock hands don't align correctly, check that your time entity is reporting in the expected format
- For time zone issues, verify that the timezone string is valid
- If animations don't work smoothly, try adjusting the transition duration and timing function
- For devices with lower performance, consider disabling the second hand by setting its stroke to "transparent"

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
