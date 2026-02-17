# Home Assistant CLI for OpenClaw

A Home Assistant skill for OpenClaw that allows controlling smart home devices via the Home Assistant API.

## Features

- **Lights**: on/off, brightness, RGB color
- **Switches**: on/off
- **Covers**: open/close/stop (blinds, garage doors)
- **Climate**: temperature, HVAC mode
- **Scenes**: activate any scene
- **Scripts**: run any script
- **Entity Discovery**: list all devices
- **History**: query sensor history
- **Custom Services**: call any HA service

## Requirements

- Node.js 18+
- Home Assistant with Long-Lived Access Token

## Installation

```bash
# Clone or copy to your OpenClaw skills folder
cp -r homeassistant ~/.openclaw/workspace/skills/
```

## Configuration

Set environment variables:

```bash
export HA_URL="http://homeassistant.local:8123"
export HA_TOKEN="your_long_lived_access_token"
```

### Get Long-Lived Access Token

1. Open Home Assistant Web UI
2. Click your username (Profile)
3. Scroll to "Long-Lived Access Tokens"
4. Click "Create Token"
5. Name it (e.g., "OpenClaw")
6. Copy the token (shown once!)

## Usage

```bash
# Status & Discovery
ha-cli discover              # Find HA on network
ha-cli status               # Get HA status & entity count
ha-cli entities             # List all entities
ha-cli entities --domain light  

# Lights
 # Filter by domainha-cli light on "Living Room"
ha-cli light off "Bedroom"
ha-cli light brightness 75 "Kitchen"
ha-cli light rgb "#FF5500" "Desk Lamp"

# Switches
ha-cli switch on "TV Plug"
ha-cli switch off "Garage"

# Covers
ha-cli cover open "Bedroom Blinds"
ha-cli cover close "Living Room Curtains"
ha-cli cover stop "All Blinds"

# Climate
ha-cli climate set 22 "Thermostat"
ha-cli climate mode auto "AC"
ha-cli climate off "Heater"

# Scenes & Scripts
ha-cli scene activate "Movie Mode"
ha-cli script run "Morning Routine"

# Advanced
ha-cli service call light.turn_on entity_id="light.living" brightness=255
ha-cli history "sensor.temperature" --hours 24
ha-cli event fire "my_event" '{"key": "value"}'
```

## Running from OpenClaw

The skill integrates with OpenClaw's tool system. Use the `exec` tool:

```bash
# Set environment in your command
HA_URL="http://ha:8123" HA_TOKEN="xxx" ha-cli light on "Living Room"
```

Or configure in your shell profile (~/.bashrc):

```bash
export HA_URL="http://homeassistant.local:8123"
export HA_TOKEN="your_token_here"
```

## Supported Domains

- `light` - On/Off, brightness, RGB, color temp
- `switch` - On/Off
- `cover` - Open/close/stop, position
- `climate` - Temperature, mode
- `fan` - On/Off, speed
- `lock` - Lock/unlock
- `media_player` - Play/pause, volume
- `scene` - Activate
- `script` - Run
- `input_boolean`, `input_number`, `input_select`

## Files

```
homeassistant/
├── SKILL.md      # OpenClaw skill documentation
├── ha-cli        # Main CLI (Node.js)
├── ha            # Bash wrapper
└── config.json   # Config template
```

## License

MIT
