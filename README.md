# FixCreative - Creative Mode Restriction Plugin

A plugin for Minecraft servers that restricts creative mode usage with separate inventories, time limits, and region-based access control.

## Compatibility

- **Minecraft Version**: 1.21.4
- **Server Software**: 
  - ✅ **Paper** 1.21.4+ (recommended)
  - ✅ **Purpur** 1.21.4+ (fully compatible)
  - ✅ **Pufferfish** 1.21.4+ (fully compatible)
  - ⚠️ **Spigot** 1.21.4+ (may have compatibility issues, not recommended)
  - ❌ **Folia** (not compatible - different threading model)
  - ❌ **CraftBukkit/Vanilla** (no plugin API)
- **Java Version**: 21 or newer
- **Dependencies**: 
  - WorldGuard (optional, for private region support)
  - LuckPerms (optional, for group-based time limits)

## Features

- **Separate Inventories**: Independent inventories for survival and creative modes
- **Creative Restrictions**: Cannot use storage blocks, drop items, or use non-whitelisted commands
- **Private Regions**: Creative mode only available in WorldGuard private regions (configurable)
- **Time Limits**: Configurable time limits with cooldown periods per player group
- **Multi-Language**: Supports 6 languages (ru, en, de, es, fr, pl)
- **Auto-Switching**: Automatically switches to survival when leaving regions or logging in

## Installation

1. Download `FixCreative.jar` from releases
2. Place it in your server's `plugins` folder
3. Restart the server
4. Configure `plugins/FixCreative/config.yml`

## Commands

- `/fixcreative` or `/fc` - Toggle between survival and creative
- `/fixcreative survival` - Switch to survival mode
- `/fixcreative creative` - Switch to creative mode
- `/fixcreative reload` - Reload configuration (requires permission)

## Permissions

- `fixcreative.use` - Use the main command (default: OP)
- `fixcreative.reload` - Reload plugin config (default: OP)

## Configuration

### Main Settings

```yaml
# Language: ru, en, de, es, fr, pl
language: ru

# Chat message prefix
prefix: "&8[&6FixCreative&8] &r"

creative:
  # Blocks that cannot be placed/picked up in creative
  prohibited-place-blocks:
    - TNT
    - BEDROCK
    - CHEST
    # ... more blocks
  
  # Prohibit all storage blocks (true/false)
  prohibit-storage-blocks: true
  
  # Allowed commands in creative mode
  allowed-commands:
    - fixcreative
    - fc
  
  # Time limit system
  time-limit:
    enabled: true
    default:
      max-time-hours: 2      # Max time per session
      cooldown-hours: 24     # Cooldown after time expires
    
    # Group-specific limits (LuckPerms groups)
    groups:
      vip:
        max-time-hours: 4
        cooldown-hours: 12
        group: "vip"
        priority: 10

private:
  # Enable region checking
  check-private-regions: true
  
  # Region names (empty = all regions)
  region-names: []
```

### Language Files

Messages are in `plugins/FixCreative/languages/`:
- `ru_message.yml`, `en_message.yml`, `de_message.yml`, `es_message.yml`, `fr_message.yml`, `pl_message.yml`

Files are auto-copied on first load. Edit them to customize messages.

## Building

### Maven (Command Line)

```bash
mvn clean package
```

Output: `target/FixCreative-1.0.0.jar`

### IDE

**IntelliJ IDEA**: Maven panel → `Lifecycle → clean` → `Lifecycle → package`

**Eclipse**: Right-click `pom.xml` → `Run As` → `Maven build...` → Goals: `clean package`

**VS Code**: Terminal → `mvn clean package`

## How It Works

1. **Inventories**: Separate survival/creative inventories are saved and loaded when switching modes
2. **Restrictions**: In creative, storage blocks, item frames, armor stands, and item dropping are blocked
3. **Regions**: If enabled, creative only works in WorldGuard regions where player is owner/member
4. **Time Limits**: Tracks creative usage time per player/group with automatic cooldown
5. **Auto-Switch**: Switches to survival when leaving regions or on server join

## License

This plugin is proprietary software. All rights reserved.

**Free Use:**
- ✅ Use this plugin on your Minecraft server
- ✅ Modify the plugin for personal use

**Commercial Use:**
- ❌ You may NOT sell, redistribute, or commercially distribute this plugin without explicit written permission from the author
- ❌ You may NOT claim this plugin as your own work
- 📧 For commercial licensing, revenue sharing, or distribution rights, contact the author: tg:@fixsirt

**Full License:** See [LICENSE](LICENSE) file for complete terms and conditions.

**Commercial Distribution Agreement:**
If you wish to sell or commercially distribute this plugin, you must:
1. Contact the author for a commercial license agreement
2. Agree to revenue sharing terms (percentage of sales)
3. Obtain written permission before any commercial activity

**Violation of these terms may result in legal action.**
