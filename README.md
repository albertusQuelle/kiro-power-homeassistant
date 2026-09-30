![Cover](cover.jpg)

# Home Assistant Power for Kiro

A Kiro Power that brings Home Assistant expertise directly into your development workflow. Control devices through natural language, write YAML configurations, and build automations with instant access to Home Assistant knowledge and capabilities.

## What is a Kiro Power?

Powers are unified packages that combine MCP tools with framework expertise. Instead of just providing API access, powers give Kiro deep knowledge of Home Assistant patterns, best practices, and workflows. When you mention "homeassistant" or "hass," the power activates—loading relevant tools and context dynamically.

## Features

This power provides comprehensive Home Assistant support:

- **80+ MCP Tools**: Complete Home Assistant API access for device control, automation creation, dashboard management, and system configuration
- **Specialized Knowledge**: YAML automation patterns, best practices, debugging workflows, and Home Assistant conventions
- **Guided Workflows**: Step-by-step assistance for common tasks like creating automations, troubleshooting issues, and optimizing configurations

**MCP tool categories:**

- **Search & Discovery**: Unified search across entities and configs (`ha_search`), system overview, live state
- **Control**: Any service call, bulk device control, custom events
- **Management**: Automations, scripts, scenes, helpers, dashboards, areas/floors, zones, groups, labels, categories, calendars, blueprints, integrations
- **Monitoring**: History, camera snapshots, automation/script traces, logs, system health (incl. Zigbee/Z-Wave)
- **System**: Backups, updates, apps (add-ons), HACS, radios (Z-Wave/Zigbee/Matter/Thread), themes, energy prefs, device/entity registry

The server also ships bundled best-practice guides via `ha_get_skill_guide`, which Kiro consults before structured tasks.

## Usage Examples

### Device Control & State Query

- "Turn on the living room lights"
- "What's the temperature in the bedroom?"
- "Which lights are currently on?"

### Automation & Template Development

- "Create an automation that turns on the porch light at sunset"
- "Why isn't my motion sensor automation working?"
- "Create a template sensor that averages two temperature sensors"

### Dashboard Management

- "Show me my current dashboard configuration"
- "Add a weather card to my dashboard"
- "Create a new view for my climate controls"

### YAML Configuration

- "Can you review my automation YAML for best practices?"
- "How should I split my configuration.yaml?"
- "My template sensor shows 'unavailable' on startup"
- "Update my old automation to use modern syntax"

## Installation

### From GitHub

1. Open Kiro
2. Open Powers panel
3. Click "Import power from GitHub"
4. Enter: `https://github.com/rewse/kiro-power-homeassistant/tree/main/power-homeassistant`

### From Local Path

1. Clone this repository
2. Open Kiro → Powers panel
3. Click "Import power from a folder"
4. Select the `power-homeassistant` directory (not `kiro-power-homeassistant` directory)

## How the MCP server runs

This power ships an `mcp.json` that runs the [`ha-mcp`](https://github.com/homeassistant-ai/ha-mcp) server with `uvx --system-certs ha-mcp@latest` over stdio, connecting to your Home Assistant with a long-lived token. Using the operating system trust store also supports enterprise TLS proxies and private certificate authorities. This works on any Home Assistant install type and is the zero-extra-setup default for this power.

The `ha-mcp` project also offers other ways to run the same server, which you can point Kiro at instead:

- **HACS in-process Custom Component (upstream's recommended path):** installs into Home Assistant via HACS and runs in-process on every install type, with no token to manage. You connect Kiro to a server URL from the integration's Configure screen.
- **Home Assistant app (add-on):** for Home Assistant OS / Supervised installs, also token-free.
- **Docker (HTTP):** run `ghcr.io/homeassistant-ai/ha-mcp` pointed at your Home Assistant URL and token.

See the [ha-mcp README](https://github.com/homeassistant-ai/ha-mcp) and [Setup Wizard](https://homeassistant-ai.github.io/ha-mcp/setup/) for those methods. Use exactly one method per client.

## Prerequisites

The default (uvx) method requires `uv` to be installed:

**macOS / Linux:**
```bash
brew install uv
# or
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows:**
```powershell
winget install astral-sh.uv -e
```

## Configuration

### 1. Generate Access Token

1. Log in to Home Assistant
2. Profile → Security → Long-lived access tokens
3. Click "Create token" and copy it

### 2. Set Environment Variables

When installing the power, configure:
- `HOMEASSISTANT_URL`: Your Home Assistant URL (e.g., `http://homeassistant.local:8123`)
- `HOMEASSISTANT_TOKEN`: The generated long-lived access token

### 3. Test

Ask Kiro: "Can you see my Home Assistant?"

## Project Structure

```
.
├── power-homeassistant/
│   ├── POWER.md           # Power metadata and documentation
│   ├── mcp.json           # MCP server configuration
│   └── steering/
│       ├── homeassistant-companion-app-guide.md # Companion app, notifications, and mobile features
│       ├── homeassistant-dev-guide.md      # YAML and development patterns
│       ├── homeassistant-mcp-tools.md      # MCP tools reference
│       ├── homeassistant-scripts-guide.md  # Script syntax, actions, and conditions
│       ├── homeassistant-smart-climate-guide.md # Modular climate/lighting automation patterns
│       ├── homeassistant-templating-guide.md # Jinja2 templating reference
│       ├── homeassistant-tips-and-tricks.md # Practical tips: Assist, subviews, zones, dynamic scenes
│       └── homeassistant-advanced-workflows.md # Extended workflow examples
├── LICENSE.md
└── README.md
```

## How It Works

This power combines:

1. **MCP Tools**: 80+ tools from [ha-mcp](https://github.com/homeassistant-ai/ha-mcp) for direct Home Assistant API access
2. **Framework Expertise**: Built-in knowledge of Home Assistant patterns, YAML syntax, and best practices

When you mention keywords like "homeassistant," "home assistant," "hass,", "ha-mcp", or "lovelace," the power activates—loading relevant tools and context.

## Troubleshooting

### Cannot Connect
- Verify `HOMEASSISTANT_URL` is correct
- Ensure Home Assistant is running
- Check network/firewall settings

### Authentication Error
- Verify `HOMEASSISTANT_TOKEN` is correct
- Generate a new token if needed

### uv Not Found
- Install `uv` and restart terminal

For detailed troubleshooting, see the [official FAQ](https://github.com/homeassistant-ai/ha-mcp/blob/master/docs/FAQ.md).

## Credits

Special thanks to the [Home Assistant AI team](https://github.com/homeassistant-ai/ha-mcp) for their excellent work on the MCP server.
