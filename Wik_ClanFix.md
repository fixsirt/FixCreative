# ClansFix - Advanced Clan System Plugin

A comprehensive Minecraft plugin for Spigot/Paper servers that provides a full-featured clan system with ranking, houses, treasury management, upgrades, quests, and more.

## Features

### Core Clan Management
- Create, join, and leave clans
- **Colored clan tags** - Use Minecraft color codes (e.g., `&4` for red) to color your clan name
- Clan names and tags (tags are optional, default is white `&f`)
- Member management (invite, kick, promote, demote)
- **5-tier rank system** with different permissions
- Open/closed clan system (open clans can be joined directly, closed clans require requests)
- Pagination support for large clan lists

### Rank System
The plugin features a comprehensive 5-tier rank system:

1. **Novice** (Gray) - Default rank for new members
   - Access to clan house (teleport)
   - View members
   - View rankings
   - Deposit to treasury

2. **Member** (White) - Basic member
   - All Novice permissions
   - Access to clan upgrades
   - View clan quests

3. **Trusted** (Cyan) - Trusted member
   - All Member permissions
   - Full access to clan storage (put/take items)

4. **Veteran** (Gold) - Veteran member
   - All Trusted permissions
   - Full treasury access (deposit and withdraw)

5. **Elder** (Purple) - Senior member
   - All Veteran permissions
   - House management (set/remove)
   - Manage clan requests (accept/reject)
   - Invite players
   - Rank management (promote to Veteran, demote, kick members)
   - Cannot kick other Elders (only leader can)

### Clan Level System
- **5 levels** of clan progression
- Each level increases max members:
  - Level 1: 5 members
  - Level 2: 10 members
  - Level 3: 15 members
  - Level 4: 20 members
  - Level 5: 25 members
- Level upgrades require completing quests and paying costs
- Configurable quests and costs per level

### Quest System
- **Dynamic quest system** with multiple quest types:
  - Kill players
  - Kill mobs (specific types)
  - Collect items
  - Mine blocks
  - Place blocks
  - Catch fish
  - Breed animals
  - Eat food
  - Craft items
  - Plant crops
  - Tame animals
  - Travel distance
  - Enchant items
  - Trade with villagers
  - Brew potions
  - Shear sheep
  - Deal damage
- Quests are required for leveling up
- Progress tracking for all quest types
- Visual quest menu with completion status

### Coat of Arms (Drag & Drop)
- Customizable clan emblems using drag and drop
- Open the coat of arms menu with `/clan coat` or from clan settings
- Drag any item into the slot to set it as your clan's emblem
- Visual representation of your clan in rankings and menus
- Only leaders and Elders can edit

### Clan House System
- Set a clan house location at your current position
- Teleport to the clan house
- Only leaders and Elders can set/remove the house
- All members can teleport to the house
- Visual indicators in the management menu

### Treasury Management
- Deposit and withdraw money from clan treasury
- Balance tracking
- Permission-based access:
  - All members can deposit
  - Only Veterans and above can withdraw
- Visual treasury menu with balance display
- Integration with Vault economy

### Upgrade System
- Access upgrade menu to view clan level
- View available quests for next level
- Cost-based upgrades (configured per level)
- Visual upgrade menu showing current level and requirements
- Max level 5

### Ranking System
The ranking system uses a **composite score** based on KDR and balance:

**Formula:** `Score = (KDR × 100) + (Balance ÷ 100)`

- **KDR** (Kill/Death Ratio) has higher weight (multiplied by 100)
- **Balance** also affects ranking (every 100$ adds 1 point)
- Rankings update automatically every 5 minutes
- Top clans are displayed with special colors:
  - #1: Gold
  - #2: Silver
  - #3: Bronze
- Pagination support for large rankings

### Clan Armor System
- Visual armor display for clan members
- Customizable armor sets per clan
- Only leaders can manage clan armor
- Armor is visible to all players

### Hologram System
- Floating holograms above clan members showing clan name
- Toggle on/off in clan settings
- Colored clan names based on tag
- Automatic removal when leaving/deleting clan

### PvP System
- Toggle PvP between clan members
- Can be enabled/disabled in clan settings
- Only leaders can change PvP settings
- Prevents friendly fire when disabled

