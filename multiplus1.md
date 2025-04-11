# MultiPlus Card for Home Assistant

A custom button card for Home Assistant that displays Victron MultiPlus inverter/charger status with an intuitive interface that mimics the physical device appearance.

<img width="125" alt="multiplus" src="https://github.com/user-attachments/assets/f4027318-05a5-4982-93cf-f3072fe24f06" />

## Overview

This card creates a visual representation of your Victron MultiPlus inverter/charger that:
- Displays the device name at the top
- Shows all status LEDs with proper colors (green, yellow, red)
- Supports blinking LEDs for flashing status indicators
- Separates charger and inverter sections as on the physical device
- Updates dynamically as status changes
- Provides intuitive navigation to detailed views

## Requirements

- Home Assistant
- [button-card](https://github.com/custom-cards/button-card) custom component
- Victron Energy integration with your MultiPlus inverter/charger

## Installation

1. Make sure you have [button-card](https://github.com/custom-cards/button-card) installed. You can install it via HACS (Home Assistant Community Store) or manually.

2. Copy the contents of `multiplus.yaml` to your configuration.

3. Go to your dashboard, enter edit mode, and add a new card.

4. Choose "Manual" card and paste the YAML configuration.

5. Replace the entity IDs with those from your Victron system.

## Entity Requirements

The card expects the following entities:

| Entity | Purpose |
|--------|---------|
| `sensor.multiplus_name` | Name of the MultiPlus device |
| `sensor.led_mains` | Mains connection status LED (0=off, 1=on, 2=blinking) |
| `sensor.led_bulk` | Bulk charging state LED (0=off, 1=on, 2=blinking) |
| `sensor.led_absorption` | Absorption charging state LED (0=off, 1=on, 2=blinking) |
| `sensor.led_float` | Float charging state LED (0=off, 1=on, 2=blinking) |
| `sensor.led_inverter` | Inverter status LED (0=off, 1=on, 2=blinking) |
| `sensor.led_overload` | Overload warning LED (0=off, 1=on, 2=blinking) |
| `sensor.led_low_battery` | Low battery warning LED (0=off, 1=on, 2=blinking) |
| `sensor.led_temperature` | Temperature warning LED (0=off, 1=on, 2=blinking) |

## MQTT SETUP

This card uses Victron systems that publish data to MQTT.
The screenshot shows the MQTT topic structure for this card used by Victron's Cerbo GX:
cerbo/N/xxxxxxxxxxxx/vebus/276/Leds/

<img width="200" alt="leds" src="https://github.com/user-attachments/assets/7ae09a9b-b605-41d0-8582-010e66748c0e" />

### Where:

- cerbo - The device type
- N - System instance number
- xxxxxxxxxxxx - Unique identifier
- vebus/276 - VE.Bus device at address 276
- Leds - Collection of LED status indicators

### The LED status values follow Victron's convention:

- 0 = LED is off
- 1 = LED is on solid
- 2 = LED is blinking

### You can use mqtt-explorer to see your structure

### More info about LEDS meaning can be found on the victron website

## Setting Up MQTT Sensors

To use this card with MQTT data, you'll need to create sensors in your Home Assistant configuration.yaml
# Example configuration.yaml entry for MQTT sensors

```yaml
mqtt:
  sensor:
    - name: "LED Mains"
      state_topic: "cerbo/N/xxxxxxxxxxxx/vebus/276/Leds/Mains"
      value_template: "{{ value_json.value }}"
      unique_id: led_mains
      
    - name: "LED Bulk"
      state_topic: "cerbo/N/xxxxxxxxxxxx/vebus/276/Leds/Bulk"
      value_template: "{{ value_json.value }}"
      unique_id: led_bulk
      
    # Add similar entries for all other LEDs
```

Replace N and xxxxxxxxxxxx with your actual system values.

## Customization Options

The card includes several customization options within the SVG code:

### Visual Configuration

- Colors for the device body and accent bar
- LED colors for different states
- Text sizes and styling
- Card dimensions and padding

## How It Works

The card uses SVG (Scalable Vector Graphics) to create a visual representation of a Victron MultiPlus:

1. **Device Frame**: Blue rectangle with rounded corners replicating the physical device
2. **Device Name**: Shows the configured name from your MultiPlus
3. **Orange Bar**: Replicates the distinctive orange label bar on the physical device
4. **LED Indicators**: Eight status LEDs in their proper colors:
   - Green LEDs: Mains and Inverter
   - Yellow LEDs: Bulk, Absorption, Float
   - Red LEDs: Overload, Low Battery, Temperature

The JavaScript code:
- Retrieves current states from your LED sensors
- Processes the LED values (0=off, 1=on, 2=blinking)
- Applies the appropriate colors to each LED
- Adds CSS animation for blinking LEDs
- Formats and positions all elements
- Returns the SVG code which is rendered by Home Assistant

## Troubleshooting

- If LEDs don't appear correctly, ensure your sensors are reporting values as integers (0, 1, or 2)
- Check that the entity IDs are correct and accessible
- Verify that button-card is properly installed
- If LED states don't update, check the `triggers_update` list includes all needed entities

## Advanced Usage

### Multiple MultiPlus Cards

To display multiple MultiPlus devices on your dashboard:

1. Copy the card configuration multiple times
2. Change the entities for each card to match different inverter/chargers
3. Consider adjusting the navigation paths for each card

## License

MIT License - Feel free to use and modify as needed.

## Acknowledgments

- Inspired by the physical appearance of Victron MultiPlus inverter/chargers
- Built using the flexible [button-card](https://github.com/custom-cards/button-card) component
- Thanks to the Victron Energy and Home Assistant communities
