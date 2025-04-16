# Ceiling Light Card for Home Assistant

A custom button card for Home Assistant that displays a visual representation of a hanging/ceiling lamp with real-time state, brightness, and color information.

<img width="125" alt="ceiling_light_100" src="https://github.com/user-attachments/assets/858e88ea-bb3d-4577-918b-929c31b1d83a" />

## Overview

This card creates a modern, stylized visual representation of a ceiling light that:
- Shows current on/off state with visual feedback
- Displays the actual brightness percentage when the light is on
- Changes color based on the light's color settings (RGB, HSL, or named colors)
- Features a light cone effect that shows the light's color and intensity
- Works with both light and switch entities
- Shows the entity name with proper formatting
- Adapts the glow and light cone intensity based on brightness level

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Light or switch entities

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `ceiling_light.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace `light.your_ceiling_light` with your own light or switch entity.

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

The card uses SVG (Scalable Vector Graphics) to create a stylized ceiling light visualization:

1. **Hanging Cord**: A simple line element connecting to the ceiling
2. **Lamp Shade**: A custom path shape with 3D effects and shadow
3. **Light Bulb**: A circle that glows and changes color when on
4. **Light Cone**: A downward cone showing the light beam when on
5. **Status Display**: Shows the current state (ON/OFF) and brightness
6. **Entity Name**: Shows the light's name in a clean, formatted way

### The SVG Architecture

The lamp visualization consists of several key SVG elements:

- **Hanging Cord**: Simple line element from ceiling to lamp
- **Lamp Shade**: Custom path with 3D filter effects for realism
- **Light Bulb**: Circle with gradient fills that change based on state
- **Light Cone**: Downward facing triangular path that appears when light is on
- **Text Elements**: Status, brightness, and entity name display

### Color Handling

The card can derive color information from multiple attributes:

1. **RGB Color**: If the entity provides RGB values
2. **HS Color**: If the entity uses Hue/Saturation format (converts to RGB)
3. **Named Color**: If the entity uses color names
4. **Default Color**: Falls back to a default yellow when no color info is available

### Animation Effects

The card includes subtle animation effects:
- Pulsing glow on the bulb when the light is on
- Light cone that pulses slightly when on
- Brightness-dependent glow and opacity
- 3D lighting effects on the lamp shade

## Customization Options

The card includes several customization variables within the code:

### Color Configuration
- `color_inactive`: Color when light is off (default: light gray)
- `color_active`: Uses entity color when on
- `lightBaseColor`: Color for the lamp body and cord

### Text Display
- `nameColor`: Color for text elements
- `displayName`: Visibility of the entity name
- `displayStatus`: Visibility of on/off status
- `fontSizeName`, `fontSizeDegrees`: Font size settings
- `fontWeight`: Text weight (default: bold)
- `textTransform`: Text case (default: uppercase)

### Light Effects
- `glowIntensity`: Calculated based on brightness
- Light cone opacity and size

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
    entity_id: light.your_ceiling_light
    brightness: 255  # Full brightness
```

### Custom Light Cone

You can adjust the light cone shape by modifying the path:

```javascript
// For a wider, shallower cone:
<path d="M110,120 L190,120 L230,150 L70,150 Z" 
      class="${state === 'on' ? 'light-cone-active' : 'light-cone'}" />
```

### Custom Colors and Effects

You can modify the default colors and effects:

```javascript
// Change these variables to customize effects
let lightBaseColor = '#eeeeee';  // Lighter lamp color
let glowIntensity = Math.max(10, 15 * (brightnessPercent / 100)); // Stronger glow
```

### Multiple Light Cards in Grid Layout

To display multiple ceiling lights in a grid:

```yaml
type: grid
columns: 3
square: false
cards:
  - type: custom:button-card
    entity: light.living_room_ceiling
    # Ceiling light card config...
  - type: custom:button-card
    entity: light.bedroom_ceiling
    # Ceiling light card config...
  - type: custom:button-card
    entity: light.kitchen_ceiling
    # Ceiling light card config...
```

## Troubleshooting

- **Light color not showing correctly**: Verify your entity provides color information in a standard format
- **Brightness not displaying**: Check if your entity has a brightness attribute (some switches won't have this)
- **Light cone not appearing**: Check the conditional class assignment for the light cone path
- **Name not displaying properly**: Verify the entity has a friendly_name attribute or adjust the wordLimit variable
- **SVG not scaling properly**: Check the container sizing and viewBox settings

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Home Assistant community for inspiration and support