### Localization System
- **Multi-language support** with 6 languages:
  - English (en) - Default
  - Russian (ru)
  - German (de)
  - French (fr)
  - Spanish (es)
  - Polish (pl)
- All plugin texts are externalized to language files
- Easy to add new languages
- Language files located in `plugins/ClansFix/languages/`
- Change language in `config.yml`: `language: en`

### PlaceholderAPI Integration
Full PlaceholderAPI support for all clan statistics:

#### Player Placeholders
- `%clans_player_clan%` - Player's clan name
- `%clans_player_tag%` - Player's clan tag
- `%clans_player_level%` - Player's clan level
- `%clans_player_kills%` - Player's clan kills
- `%clans_player_deaths%` - Player's clan deaths
- `%clans_player_kdr%` - Player's clan KDR
- `%clans_player_balance%` - Player's clan balance
- `%clans_player_members%` - Total members in player's clan
- `%clans_player_online%` - Online members in player's clan
- `%clans_player_rank%` - Player's clan rank
- `%clans_player_score%` - Player's clan composite score

#### Top Clan Placeholders (1-10)
- `%clans_topX_name%` - Clan name at position X
- `%clans_topX_tag%` - Clan tag at position X
- `%clans_topX_balance%` - Clan balance at position X
- `%clans_topX_kdr%` - Clan KDR at position X
- `%clans_topX_kills%` - Clan kills at position X
- `%clans_topX_deaths%` - Clan deaths at position X
- `%clans_topX_level%` - Clan level at position X
- `%clans_topX_members%` - Total members at position X
- `%clans_topX_online%` - Online members at position X
- `%clans_topX_leader%` - Leader name at position X
- `%clans_topX_score%` - Composite score at position X

Replace `X` with position number (1-10).

## Commands

### Main Commands
- `/clan` - Open clan menu (management menu if in clan, clan list if not)
- `/clan create <name>` - Create a new clan (tag is optional, defaults to white)
- `/clan join <clan>` - Join an open clan
- `/clan leave` - Leave your current clan
- `/clan delete` - Delete your clan (leader only)
- `/clan reload` - Reload plugin configuration (requires `clansfix.reload` permission)

### Invitation Commands
- `/clan invite <player>` - Invite a player to your clan (Elder+ only)
- `/clan accept <clan>` - Accept a clan invitation
- `/clan decline <clan>` - Decline a clan invitation

### Management Commands
- `/clan house set` - Set clan house at your location (Elder+ only)
- `/clan house tp` - Teleport to clan house
- `/clan treasury` - Open treasury management menu
- `/clan upgrade` - Open upgrade menu
- `/clan top` - View clan rankings
- `/clan ranking` - Alternative command for rankings
- `/clan info` - View your clan's information
- `/clan coat` - Edit coat of arms (drag & drop)
- `/clan kick <player>` - Kick a member (Elder+ only)

### Command Aliases
- `/c` - Alias for `/clan`
- `/cl` - Alias for `/clan`
- `/clans` - Alias for `/clan`

## Permissions

### Main Permissions
- `clansfix.*` - All permissions (default: op)
- `clansfix.admin` - Admin permissions (default: op)
- `clansfix.reload` - Reload plugin (default: op)

### Clan Permissions
- `clansfix.create` - Create clans (default: true)
- `clansfix.join` - Join clans (default: true)
- `clansfix.leave` - Leave clans (default: true)
- `clansfix.invite` - Invite players (default: true)
- `clansfix.kick` - Kick members (default: true)
- `clansfix.house` - Manage clan house (default: true)
- `clansfix.treasury` - Manage treasury (default: true)
- `clansfix.upgrade` - Access upgrade menu (default: true)
- `clansfix.rank` - View rankings (default: true)

## Requirements

### Server Requirements
- **Minecraft Version:** 1.21+ (1.21, 1.21.1, 1.21.2, 1.21.3, 1.21.4, and newer)
- **Server Software:** 
  - **Spigot 1.21+** (recommended)
  - **Paper 1.21+** (highly recommended for better performance)
  - **Bukkit 1.21+** (not recommended, use Spigot/Paper instead)
- **Java Version:** **Java 21 or higher** (required)
  - Java 21 (LTS)
  - Java 22
  - Java 23
  - Java 24+

