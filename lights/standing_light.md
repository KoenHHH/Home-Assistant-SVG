# Standing Light Card for Home Assistant

A custom button card for Home Assistant that displays a visual representation of a standing lamp with real-time state, brightness, and color information.

<img width="125" alt="standing_light_100_green" src="https://github.com/user-attachments/assets/babf753c-22be-4ef2-bea3-84dea4240ddf" />

<img width="125" alt="standing_light_50" src="https://github.com/user-attachments/assets/50f58242-0fe8-4496-919f-8e3e779377f8" />

<img width="125" alt="standing_light_100_red" src="https://github.com/user-attachments/assets/4ef75740-bf05-42b5-9be7-8f43c3e126b6" />

<img width="125" alt="standing_light_off" src="https://github.com/user-attachments/assets/2ffb0325-1bbd-4aea-b662-ac8f399f7568" />

## Overview

This card creates a modern, minimalist visual representation of a standing light that:
- Shows current on/off state with proper visual feedback
- Displays the actual brightness percentage when the light is on
- Changes color based on the light's color settings (RGB, HSL, or named colors)
- Features a glowing effect that changes intensity based on brightness
- Works with both light and switch entities
- Shows the entity name with proper formatting
- Adapts the glow intensity based on brightness level

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Light or switch entities

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `standing_light.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace `light.your_light_entity` with your own light or switch entity.

## Entity Requirements

The card is compatible with:

| Entity Type | Support Level |
|-------------|---------------|
| `light.entity` | Full support (state, brightness, color) |
| `switch.entity` | Basic support (on/off only) |

For full functionality, the card works best with entities that provide:
- State information (on/off)
- Brightness attribute (0-255)
- Color information (RGB, HS, or named colors)

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a stylized standing lamp visualization:

1. **Lamp Base**: A simple rectangular base at the bottom
2. **Lamp Body**: A U-shaped standing arm with gradient shading for depth
3. **Light Strip**: An inner path that changes color and glows when on
4. **Status Display**: Shows the current state (ON/OFF)
5. **Brightness Display**: Shows the percentage brightness when on
6. **Entity Name**: Shows the light's name in a clean, formatted way

### The SVG Architecture

The lamp visualization consists of several key SVG elements:

- **Base**: Simple rectangular element with gradient fill
- **Outer Structure**: U-shaped path with gradient stroke
- **Inner Light**: Path that follows the outer structure but changes color and opacity based on light state
- **Glow Effect**: SVG filter that creates a halo effect when the light is on
- **Text Elements**: Status, brightness, and entity name display

### Color Handling

The card can derive color information from multiple attributes:

1. **RGB Color**: If the entity provides RGB values
2. **HS Color**: If the entity uses Hue/Saturation format (converts to RGB)
3. **Named Color**: If the entity uses color names
4. **Default Color**: Falls back to a default yellow when no color info is available

### Animation Effects

The card includes subtle animation effects:
- Pulsing glow when the light is on
- Brightness-dependent glow intensity
- Smooth opacity transitions

## Customization Options

The card includes several customization variables within the code:

### Color Configuration
- `color_inactive`: Color when light is off (default: light gray)
- `color_active`: Uses entity color when on
- `metalBaseColor`: Color for the lamp base
- `lampBodyColor`: Color for the lamp structure

### Text Display
- `nameColor`: Color for text elements
- `displayName`: Visibility of the name
- `displayStatus`: Visibility of on/off status
- `displayBrightness`: Visibility of brightness percentage
- `fontSizeName`, `fontSizeStatus`, `fontSizeDegrees`: Font size settings
- `fontWeight`: Text weight (default: bold)
- `textTransform`: Text case (default: uppercase)

### Glow Effects
- `glowIntensity`: Calculated based on brightness

## Advanced Usage

### Adding Tap Actions

You can enhance the card with tap actions for controlling the light:

```yaml
tap_action:
  action: toggle
  
double_tap_action:
  action: call-service
  service: light.turn_on
  service_data:
    entity_id: light.your_light_entity
    brightness: 255  # Full brightness
```

### Custom Color Configurations

You can modify the default colors by editing the relevant variables in the card's code:

```javascript
// Change these variables to customize colors
let color_inactive = '#d0d0d0';  // Lighter gray when off
let metalBaseColor = '#333333';  // Darker base
```

### Customizing Brightness Display

If you prefer a different way to show brightness:

```javascript
// To change percentage to a 0-10 scale
let brightnessDisplay = Math.round((brightness / 255) * 10);
// Then update the text element to show:
${brightnessDisplay}/10
```

### Multiple Light Cards in Grid Layout

To display multiple lights in a grid:

```yaml
type: grid
columns: 3
square: false
cards:
  - type: custom:button-card
    entity: light.living_room
    # Standing light card config...
  - type: custom:button-card
    entity: light.bedroom
    # Standing light card config...
  - type: custom:button-card
    entity: light.kitchen
    # Standing light card config...
```

## Troubleshooting

- **Light color not showing correctly**: Verify your entity provides color information in a standard format
- **Brightness not displaying**: Check if your entity has a brightness attribute (some switches won't have this)
- **Name not displaying properly**: Verify the entity has a friendly_name attribute or adjust the wordLimit variable
- **SVG not scaling properly**: Check the container sizing and viewBox settings

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
