# Home Assistant SVG

A collection of custom SVG-based components for Home Assistant that provide visual representations of various home systems and sensors.

<img width="125" alt="battery" src="https://github.com/user-attachments/assets/0f1f505c-fa34-46b5-9929-e9f7b357fdc1" />
<img width="125" alt="standing_light_100_green" src="https://github.com/user-attachments/assets/babf753c-22be-4ef2-bea3-84dea4240ddf" />
<img width="125" alt="window_open" src="https://github.com/user-attachments/assets/7f8a504d-ef8e-43a8-8f95-abef27f5e16d" />
<img width="125" alt="shutter" src="https://github.com/user-attachments/assets/cbe3bfef-d186-4c15-a494-29b5defc3ded" />
<img width="125" alt="thermo" src="https://github.com/user-attachments/assets/181beedf-aa3c-44b3-8ba6-453e6dde0dbd" />


## Overview

This library contains custom SVG-based cards for Home Assistant that display various home systems and sensor data in visually intuitive and aesthetically pleasing ways. Instead of standard gauges and text, these components mimic the appearance of physical devices and provide at-a-glance information through visual indicators.

## Components

The library currently includes:

### Battery Status
Visual battery indicators showing charge level, charging status, and connection information.

### Window Shutter
Visual representation of a window with shutter. Animates when entity has a position attribute.

### Window
Visual representation of a window open and closed state. 

### Lights
Visual representation of ceiling and standing lights. Animates color and brightness 

### Motion Sensor
Motion Sensor with visual indicators for detected/not detected status.

### Water Usage Level
Water tank level indicators and usage statistics visualization.

### Thermometer
Temperature display with visual indicators for heating/cooling status.

### Airco/Air Purifier
Visual representation of an air purifier with led indicators, animated airflow lines and air quality status.

### Victron MPPT Solar Controller & Multiplus
Visual representation of a Victron MPPT solar charge controller with daily yield and charging state indicators and a Multiplus with visual representation off the LED Status.

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
      let entity_id = 'sensor.your_main_entity';
      let textTransform = 'uppercase';

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
            <text text-anchor="middle" class="text" x="20" y="40" fill="white" font-size="12">
                ${entity_id}
            </text>
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
## Advanced Usage

### Combining SVGs into Custom Room Card

As shown in the example image, you can combine multiple SVG components to create a unified dashboard view. This allows you to display multiple sensors and indicators in a cohesive and visually appealing layout.

<img width="232" alt="advanced_room_card" src="https://github.com/user-attachments/assets/c2b54849-106f-4194-8804-487a47ac2853" />

#### How to Use SVGs in Custom Dashboards

You can extract the JavaScript code from inside each card's custom field and place it inside your own button card configuration. This allows you to:

1. Create dashboards that combine multiple SVG components in a single view
2. Position and scale components independently to create a custom layout
3. Add your own styling and background elements to create a unique design

The example image shows a visual representation of a living room with good air quality, 13μg/m³, the purifier is working on minimum speed, the ceiling light is off, the standing light in the corner is on and on full brightness, the window and window shutter are closed (i combined the shutter and window functionality into 1 SVG and 1 custom field), the temperature is a lovely 19.8°C and humidity is around 57%. 

#### WARNING: make sure you use different naming schemes when combining custom fields into your own button-card.

For example (Combining the 2 lights):

- They both share the same filter IDs "lightGlow".

```yaml
    <filter id="lightGlow" x="-50%" y="-50%" width="200%" height="200%">
      <feGaussianBlur stdDeviation="${state === 'on' ? glowIntensity : 0}" result="blur" />
      <feComposite in="SourceGraphic" in2="blur" operator="over" />
    </filter>
```

- Rename IDs in both custom fields, make sure they are unique from each other.

```yaml
    <filter id="ceilinglightGlow" x="-50%" y="-50%" width="200%" height="200%">
      <feGaussianBlur stdDeviation="${state === 'on' ? glowIntensity : 0}" result="blur" />
      <feComposite in="SourceGraphic" in2="blur" operator="over" />
    </filter>
```

- Dont forget to update the name everywhere it excists in the code

```yaml
    <path d="M120,120 L180,120 L210,170 L90,170 Z" class="${state === 'on' ? 'light-cone-active' : 'light-cone'}"
    filter="${state === 'on' ? 'url(#ceilinglightGlow)' : ''}" />
```

### Using SVGs as MDI Icon Replacements

Another use case is to use these SVGs as replacements for existing MDI icons that are not dynamic. Standard Home Assistant icons are static, but these SVG components can provide visual feedback by:

1. Changing colors based on entity states or thresholds
2. Filling to different levels to represent percentages or values
3. Displaying actual numerical data within the icon itself
4. Animating to show status changes or alerts

### Creating Your Own Components

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