### Plugin Dependencies
- **ProtocolLib 5.3.0+** (required) - For holograms and visual features
- **Vault** (required) - For economy integration (treasury system)
- **PlaceholderAPI 2.11.6+** (optional but recommended) - For placeholders

### Compatibility Notes
- ✅ **Fully compatible** with Paper 1.21+ (recommended)
- ✅ **Fully compatible** with Spigot 1.21+
- ✅ **Compatible** with newer versions (1.22, 1.23, etc.) - API is forward compatible
- ⚠️ **Not compatible** with versions below 1.21
- ⚠️ **Not compatible** with Java versions below 21

## Installation

### Step-by-Step Installation

1. **Check your server version**
   - Ensure you're running **Minecraft 1.21 or newer**
   - Ensure you're using **Java 21 or higher**
   - Check with: `java -version` (should show Java 21+)

2. **Download required plugins**
   - Download **ProtocolLib** (5.3.0 or newer) from [SpigotMC](https://www.spigotmc.org/resources/protocollib.1997/)
   - Download **Vault** from [SpigotMC](https://www.spigotmc.org/resources/vault.34315/)
   - Download **PlaceholderAPI** (optional) from [SpigotMC](https://www.spigotmc.org/resources/placeholderapi.6245/)

3. **Install plugins**
   - Place all downloaded JAR files in your server's `plugins` folder
   - Place **ClansFix** JAR file in the `plugins` folder

4. **Start your server**
   - Start/restart your server
   - Wait for all plugins to load

5. **Configure the plugin**
   - Edit `plugins/ClansFix/config.yml` to set your preferred language
   - Configure quests and level requirements as needed
   - Set up permissions in your permission plugin (LuckPerms, etc.)

6. **Verify installation**
   - Check console for any errors
   - Test the `/clan` command
   - Verify language files are loaded in `plugins/ClansFix/languages/`

### Server Software Recommendations

**Best Choice: Paper**
- Better performance than Spigot
- More optimizations
- Active development
- Download: [PaperMC](https://papermc.io/downloads)

**Alternative: Spigot**
- Good performance
- Stable
- Download: [SpigotMC BuildTools](https://www.spigotmc.org/wiki/buildtools/)

**Not Recommended: Bukkit**
- Outdated
- No longer maintained
- Use Spigot/Paper instead

## Configuration

### Main Configuration (`config.yml`)

#### Language Settings
```yaml
language: en  # Available: ru, en, de, fr, es, pl
```

#### Member Settings
```yaml
members:
  default_max: 5  # Initial maximum members (level 1)
  per_level: 5    # Additional slots per clan level
```

#### Level Configuration
Each level can be configured with:
- `max_members` - Maximum members at this level
- `upgrade_cost` - Cost to upgrade to next level
- `quests` - List of quests required to upgrade

Quest types include:
- `KILL_PLAYERS` - Kill players
- `KILL_MOBS` - Kill mobs (specify `mob_type`)
- `COLLECT_ITEMS` - Collect items (specify `item`)
- `MINE_BLOCKS` - Mine blocks (specify `block`)
- `PLACE_BLOCKS` - Place blocks (specify `block`)
- `CATCH_FISH` - Catch fish
- `BREED_ANIMALS` - Breed animals (specify `mob_type`)
- `EAT_FOOD` - Eat food (specify `item`)
- `CRAFT_ITEMS` - Craft items (specify `item`)
- `PLANT_CROPS` - Plant crops (specify `block`)
- `TAME_ANIMALS` - Tame animals (specify `mob_type`)
- `TRAVEL_DISTANCE` - Travel distance
- `ENCHANT_ITEMS` - Enchant items
- `TRADE_WITH_VILLAGERS` - Trade with villagers
- `BREW_POTIONS` - Brew potions
- `SMELT_ITEMS` - Smelt items (specify `item`)
- `SHEAR_SHEEP` - Shear sheep
- `DEAL_DAMAGE` - Deal damage

### Language Files

Language files are located in `plugins/ClansFix/languages/`:
- `en.yml` - English (default)
- `ru.yml` - Russian
- `de.yml` - German
- `fr.yml` - French
- `es.yml` - Spanish
- `pl.yml` - Polish

All plugin texts can be customized in these files.



## Data Storage

Clan data is stored in YAML format in `plugins/ClansFix/clans/` directory. Each clan has its own file named after the clan name.

## GUI Menus

The plugin features a comprehensive GUI menu system:

### Clan Management Menu
- Clan information display
- Quick access to all features
- Member count and online status
- Clan statistics (kills, deaths, KDR, balance, ranking)

### Members Menu
- Paginated member list (21 per page)
- Member rank display
- Online/offline status
- Rank management (for Elders and leaders)

### Treasury Menu
- Deposit/withdraw interface
- Balance display
- Permission-based access

### Settings Menu
- Change clan name
- Change clan tag (color code)
- Toggle clan access (open/closed)
- Manage coat of arms
- Toggle holograms
- Toggle PvP between members
- Manage clan armor

### Ranking Menu
- Top clans display
- Composite score display
- Pagination support
- Special colors for top 3

### Upgrade Menu
- Current level display
- Quest progress
- Upgrade requirements

### Quest Menu
- All quests for current/next level
- Progress tracking
- Completion status

## Ranking Updates

Rankings are automatically updated every 5 minutes. The ranking system uses a composite score:

**Formula:** `Score = (KDR × 100) + (Balance ÷ 100)`

This means:
- KDR has higher priority (multiplied by 100)
- Balance also affects ranking (every 100$ adds 1 point)
- Top clans are determined by highest score

## Important Notes

### Clan Management
- Clan leaders cannot leave their clan (must delete it first)
- Clan tags can use Minecraft color codes (e.g., `&4` for red)
- Tags are optional when creating a clan (defaults to white `&f`)
- Tags don't need to be unique
- Clan names must be unique

### Permissions
- Only leaders and Elders can manage treasury withdrawals
- Only leaders and Elders can set/remove clan houses
- Only leaders and Elders can edit coat of arms
- Only leaders and Elders can invite players
- Only leaders and Elders can manage ranks
- Elders cannot kick other Elders (only leader can)
- Veterans and above can withdraw from treasury
- Trusted and above can access clan storage

### Data Management
- When a player leaves a clan, their holograms are automatically removed
- When a clan is deleted, all member holograms are removed
- Players can immediately create a new clan after leaving/deleting

### Localization
- Default language is English
- Change language in `config.yml`
- Use `/clan reload` to apply language changes
- All language files are automatically copied on first run

## Support

For issues or questions:
1. Check the plugin configuration
2. Ensure all dependencies are properly installed (ProtocolLib, Vault)
3. Check server logs for errors
4. Verify permissions are set correctly
5. Ensure language files are present in `plugins/ClansFix/languages/`

## Version Compatibility

### Supported Minecraft Versions
- ✅ **1.21** - Fully supported
- ✅ **1.21.1** - Fully supported
- ✅ **1.21.2** - Fully supported
- ✅ **1.21.3** - Fully supported
- ✅ **1.21.4** - Fully supported (tested)
- ✅ **1.22+** - Should work (forward compatible API)
- ❌ **1.20.x and below** - Not supported (requires 1.21+)

### Supported Server Software
- ✅ **Paper 1.21+** - Recommended (best performance)
- ✅ **Spigot 1.21+** - Fully supported
- ⚠️ **Bukkit 1.21+** - Not recommended (use Spigot/Paper)
- ❌ **Forge/NeoForge** - Not supported (Bukkit/Spigot only)
- ❌ **Fabric** - Not supported (Bukkit/Spigot only)

### Java Version Requirements
- ✅ **Java 21** (LTS) - Recommended
- ✅ **Java 22** - Supported
- ✅ **Java 23** - Supported
- ✅ **Java 24+** - Should work
- ❌ **Java 17** - Not supported (requires Java 21+)
- ❌ **Java 8/11** - Not supported

### Dependency Versions
- **ProtocolLib:** 5.3.0 or newer (required)
- **Vault:** Any version (required for economy)
- **PlaceholderAPI:** 2.11.6 or newer (optional)

### Testing Status
- ✅ Tested on Paper 1.21.4
- ✅ Tested with Java 21
- ✅ Tested with ProtocolLib 5.3.0
- ✅ Tested with Vault
- ✅ Tested with PlaceholderAPI 2.11.6

## Version

**Current Version:** 1.0.0

## Author

**fixsirt**

---

**Enjoy your advanced clan system!**
