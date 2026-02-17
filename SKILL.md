# Home Assistant Skill

Control smart home devices via Home Assistant API.

## Setup

### Configuration (Environment Variables)

Set these in your environment or ask user to configure:

```bash
# Required
export HA_URL="http://homeassistant.local:8123"
export HA_TOKEN="your_long_lived_access_token"

# Optional (for local discovery)
export HA_USE_WS=true
```

### Get Long-Lived Access Token

1. Open Home Assistant UI
2. Go to Profile (click your username)
3. Scroll down to "Long-Lived Access Tokens"
4. Click "Create Token"
5. Name it (e.g., "OpenClaw")
6. Copy the token (only shown once!)

## Usage

### Discovery & Status

```bash
# Discover HA instance on network
ha-cli discover

# Check connection and get system info
ha-cli status

# Get all entities
ha-cli entities

# Get entities by domain
ha-cli entities --domain light
ha-cli entities --domain switch
ha-cli entities --domain climate
ha-cli entities --domain cover
ha-cli entities --domain sensor
ha-cli entities --domain binary_sensor
```

### Control Devices

```bash
# Lights
ha-cli light on "Living Room Lights"
ha-cli light off "Bedroom Light"
ha-cli light brightness 75 "Kitchen Light"
ha-cli light rgb "#FF5500" "Desk Lamp"

# Switches
ha-cli switch on "Garage Door"
ha-cli switch off "TV Plug"

# Covers (Blinds/Doors)
ha-cli cover open "Bedroom Blinds"
ha-cli cover close "Living Room Curtains"
ha-cli cover stop "All Blinds"

# Climate
ha-cli climate set 22 "Thermostat"
ha-cli climate mode "auto" "Upstairs AC"
ha-cli climate off "Heater"

# Scenes
ha-cli scene activate "Movie Mode"
ha-cli scene activate "Good Morning"

# Scripts
ha-cli script run "Morning Routine"
```

### Advanced

```bash
# Call any HA service
ha-cli service call light.turn_on entity_id="light.living_room" brightness=255

# Get history for entity
ha-cli history "sensor.temperature" --hours 24

# Fire an event
ha-cli event fire "my_custom_event" '{"key": "value"}'
```

## Supported Domains

- `light` - On/Off, brightness, RGB, color temperature
- `switch` - On/Off
- `cover` - Open/close/stop, position
- `climate` - Temperature, mode, off
- `fan` - On/Off, speed, oscillation
- `lock` - Lock/unlock
- `alarm_control_panel` - Arm/disarm
- `media_player` - Play/pause, volume, source
- `vacuum` - Start/stop/return_to_base
- `water_heater` - Temperature, mode
- `scene` - Activate
- `script` - Run
- `input_boolean` - On/Off
- `input_number` - Set value
- `input_select` - Select option

## Entity Matching

- Entity ID or friendly name works
- Case-insensitive partial matching
- Use quotes for names with spaces

## Error Handling

- Connection errors show helpful message
- Invalid entity shows closest matches
- Token errors indicate how to fix
