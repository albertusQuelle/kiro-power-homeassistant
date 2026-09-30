# Home Assistant MCP Server Tools Reference

## MCP Server: Home Assistant

**Package:** `ha-mcp@latest` (verified against ha-mcp 8.x)
**Connection:** uvx-based MCP server (also runnable as a HACS in-process component or Home Assistant app — see README)
**Authentication:** Home Assistant long-lived access token (for the uvx/PyPI and Docker methods)

**Configuration Required (uvx/PyPI method):**
- `HOMEASSISTANT_URL` - Your Home Assistant URL (e.g., `http://homeassistant.local:8123`)
- `HOMEASSISTANT_TOKEN` - Long-lived access token

> The in-process HACS component and the Home Assistant app run inside Home Assistant and need no token — you connect Kiro to a server URL instead. This reference describes the tools; they are identical across install methods.

## Start Here: `ha_get_skill_guide`

The server ships bundled best-practice "skill" guides. **Call `ha_get_skill_guide` first** before automations, dashboards, templates, and other structured work. It returns the server's own up-to-date guidance and complements the steering files in this power.

## Consolidated tool model (ha-mcp 8.x)

ha-mcp 8.x consolidated many single-purpose tools into a smaller set of multi-mode tools. Instead of separate `list`/`get` tools, most read tools take an optional identifier (omit it to list, pass it to fetch one). Instead of separate `create`/`update`/`delete` tools, most writes use a `ha_set_*` (create or update) plus `ha_remove_*` pair, and several domains use a single `ha_manage_*` tool with an `action` parameter.

Key conventions:
- `ha_set_*` — create when no ID is given, update when an ID is given.
- `ha_get_*` — list when no ID is given, fetch details when an ID is given.
- `ha_manage_*` — takes an `action` argument (e.g., `list`, `install`, `remove`).

## Available Tools (77 tools)

### Discovery & State
- `ha_search` — Search entities by name/domain/area AND inside automation/script/scene/helper/dashboard configs (replaces the old `ha_search_entities` and `ha_deep_search`)
- `ha_get_overview` — AI-friendly system overview with intelligent categorization
- `ha_get_state` — Current state and attributes of one or more entities
- `ha_get_entity` — Entity registry information for one or more entities
- `ha_get_entity_exposure` — Assist/voice exposure settings (list all, or one entity)
- `ha_get_history` — Historical/time-series and statistics data from the recorder (replaces `ha_get_statistics`)
- `ha_get_logs` — Home Assistant logs from various sources (replaces `ha_get_logbook`)
- `ha_get_camera_image` — Snapshot from a camera entity
- `ha_eval_template` — Evaluate a Jinja2 template with Home Assistant's engine

### Control & Services
- `ha_call_service` — Execute any Home Assistant service (device control, trigger automations)
- `ha_bulk_control` — Explicit operations or one deterministic structural bulk action
- `ha_call_event` — Fire a custom event on the event bus
- `ha_list_services` — List available services (paginated, detail control)
- `ha_get_operation_status` — Status of device operations with WebSocket verification

### Entities & Devices
- `ha_set_entity` — Update entity registry properties (rename, area, disable, labels — replaces `ha_rename_entity`)
- `ha_remove_entity` — Remove one or more entities from the registry
- `ha_get_device` — Device info (paginated), including Zigbee (ZHA/Z2M) and Z-Wave JS (replaces `ha_list_devices`/`ha_get_zha_devices`)
- `ha_set_device` — Update device name, area, disabled state, labels
- `ha_remove_device` — Remove an orphaned device from the registry

### Automations
- `ha_config_get_automation` — Read automation config (list all, or one by ID)
- `ha_config_set_automation` — Create or update an automation
- `ha_config_remove_automation` — Delete an automation
- `ha_get_automation_traces` — Execution traces for automations and scripts (debugging)

### Scripts
- `ha_config_get_script` — Read script config
- `ha_config_set_script` — Create or update a script
- `ha_config_remove_script` — Delete a script

### Scenes
- `ha_config_get_scene` — Read scene config
- `ha_config_set_scene` — Create or update a scene
- `ha_config_remove_scene` — Delete a scene

### Helpers & Integrations
- `ha_config_list_helpers` — List helpers of a type with their config
- `ha_config_set_helper` — Create or update helper entities and config subentries (template sensors are created here; there is no separate `ha_config_set_template`)
- `ha_get_integration` — Integration (config entry) information (paginated)
- `ha_set_integration` — Enable/disable, add, update options, or reconfigure an integration
- `ha_remove_helpers_integrations` — Remove a helper or integration config entry

### Groups
- `ha_config_list_groups` — List entity groups with members
- `ha_config_set_group` — Create or update a service-based group (`group.set`)
- `ha_config_remove_group` — Remove a service-based group (`group.remove`)

