# Home Assistant Skill

Control smart home devices via Home Assistant API. Optimized for one-command setup and natural language.

## Quick Start

### One-Command Setup

```bash
ha-cli setup <url> <token>
```

Example:
```bash
ha-cli setup 192.168.1.100 your_long_lived_token
# or
ha-cli setup http://homeassistant.local:8123 your_token
```

That's it! Configuration is saved automatically.

## Get Your Token

1. Open Home Assistant Web UI
2. Click your username (Profile)
3. Scroll to "Long-Lived Access Tokens"
4. Click "Create Token"
5. Copy the token (shown once!)

## Usage - Natural Commands

### Basic Control

```bash
# Turn on/off (any device type)
ha-cli on living room
ha-cli off bedroom light
ha-cli open garage door
ha-cli close blinds

# Alternative syntax (name + action)
ha-cli living room on
ha-cli bedroom light off
```

### Brightness & Color

```bash
ha-cli brightness 75 living room
ha-cli brightness 50 kitchen
ha-cli rgb #FF5500 desk lamp
```

### Temperature

```bash
ha-cli 22 thermostat
ha-cli temperature 24 bedroom
```

### Scenes & Scripts

```bash
ha-cli scene movie
ha-cli scene good morning
ha-cli script morning
ha-cli run cleanup
```

### Status & Discovery

```bash
ha-cli status           # Show HA status
ha-cli list             # List all entities
ha-cli list light       # List only lights
ha-cli list switch     # List only switches
```

### Get Entity State

```bash
ha-cli living room      # Show state of entity
```

## Smart Features

- **Fuzzy matching**: "living" matches "Living Room Lights"
- **Auto-discovery**: First-time setup tries common addresses
- **Partial names**: "bed" finds "Bedroom Light", "Bedroom AC", etc.
- **Smart suggestions**: Shows close matches if entity not found

## Configuration

Configuration is saved to `config.json` in the skill folder:

```json
{
  "url": "http://192.168.1.100:8123",
  "token": "your_token_here"
}
```

Or use environment variables:

```bash
export HA_URL="http://homeassistant.local:8123"
export HA_TOKEN="your_token"
```

## Advanced

```bash
# Call any HA service
ha-cli call light.turn_on "living room"

# Show all commands
ha-cli help
```

## Supported Devices

- Lights (on/off, brightness, RGB)
- Switches
- Covers (blinds, garage doors)
- Climate (temperature)
- Locks
- Scenes
- Scripts
- Any HA entity
