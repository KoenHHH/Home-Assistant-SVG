# Home Assistant SVG

A collection of custom SVG-based components for Home Assistant that provide visual representations of various home systems and sensors.

<img width="125" alt="battery" src="https://github.com/user-attachments/assets/0f1f505c-fa34-46b5-9929-e9f7b357fdc1" />
<img width="125" alt="thermo" src="https://github.com/user-attachments/assets/181beedf-aa3c-44b3-8ba6-453e6dde0dbd" />
<img width="125" alt="shutter" src="https://github.com/user-attachments/assets/cbe3bfef-d186-4c15-a494-29b5defc3ded" />


## Overview

This library contains custom SVG-based cards for Home Assistant that display various home systems and sensor data in visually intuitive and aesthetically pleasing ways. Instead of standard gauges and text, these components mimic the appearance of physical devices and provide at-a-glance information through visual indicators.

## Components

The library currently includes:

### Battery Status
Visual battery indicators showing charge level, charging status, and connection information.

### Window Shutter
Visual representation of a window with shutter. Animates when entity has a position attribute.

### Water Usage Level
Water tank level indicators and usage statistics visualization.

### Thermometers
Temperature display with visual indicators for heating/cooling status.

### Custom Switches
Visually appealing switch controls that mimic physical switches.

### VICTRON MPPT Solar Controller
Visual representation of a Victron MPPT solar charge controller with daily yield and charging state indicators.

### VICTRON Multiplus 
Visual representation of a Victron Multiplus LED Status.

### .............

## Features

- **Visual Feedback**: All components provide visual feedback through colors, fill levels, and indicators
- **Real-Time Updates**: Components update in real-time as sensor values change
- **Interactive Elements**: Many components include tap actions for navigation to detailed views
- **Fully Customizable**: All SVG elements can be customized (colors, sizes, indicators)
- **Responsive Design**: Components scale appropriately on different devices and screen sizes

## How It Works

These components use the `custom:button-card` to render SVG graphics that are dynamically updated using JavaScript based on entity states. The SVG code is embedded within the YAML configuration and uses template literals to create dynamic visualizations.

## Installation

### Prerequisites

- Home Assistant instance
- [button-card](https://github.com/custom-cards/button-card) custom component
- Relevant sensors/entities for the components you wish to use

### Setup

1. Install the `button-card` custom component if you haven't already
2. Copy the YAML configuration for any component you want to use to your dashboard
3. Adjust the entity IDs to match your Home Assistant setup
4. Customize colors, sizes, and other visual elements as desired

## Customization

Each component can be customized in various ways:

- **Colors**: Change the main colors, accent colors, and indicator colors
- **Entities**: Replace the default entity IDs with your own
- **Scale/Range**: Adjust the min/max values for gauges and indicators
- **Layout**: Modify the SVG elements' positions and sizes
- **Logic**: Customize the JavaScript logic that determines how entity states are visualized

## Usage Examples

Each component's directory contains detailed documentation and usage examples. Here's a general example of how a component is structured:

```yaml
type: custom:button-card
entity: sensor.your_main_entity
show_name: false
show_icon: false
tap_action:
  action: navigate
  navigation_path: "#detailed-view"
triggers_update:
  - sensor.your_main_entity
  - sensor.related_entity_1
  - sensor.related_entity_2
custom_fields:
  svg_component: |
    [[[ 
      let entity_id = 'sensor.victron_system_battery_soc';

      return `
        <div style="width: 100%; padding: 5px; position: relative;">
          <svg width="100%" height="auto" viewBox="0 0 300 240" xmlns="http://www.w3.org/2000/svg">
            <style>
              .text {
                text-transform: ${textTransform};
              }
            </style>  

            <rect x="20" y="20" width="100" height="100" rx="10" ry="10" fill="white" />
            <circle cx="20" cy="20" r="10" fill="white" />
            <text text-anchor="middle" class="text" x="20" y="40" fill="white" font-size="12">${entity_id}</text>
            
           </svg>
         </div>
      `;
    ]]]
styles:
  card:
    - position: relative
    - display: block
    - width: 100%
```

## Creating Your Own Components

You can use the existing components as templates to create your own custom visualizations:

1. Start with one of the existing components as a base
2. Modify the SVG elements to match your desired visualization
3. Update the JavaScript logic to use your entity IDs and visualization logic
4. Add new visual elements or indicators as needed

## Best Practices

- Keep SVG viewBox consistent for similar components
- Use consistent color schemes across components
- Comment your JavaScript code for easier maintenance
- Use relative positioning for SVG elements to ensure proper scaling
- Test components on different devices and screen sizes

## Troubleshooting

- If a component isn't updating, check that all required entities exist and are properly monitored in `triggers_update`
- For JavaScript errors, inspect the browser console while viewing the dashboard
- If SVG elements appear misaligned, check the viewBox settings and element positioning
- Ensure entity IDs match exactly with those in your Home Assistant instance

## Contributing

Contributions to this library are welcome! Please feel free to submit pull requests with new components or improvements to existing ones.

## License

MIT
