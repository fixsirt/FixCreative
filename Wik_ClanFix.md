# ClansFix — Clan & Raid Plugin

> **Version:** 1.1.7  
> **Minecraft:** 1.21.x (Paper/Purpur)  
> **Dependencies:** PlaceholderAPI (optional), Vault (optional)

---

## 📋 Table of Contents

- [Installation](#-installation)
- [Commands](#-commands)
- [Permissions](#-permissions)
- [Clan System](#-clan-system)
- [Raid System](#-raid-system)
- [GUI System](#-gui-system)
- [Language System](#-language-system)
- [Placeholders](#-placeholders)
- [Configuration](#-configuration)
- [Troubleshooting](#-troubleshooting)
- [Support](#-support)

---

## 📦 Installation

1. Download `ClansFix-1.1.7.jar`
2. Place it in your server's `plugins/` folder
3. Restart the server (or use PlugManX to load)
4. Edit `plugins/ClansFix/config.yml` to your liking
5. Change language files in `plugins/ClansFix/languages/` if needed
6. Run `/clan reload` to apply changes without a restart

### First-Time Setup

```yaml
# config.yml — essential settings to review:
language: ru                    # Server default language
per-player-locale: true         # Auto-detect player language from client
clan_creation:
  enabled: true
  price: 1000.0                 # Requires Vault
raids:
  enabled: true
  cost: 10000.0
```

### Updating from Older Versions

1. Replace the JAR
2. **Delete** old language files from `plugins/ClansFix/languages/` — new ones will be extracted from the JAR
3. Run `/clan reload` or restart

---

## 🎮 Commands

### Player Commands (`/clan`)

| Command | Description | Permission |
|---------|-------------|------------|
| `/clan` | Open clan management GUI | — |
| `/clan create <name> <color>` | Create a clan (name + color tag) | `clansfix.create` or payment |
| `/clan invite <player>` | Invite a player | `clansfix.invite` |
| `/clan kick <player>` | Kick a member | `clansfix.kick` |
| `/clan leave` | Leave your clan | `clansfix.leave` |
| `/clan join <clan>` | Join an open clan | — |
| `/clan deposit <amount>` | Deposit money into clan treasury | `clansfix.deposit` |
| `/clan chat <message>` | Send message to clan chat | `clansfix.chat` |
| `/clan info [clan]` | Your clan info (or another clan) | — |
| `/clan top` | Top clans ranking | — |
| `/clan stats` | Clan raid statistics (waves, points) | — |
| `/clan raid` | Open raid menu | — |
| `/clan raid info <id>` | Info about a specific raid | — |
| `/clan raid top` | Raid ranking leaderboard | — |
| `/clan raid stats` | Your clan's raid statistics | — |
| `/clan reload` | Reload plugin config | `clansfix.reload` |
| `/clan admin <clan>` | Open clan admin menu | `clansfix.admin` |
| `/clan transfer <player>` | Transfer clan ownership | — |
| `/clan delete` | Delete your clan (leader only) | — |
| `/clan tphere <clan>` | Teleport all clan members to you | `clansfix.tphere` |

### Admin Commands

| Command | Description |
|---------|-------------|
| `/clan admin <clan>` | Open clan admin panel |
| `/clan reload` | Reload all configs and language files |

---

## 🔑 Permissions

| Permission | Default | Description |
|------------|---------|-------------|
| `clansfix.create` | op | Create clan without payment |
| `clansfix.invite` | leader | Invite players |
| `clansfix.kick` | leader | Kick members |
| `clansfix.leave` | true | Leave clan |
| `clansfix.deposit` | member | Deposit to treasury |
| `clansfix.withdraw` | elder | Withdraw from treasury |
| `clansfix.chat` | true | Use clan chat |
| `clansfix.reload` | op | Reload config |
| `clansfix.admin` | op | Admin panel access |
| `clansfix.tphere` | op | Teleport clan members |

### Rank Hierarchy

| Rank | Permissions |
|------|-------------|
| **Leader** | Full access — invite, kick, deposit, withdraw, settings, rename, delete, start raid, manage permissions |
| **Elder** | Invite, kick members, deposit, withdraw, start raid |
| **Trusted** | Deposit, invite |
| **Member** | Deposit, clan chat, participate in raids |
| **Novice** | Clan chat, basic participation |

### Fine-Grained Permissions

Each rank can have individual permissions configured via the in-game permissions GUI:

| Permission Node | Description |
|----------------|-------------|
| `treasury_deposit` | Can deposit money |
| `treasury_withdraw` | Can withdraw money |
| `set_home` | Can set clan home |
| `teleport_home` | Can teleport to home |
| `delete_home` | Can delete home |
| `access_storage` | Can open clan storage |
| `manage_invitations` | Can invite players |
| `manage_requests` | Can handle join requests |
| `start_raid` | Can start a raid |
| `kick_member` | Can kick members |
| `edit_permissions` | Can edit rank permissions |
| `upgrade_clan` | Can upgrade the clan |
| `change_coat_of_arms` | Can change coat of arms |
| `change_name` | Can rename the clan |
| `change_open_closed` | Can toggle open/closed |
| `change_armor` | Can change clan armor |
| `change_pvp` | Can toggle clan PvP |
| `change_tag` | Can change color tag |
| `toggle_holograms` | Can toggle holograms |

---

## 🏰 Clan System

### Creating a Clan
- Use `/clan create <name> <color>` to create a clan
  - Example: `/clan create Dragons &4`
  - `name`: 3–7 characters, letters/numbers only
  - `color`: Minecraft color code (`&0`–`&f`)
- Cost: configured in `config.yml` (default 1000$, requires Vault)
- Permission `clansfix.create` bypasses payment

### Clan Colors (Tag)
- The `tag` parameter in `/clan create` is a Minecraft **color code**
- Common tags: `&4` (dark red), `&b` (aqua), `&e` (yellow), `&a` (green)
- Can be changed later in clan settings
- The tag color is applied to the clan name wherever it appears

### Clan Treasury
- `/clan deposit <amount>` — members can deposit money
- Balance used for clan upgrades and raid costs
- Withdraw requires elder+ permission
- Treasury limit scales with clan level

### Clan Management GUI
- `/clan` opens the main management menu with options:

| Slot | Option | Description |
|------|--------|-------------|
| 12 | **House** | Set/teleport to clan home |
| 13 | **Info** | Name, members, KDR, balance, ranking |
| 14 | **Sword** | Raid menu |
| 19 | **Storage** | Shared clan storage (54 slots) |
| 21 | **Upgrades** | Level up, increase members/size |
| 23 | **Treasury** | Deposit/withdraw money |
| 25 | **Members** | Manage roster, ranks, permissions |
| 28 | **Ranking** | Clan rankings leaderboard |
| 30 | **Settings** | Toggle open/closed, PvP, holograms, rename, tag color |
| 32 | **Requests** | Accept/reject join requests |
| 34 | **Raids** | Raid menu |
| 40 | **Leave/Delete** | Leave clan (non-leader) or delete (leader) |

### Clan Holograms
- Displays clan name tag + coat of arms above each member
- Uses Minecraft 1.19.4+ TextDisplay & ItemDisplay entities
- Configurable offset, scale, background (see `config.yml`)
- Per-clan toggle in settings menu

### Clan Armor
- Visual armor worn by clan members
- Customizable via GUI (helmet, chestplate, leggings, boots, offhand)
- Cosmetic only — does not affect stats
- Can be toggled per-clan

### Ranking System
- Combined score formula: `KDR × 100 + Balance ÷ 100 + Raid Points × Weight`
- Viewable via `/clan top` or ranking GUI
- Clan level increases with XP (from raiding, quests)

### Clan Storage
- 54-slot shared inventory accessible to all members with permission
- Title format: `"Clan Storage - {name}"` (configurable in language files)
- Players can deposit/withdraw items based on their permissions

---

## ⚔️ Raid System

### Overview
Infinite-wave PvE raid system. Players defend a BEACON core against waves of mobs inside a protected zone. Each wave gets harder — more mobs, more HP, more damage. The raid ends when the core is destroyed or all participants leave.

### Starting a Raid
1. Leader/Elder opens `/clan` → **Raids** → **Start Raid**
2. Right-click the BEACON Interaction entity after it spawns
3. Zone is created at the starter's location (configurable radius)
4. Initialization phase (default 3 minutes) — members can join
5. Waves begin automatically after initialization

### Requirements
- Clan level ≥ `min-clan-level` (default 1)
- Online members ≥ `min-online-players` (default 1)
- Treasury balance ≥ `cost` (default 10,000$)
- Server-wide: max concurrent raids ≤ `max-active-raids` (default 5)
- Cooldown between raids: `cooldown-hours` (default 24)

### Raid Core
- **Visual:** BlockDisplay entity with BEACON block data
- **Hitbox:** Interaction entity (4×4 block selection box)
- **Interaction:** Right-click to open upgrade menu
- **HP:** Base HP + per-wave increase
- **Label:** TextDisplay above core showing current HP
- **Behavior:** Mobs pathfind to and attack the core

### Wave System

| Parameter | Default | Description |
|-----------|---------|-------------|
| `mobs-per-wave-base` | 10 | Starting mob count |
| `mobs-per-wave-increment` | 3 | Extra mobs per wave |
| `boss-interval` | 5 | Boss wave every N waves |
| `max-alive-mobs` | 30 | Cap on concurrent mobs |
| `health-per-wave` | 0.1 | +10% mob HP per wave |
| `damage-per-wave` | 0.05 | +5% mob damage per wave |

**Mob types:** Zombie, Skeleton, Spider, Creeper, Witch, Blaze, Wither Skeleton, Enderman, Cave Spider, Hoglin, Piglin, Vindicator, Magma Cube, Drowned, Husk, Ghast

**Boss types:** Wither Skeleton, Evoker, Elder Guardian, Ravager

### Raid End Conditions

| Condition | Result |
|-----------|--------|
| **Core destroyed** | Raid ends — rewards distributed, all mobs removed, final broadcast |
| **No participants** | Raid ends automatically after a timeout |
| **All waves cleared** | Continuous waves until core breaks — no "win" state |

### Raid Stats
Each clan tracks raid statistics:

| Stat | Description |
|------|-------------|
| `totalRaidWaves` | Total waves survived across all raids |
| `maxRaidWave` | Highest wave ever reached |
| `raidPoints` | Cumulative raid points earned |
| `totalRaids` | Number of raids participated in |
| `firstPlaces` | 1st place finishes |
| `secondPlaces` | 2nd place finishes |
| `thirdPlaces` | 3rd place finishes |

### Raid Upgrades (via Shards)

Earn **Shadow Shards** by killing raid mobs (auto-pickup). Spend them in the core upgrade menu to help your team survive longer.

#### Core Fortification
| Upgrade | Effect |
|---------|--------|
| **Max Health** | Permanently increases core max HP |
| **Heal Core** | Instantly heals the core |
| **Wave Shield** | Reduces incoming damage per wave |

#### Battle Buffs (apply to all participants)
| Buff | Effect |
|------|--------|
| **Resistance** | Damage reduction |
| **Regeneration** | Health regen |
| **Strength** | Increased attack damage |
| **Speed** | Movement speed boost |

#### Tactical Abilities
| Ability | Effect | Cost |
|---------|--------|------|
| **Kill All** | Instantly kills all alive raid mobs | Shards |
| **Highlight** | Permanently glows all mobs | Shards |
| **Summon Clan** | Teleports all members to raid zone | Shards |

### Raid Shards
- Dropped by mobs during active raids
- Auto-collected when walked over
- Persist for the duration of the raid (lost at end)
- Displayed in the action bar and core upgrade menu

### Raid Rewards
Configured in `config.yml` `raids.rewards` section. Supports:
- Console commands (`%player%`, `%waves%`, `%raid_id%`)
- Item rewards (via commands)
- Money rewards

### Raid Ranking
- Clans earn ranking points based on participation
- Point calculation: kills, participation time, action points
- Leaderboard accessible via `/clan raid top`
- Rank shown on clan info

### Raid Mob AI
- Mobs use Pathfinder goals to reach the core
- No look-at-player behavior (mobs focus on core)
- 3-tick update cycle for performance
- Custom damage scaling per wave

### Raid Boss Bar
- Shows initialization countdown: `"Initializing: {time} | Core: {core} HP"`
- Active phase: `"Wave {wave} | {killed}/{total} | Core: {core}/{maxcore} | {shards}"`
- Color changes: Yellow (initializing) → Red (active)

---

## 🖥️ GUI System

### Inventory Click Handling
All ClansFix menus use **slot-based** click handling — no material checks. This means:

✓ Button materials can be freely changed in `gui_layouts.yml` without breaking functionality  
✓ Material changes via resource packs or server updates don't break menus  
✓ Sound (`UI_BUTTON_CLICK`) plays on every slot click (not on glass panes)

### Exceptions (Material Checks)
A few conflict slots still use material checks:
- **Slot 40:** BARRIER (leave clan) vs LAVA_BUCKET (delete clan)
- **PLAYER_HEAD:** Invite player menu buttons
- **Slot 40:** COMPASS/BARRIER/ARROW in MembersMenu

### GUI Layout Configuration (`gui_layouts.yml`)
All menu layouts are fully configurable via `plugins/ClansFix/gui_layouts.yml`.  
Change button positions, materials, or disable entire menus.

> After any change, run `/clan reload` to apply.

#### Structure
```yaml
menu_key:
  enabled: true                    # false = entire menu disabled
  slots:
    slot_number: MATERIAL          # simple format
    slot_number:                   # nested format
      enabled: false               # hide this specific button
      material: MATERIAL
```

#### Decorative Items
```yaml
decorative:
  enabled: true                    # false = no glass panes
  border: BLUE_STAINED_GLASS_PANE
  fill: LIGHT_BLUE_STAINED_GLASS_PANE
  accent: LIGHT_BLUE_STAINED_GLASS_PANE
  soft: LIGHT_BLUE_STAINED_GLASS_PANE
  decorative: BLUE_STAINED_GLASS_PANE
```

#### Menu Keys Reference
| Key | Menu | Java Class |
|-----|------|------------|
| `clan_management` | Main clan menu (`/clan`) | ClanManagementMenu |
| `raid_menu` | Raid menu | RaidMenu |
| `raid_ranking` | Raid ranking | RaidRankingMenu |
| `raid_upgrade` | Raid upgrade menu | RaidUpgradeMenu |
| `raid_core_sub` | Core upgrades | RaidCoreSubMenu |
| `raid_buff_sub` | Battle buffs | RaidBuffSubMenu |
| `raid_tactical_sub` | Tactical abilities | RaidTacticalSubMenu |
| `clan_settings` | Clan settings | ClanSettingsMenu |
| `clan_stats` | Raid stats | ClanRaidStatsMenu |
| `active_raids` | Active raids list | ActiveRaidsMenu |
| `armor_menu` | Clan armor editor | ClanArmorMenu |
| `members_menu` | Members list | MembersMenu |
| `invite_player` | Invite player | InvitePlayerMenu |
| `treasury` | Treasury | TreasuryMenu |
| `upgrade_menu` | Clan upgrades | UpgradeMenu |
| `clan_ranking` | Rankings | RankingMenu |
| `confirmation` | Confirm dialogs | ConfirmationMenu |
| `invitations` | Invitations | InvitationsMenu |
| `my_invitations` | My invitations | MyInvitationsMenu |
| `clan_requests` | Join requests | ClanRequestsMenu |
| `clan_list` | Clan list | ClanListMenu |
| `admin_clan_list` | Admin clan list | AdminClanListMenu |
| `tphere_clan_list` | TP-here clan list | TpHereClanListMenu |
| `permissions` | Permissions editor | PermissionsMenu |
| `coat_of_arms` | Coat of arms | CoatOfArmsMenu |
| `clan_storage` | Clan storage | ClanStorageMenu |
| `quests` | Quests | QuestsMenu |

#### Examples

**Disable entire raid menu:**
```yaml
raid_menu:
  enabled: false
```

**Change sword to nether star:**
```yaml
clan_management:
  slots:
    34: NETHER_STAR
```

**Hide the clan house button:**
```yaml
clan_management:
  slots:
    12:
      enabled: false
      material: GOLDEN_AXE
```

**Change all glass to purple:**
```yaml
decorative:
  border: PURPLE_STAINED_GLASS_PANE
  fill: PURPLE_STAINED_GLASS_PANE
```

**Remove all decorative glass:**
```yaml
decorative:
  enabled: false
```

---

## 🌍 Language System

The plugin supports **7 languages** with full localization. Every text message, menu title, and button label is configurable per language.

| Code | Language |
|------|----------|
| `en` | English |
| `ru` | Русский |
| `de` | Deutsch |
| `fr` | Français |
| `es` | Español |
| `pl` | Polski |
| `pt` | Português |

### How Languages Work (Priority Order)

1. **Player language** (if `per-player-locale: true`) — detected from the Minecraft client locale setting
2. **Server default** (`language` in `config.yml`)
3. **Fallback to English** — if a key doesn't exist in the active language, English is used

### Placeholder Variables

All language files support `{variable}` placeholders that are replaced at runtime:

| Variable | Description | Example Keys |
|----------|-------------|-------------|
| `{name}` | Clan name | `commands.clan.create.name`, `messages.joined_clan_name` |
| `{tag}` | Color tag | `commands.clan.create.tag`, `menus.clan_list.clan_item.tag` |
| `{clan}` | Clan name (contextual) | `commands.clan.invite.received_message` |
| `{player}` | Player name | Various permission/invite messages |
| `{rank}` | Player's rank | Ranking, permission messages |
| `{level}` | Clan level | Upgrade info, raid requirements |
| `{count}` | Count/number | Member count, invitation count |
| `{position}` | Ranking position | Ranking list entries |
| `{price}` | Money amount | Creation cost, upgrade cost |
| `{balance}` | Treasury balance | Treasury info |
| `{wave}` | Current wave | Raid info |
| `{total}` | Total count | Pagination, wave display |
| `{color}` | Color code prefix | In raid health format |

### Editing Translations

1. Edit files in `plugins/ClansFix/languages/*.yml`
2. Run `/clan reload`
3. Changes take effect immediately

> ⚠️ **Important:** If you update the plugin JAR, **delete** old language files from the languages folder. The plugin will extract fresh defaults from the new JAR. Old files can contain stale keys or missing placeholders.

### Color Palette

| Color | Code | Usage |
|-------|------|-------|
| Pink/Red | `#FF3366` | Headings, warnings, danger, 1st place |
| Cyan/Blue | `#00C8FF` | Values, numbers, success, 2nd place |
| White | `#F0F4F8` | Body text, descriptions |
| Purple | `#7000FF` | Accents, 3rd place, shards |

Colors are defined in `ColorUtil.Palette` and used throughout all language files. Change them globally or per-key.

---

## 📊 Placeholders (PlaceholderAPI)

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `%clans_player_clan%` | Player's clan name | `Dragons` |
| `%clans_player_tag%` | Player's clan tag (color code) | `&4` |
| `%clans_player_level%` | Player's clan level | `5` |
| `%clans_player_kills%` | Clan total kills | `1234` |
| `%clans_player_deaths%` | Clan total deaths | `567` |
| `%clans_player_kdr%` | Clan KDR | `2.17` |
| `%clans_player_balance%` | Clan treasury balance | `50000.0` |
| `%clans_player_members%` | Clan member count | `15` |
| `%clans_player_online%` | Online members | `3` |
| `%clans_player_rank%` | Clan ranking position | `#1` |
| `%clans_player_raid_points%` | Raid points | `2500` |
| `%clans_player_total_waves%` | Total waves survived | `47` |
| `%clans_player_max_wave%` | Highest wave reached | `12` |
| `%clans_other_<player>_<stat>%` | Any player's stat | `%clans_other_Notch_kills%` |
| `%clans_top<1-10>_<stat>%` | Top clan stat | `%clans_top1_name%` |

**Supported stats for top/other:** `name`, `tag`, `kills`, `deaths`, `balance`, `level`, `members`, `online`, `kdr`, `raid_points`, `total_waves`, `max_wave`

---

## ⚙️ Configuration

Full reference of `plugins/ClansFix/config.yml`:

### General
```yaml
clan_name:
  pattern: "^[a-zA-Zа-яА-Я0-9]{3,7}$"
  max_length: 7

clan_creation:
  enabled: true
  price: 1000.0

clan:
  max-members-base: 10
  max-members-per-level: 5
  max-moderators-base: 3
  house-tp-cooldown-seconds: 10
```

### Language & Debug
```yaml
language: en
per-player-locale: true
debug: false
```

### Clan Chat
```yaml
clan-chat-format: "<#00C8FF>&l[{clan}] <#00C8FF>%player%<#F0F4F8>: <#F0F4F8>%message%"
```
Available variables: `{clan}`, `{player}`, `{message}`, `{rank}`

### Performance
```yaml
performance:
  save-clan-async: true
  periodic-save-interval-ticks: 6000
```

### Holograms
```yaml
holograms:
  enabled: true
  display:
    tag:
      offset-y: 2.4
      scale: 1.0
      background:
        color: '#000000'
    coat:
      offset-y: 2.7
      scale: 0.5
```

### Raids
```yaml
raids:
  enabled: true
  cost: 10000.0
  initialization-minutes: 3
  radius: 25
  min-clan-level: 1
  min-online-players: 1
  cooldown-hours: 24
  max-active-raids: 5

  waves:
    mobs-per-wave-base: 10
    mobs-per-wave-increment: 3
    boss-interval: 5
    max-alive-mobs: 30
    health-per-wave: 0.1
    damage-per-wave: 0.05

  core:
    base-health: 1000
    health-per-wave: 50

  upgrades:
    fortification:
      max-health:
        levels:
          1: { cost: 50, hp: 100 }
          2: { cost: 100, hp: 200 }
          3: { cost: 200, hp: 400 }
      heal:
        levels:
          1: { cost: 30, heal-percent: 25 }
          2: { cost: 60, heal-percent: 50 }
          3: { cost: 100, heal-percent: 100 }
    tactical:
      kill-all:
        levels:
          1: { cost: 100 }
      highlight:
        levels:
          1: { cost: 50 }
      summon:
        levels:
          1: { cost: 75 }
    buffs:
      resistance:
        levels:
          1: { cost: 30, amplifier: 0, duration: 200 }
          2: { cost: 50, amplifier: 1, duration: 200 }
      regeneration:
        levels:
          1: { cost: 30, amplifier: 0, duration: 200 }
      strength:
        levels:
          1: { cost: 30, amplifier: 0, duration: 200 }
      speed:
        levels:
          1: { cost: 20, amplifier: 0, duration: 400 }

  rewards:
    1:
      display-name: "&aReward for 1 wave"
      commands:
        - "give %player% diamond 1"
    5: { display-name: "...", commands: [...] }
    10: { display-name: "...", commands: [...] }

  ranking:
    enabled: true
    weights:
      points: 1.0
      kills: 5.0
    combined-weight: 0.1
```

---

## 🔧 Troubleshooting

### Common Issues & Solutions

| Symptom | Cause | Fix |
|---------|-------|-----|
| `{name}` / `{tag}` / `{rank}` appears literally in chat | Stale language file on disk | Delete `plugins/ClansFix/languages/*.yml` and reload |
| YAML parse error on startup | Corrupted language file | Delete the broken `.yml` file, restart — fresh copy extracted from JAR |
| Clan menu shows wrong materials | `gui_layouts.yml` has wrong slot | Check slot numbers in `gui_layouts.yml` |
| Slot 40 doesn't work (leave/delete) | `gui_layouts.yml` overrides slot 40 | Remove `40:` from `gui_layouts.yml` for `clan_management` |
| Per-player locale not working | Player language not detected | Requires Paper 1.21+; player must have correct client locale |
| Raid shards not appearing | Mobs not dropping | Check `raids.shards.enabled` in config |
| Placeholders not working | PlaceholderAPI not installed | Install PlaceholderAPI, restart |
| `/clan reload` doesn't apply language changes | Outdated disk cache | Disk language files take priority over JAR defaults |
| Clan chat format shows raw variables | Old config.yml | Check `clan-chat-format` uses `{clan}` not `{tag}` |

### Debug Mode
Set `debug: true` in `config.yml` to see detailed error output in console. Useful for:
- Identifying missing language keys
- Tracing placeholder replacements
- Debugging raid initialization issues

### YAML Validation
If you edit language files manually and get parse errors:
1. Use a YAML validator (e.g., `yamllint.com`)
2. Check for unclosed quotes (`"`) 
3. Check indentation consistency (spaces only, no tabs)
4. Run `/clan reload` — the error log will tell you which file and line

---

## 📝 Developer Notes

- All text colors are defined in `ColorUtil.Palette` — change them globally
- Language files are loaded from disk first, then JAR defaults as fallback
- Menu button handling is slot-based (not material-based) for `gui_layouts.yml` compatibility
- Color codes support: `&` legacy, `<#RRGGBB>` hex, `<gradient:...>` gradients
- Raid mobs use Paper's pathfinder API — no custom NMS
- Interaction entities (raid core) require Minecraft 1.19.4+

---

## 🆘 Support

| Platform | Link |
|----------|------|
| 📱 Telegram | [@Fixsirt](https://t.me/Fixsirt) |
| 💬 Discord | [Join Server](https://discord.com/invite/VTZhz2qYVb) |

---

> **ClansFix** — developed by Fixsirt  
> *Last updated: June 2026*