### Dashboards
- `ha_config_get_dashboard` — List dashboards, get config, or search for cards (replaces `ha_config_list_dashboards`)
- `ha_config_set_dashboard` — Create or update a dashboard (also handles metadata)
- `ha_config_delete_dashboard` — Delete a storage-mode dashboard
- `ha_config_list_dashboard_resources` — List Lovelace resources (custom cards, themes, CSS/JS)
- `ha_config_set_dashboard_resource` — Create or update a dashboard resource (inline or URL)
- `ha_config_delete_dashboard_resource` — Delete a dashboard resource
- `ha_manage_theme` — Manage frontend themes

### Areas, Floors, Labels & Categories
- `ha_list_floors_areas` — Floors (by level) with nested areas, plus areas without a floor
- `ha_set_area_or_floor` — Create or update an area or floor
- `ha_remove_area_or_floor` — Remove an area or floor
- `ha_config_get_label` — List labels or get one by ID
- `ha_config_set_label` — Create or update a label
- `ha_config_remove_label` — Delete a label
- `ha_config_get_category` — List categories for a scope, or get one by ID
- `ha_config_set_category` — Create or update a category
- `ha_config_remove_category` — Delete a category

### Zones
- `ha_get_zone` — List zones or get one
- `ha_set_zone` — Create or update a zone (replaces `ha_create_zone`/`ha_update_zone`)
- `ha_remove_zone` — Remove a zone

### Todo & Calendar
- `ha_get_todo` — List todo lists or items from a list
- `ha_set_todo_item` — Create or update a todo item
- `ha_remove_todo_item` — Remove a todo item
- `ha_config_get_calendar_events` — Retrieve calendar events
- `ha_config_set_calendar_event` — Create a calendar event
- `ha_config_remove_calendar_event` — Delete a calendar event

### Blueprints
- `ha_manage_blueprints` — List, read, import, save, delete, or render a blueprint (replaces `ha_list_blueprints`/`ha_get_blueprint`/`ha_import_blueprint`)

### Voice / Assist
- `ha_manage_pipeline` — Manage Assist pipelines

### HACS
- `ha_get_hacs_info` — Search the store or fetch repository details (replaces `ha_hacs_info`/`ha_hacs_search`/`ha_hacs_repository_info`)
- `ha_manage_hacs` — Install/update, remove, add custom repos, refresh repo info

### Apps (Add-ons)
- `ha_get_app` — List installed/available apps (add-ons) or one's details (replaces `ha_list_addons`/`ha_list_available_addons`)
- `ha_manage_app` — Manage apps (add-ons) or proxy an app API

### Radios & Energy
- `ha_manage_radio` — Manage Z-Wave, Zigbee, Matter, and Thread radios
- `ha_manage_energy_prefs` — Manage the Energy Dashboard preferences

### System, Updates & Backups
- `ha_get_system_health` — System health, including ZHA, Z-Wave JS, and per-integration diagnostics (replaces `ha_get_system_info`/`ha_get_system_version`)
- `ha_reload_core` — Reload configuration without a full restart (also validates config; use before `ha_restart`)
- `ha_restart` — Restart Home Assistant
- `ha_manage_updates` — List, read details, batch install, skip, or un-skip updates (replaces `ha_list_updates`/`ha_get_release_notes`)
- `ha_manage_backup` — Manage full HA snapshots AND per-edit auto-backups (replaces `ha_backup_create`/`ha_backup_restore`)

### Guides & Diagnostics
- `ha_get_skill_guide` — Bundled best-practice guides — **call first** for matching actions
- `ha_report_issue` — Diagnostic info and templates for filing issue reports

## Auto-Approved (read-only) Tools

The power auto-approves read-only tools so common queries run without prompts. Mutating tools (`ha_set_*`, `ha_remove_*`, `ha_call_service`, `ha_bulk_control`, `ha_manage_*`, `ha_restart`, `ha_reload_core`, deletes) require confirmation by design.

## Tool Usage Guidelines

### Common Patterns

**Pattern 1: Safe entity control**
1. Find the entity: `ha_search`
2. Read current state: `ha_get_state`
3. Act: `ha_call_service`
4. Verify: `ha_get_operation_status`

**Pattern 2: Automation lifecycle**
1. Load guidance: `ha_get_skill_guide`
2. Read existing: `ha_config_get_automation`
3. Create/update: `ha_config_set_automation`
4. Debug: `ha_get_automation_traces`

**Pattern 3: Dashboard customization**
1. Read: `ha_config_get_dashboard`
2. Update: `ha_config_set_dashboard`
3. Custom cards: `ha_config_set_dashboard_resource`

**Pattern 4: Template sensor / helper**
1. Load guidance: `ha_get_skill_guide`
2. Create: `ha_config_set_helper` (helper_type `template`)

**Pattern 5: Bulk operations**
1. Find targets: `ha_search`
2. Execute: `ha_bulk_control`
3. Check: `ha_get_operation_status`

## Error Handling

When tools return errors:
1. Verify entity IDs with `ha_search` or `ha_get_state`
2. Verify service names with `ha_list_services`
3. Confirm authentication (token validity) for the uvx/Docker methods
4. Review `ha_get_automation_traces` for automation issues
5. Check `ha_get_system_health` and `ha_get_logs` for system problems
