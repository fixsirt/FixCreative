# ClansFix — Clan & Raid Plugin

> **Version:** 1.1.6  
> **Minecraft:** 1.21.x (Paper/Purpur)  
> **Dependencies:** PlaceholderAPI (optional), Vault (optional)

---

## 📋 Table of Contents

- [Commands](#-commands)
- [Permissions](#-permissions)
- [Clan System](#-clan-system)
- [Raid System](#-raid-system)
- [Language System](#-language-system)
- [Placeholders](#-placeholders)
- [Configuration](#-configuration)
- [Support](#-support)

---

## 🎮 Commands

### Player Commands (`/clan`)

| Command | Description | Permission |
|---------|-------------|------------|
| `/clan create <name>` | Create a clan | `clansfix.create` or payment |
| `/clan invite <player>` | Invite a player | `clansfix.invite` |
| `/clan kick <player>` | Kick a member | `clansfix.kick` |
| `/clan leave` | Leave your clan | `clansfix.leave` |
| `/clan join <clan>` | Join an open clan | — |
| `/clan deposit <amount>` | Deposit money into clan treasury | `clansfix.deposit` |
| `/clan chat <message>` | Send message to clan chat | `clansfix.chat` |
| `/clan info` | Your clan info | — |
| `/clan top` | Top clans ranking | — |
| `/clan stats` | Clan raid statistics | — |
| `/clan raids` | Open raid menu | — |
| `/clan reload` | Reload plugin config | `clansfix.reload` |

### Admin Commands

| Command | Description |
|---------|-------------|
| `/clan admin <clan>` | Open clan admin menu |
| `/clan transfer <player>` | Transfer clan ownership |
| `/clan delete` | Delete your clan |

---

## 🔑 Permissions

| Permission | Default | Description |
|------------|---------|-------------|
| `clansfix.create` | op | Create clan without payment |
| `clansfix.invite` | leader | Invite players |
| `clansfix.kick` | leader | Kick members |
| `clansfix.leave` | true | Leave clan |
| `clansfix.deposit` | member | Deposit to treasury |
| `clansfix.chat` | true | Use clan chat |
| `clansfix.reload` | op | Reload config |
| `clansfix.admin` | op | Admin panel |

### Rank Hierarchy

| Rank | Permissions |
|------|-------------|
| **Leader** | Full access — invite, kick, deposit, withdraw, settings, rename, delete, start raid |
| **Elder** | Invite, kick members, deposit, start raid |
| **Member** | Deposit, clan chat, participate in raids |
| **Novice** | Clan chat, basic participation |

---

## 🏰 Clan System

### Creating a Clan
- Use `/clan create <name>` to create a clan
- Name: 3–7 characters, letters and numbers only
- Cost: configured in `config.yml` (default 1000$, requires Vault)
- Alternative: `clansfix.create` permission bypasses payment

### Clan Treasury
- Members can deposit money via `/clan deposit <amount>`
- Balance is used for clan upgrades
- Withdraw requires leader/elder permissions

### Clan Management GUI
- `/clan` opens the main management menu with options:
  - **Info** — clan name, tag, level, members, KDR, balance, ranking
  - **House** — set/teleport to clan home
  - **Members** — manage member list
  - **Ranking** — combined ranking score
  - **Treasury** — deposit/withdraw
  - **Upgrades** — upgrade clan (max members, max moderators, house size, treasury limit)
  - **Storage** — shared clan storage
  - **Settings** — toggle open/closed, PvP, holograms, armor, tag color, coat of arms
  - **Raids** — raid menu
  - **Requests** — manage join requests

### Clan Holograms
- Displays clan name tag + coat of arms above each member's head
- Uses Minecraft 1.19.4+ TextDisplay & ItemDisplay entities
- Configurable offset, scale, background color
- Can be toggled per-clan in settings

### Clan Armor
- Visual armor that clan members can wear
- Customizable via GUI (helmet, chestplate, leggings, boots, offhand)
- Shows clan identity without affecting stats

### Ranking System
- Combined score = KDR × 100 + Balance ÷ 100 + Raid Points × Weight
- Viewable via `/clan top` or ranking GUI

---

## ⚔️ Raid System

### Overview
Infinite-wave raid system where players defend a core against waves of mobs. Each wave gets progressively harder. The raid ends when the core is destroyed or all participants leave.

### Starting a Raid
1. Leader/Elder opens `/clan` → **Raids** → **Start Raid**
2. A zone is created at the player's location
3. Initialization phase (configurable duration)
4. Waves begin automatically

### Raid Core
- **BlockDisplay** (BEACON block data) — visual core
- **Interaction** entity (4×4 hitbox) — right-click to open upgrade menu
- HP increases with each wave
- Mobs pathfind to and attack the core
- Core HP shown as TextDisplay above it

### Wave System
- **Base mobs:** configured per wave
- **Increment:** more mobs each wave
- **Boss interval:** every N waves a boss wave spawns
- **Mob scaling:** HP and damage increase per wave
- **Mob types:** Zombie, Skeleton, Spider, Creeper, Witch, Blaze, Wither Skeleton, Enderman, Cave Spider, Hoglin, Piglin, Vindicator, Magma Cube, Drowned, Husk
- **Boss types:** Wither Skeleton, Evoker, Elder Guardian, Ravager

### Raid End Conditions
- **Core destroyed** → raid ends, rewards distributed, all mobs removed
- **No participants** → raid ends automatically

### Raid Upgrades (via Shards)
Players earn **Shadow Shards** from killing raid mobs. Spend them in the core upgrade menu:

**Core Fortification:**
- **Max Health** — increases core max HP
- **Heal** — instantly heals core
- **Wave Shield** — damage reduction per wave

**Battle Buffs (apply to all participants):**
- **Resistance** — damage reduction
- **Strength** — increased damage
- **Speed** — movement speed boost
- **Haste** — mining speed boost
- **Regeneration** — health regen

**Tactical Abilities:**
- **Kill All** — instantly kills all raid mobs (consumes shards)
- **Highlight** — highlights all mobs with glowing effect (permanent)
- **Summon** — teleports all participants to the raid zone

### Raid Shards
- Dropped by mobs during raids
- Auto-pickup when walked over
- Used in the upgrade menu
- Persist for the duration of the raid

### Raid Rewards
- Configured in `config.yml` under `raids.rewards`
- Rewards are distributed when the core is destroyed
- Based on waves completed
- Can include commands, items, or money

### Raid Ranking
- Clans earn ranking points by participating in raids
- Points calculated from: participation, action points, kills
- Top clans shown in raid ranking menu
- Ranking points can be spent on... (to be implemented)

---

## 🌍 Language System

The plugin supports **7 languages** with full localization:

| Code | Language |
|------|----------|
| `en` | English |
| `ru` | Русский |
| `de` | Deutsch |
| `fr` | Français |
| `es` | Español |
| `pl` | Polski |
| `pt` | Português |

### Configuration

```yaml
# config.yml
language: en
per-player-locale: true
```

- `language` — default server language
- `per-player-locale: true` — auto-detects each player's client language
- When enabled, players with Russian client see Russian text, English client see English, etc.
- Falls back to `language` default if player's locale is not supported

### Color Palette

| Color | Code | Usage |
|-------|------|-------|
| Pink/Red | `#FF3366` | Headings, warnings, danger, 1st place |
| Cyan/Blue | `#00C8FF` | Values, numbers, success, 2nd place |
| White | `#F0F4F8` | Body text, descriptions |
| Purple | `#7000FF` | Accents, 3rd place, shards |

### Editing Translations
1. Edit files in `plugins/ClansFix/languages/*.yml`
2. Run `/clan reload`
3. Changes take effect immediately

---

## 📊 Placeholders (PlaceholderAPI)

| Placeholder | Description |
|-------------|-------------|
| `%clans_player_clan%` | Player's clan name |
| `%clans_player_tag%` | Player's clan tag (with color) |
| `%clans_player_level%` | Player's clan level |
| `%clans_player_kills%` | Player's clan total kills |
| `%clans_player_deaths%` | Player's clan total deaths |
| `%clans_player_kdr%` | Player's clan KDR |
| `%clans_player_balance%` | Player's clan treasury balance |
| `%clans_player_members%` | Player's clan member count |
| `%clans_player_online%` | Player's clan online members |
| `%clans_player_rank%` | Player's clan ranking position |
| `%clans_other_<player>_<stat>%` | Any player's clan stat |
| `%clans_top<pos>_<stat>%` | Top clan stat (position 1–10) |

**Supported stats:** `name`, `tag`, `kills`, `deaths`, `balance`, `level`, `members`, `online`, `kdr`

---

## ⚙️ Configuration

Full reference of `config.yml` sections:

### General
```yaml
clan_name:
  pattern: "^[a-zA-Zа-яА-Я0-9]{3,7}$"
  max_length: 7

clan_creation:
  enabled: true
  price: 1000.0
```

### Language
```yaml
language: en
per-player-locale: true
debug: false
```

### Clan Chat
```yaml
clan-chat-format: "<#00C8FF>&l[{clan}] <#00C8FF>%player%<#F0F4F8>: <#F0F4F8>%message%"
```

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
  
  # Raid upgrades configuration
  upgrades:
    fortification:
      max-health:
        levels:
          1: { cost: 50, hp: 100 }
          ...
    tactical:
      kill-all:
        levels:
          1: { cost: 100 }
          ...
    buffs:
      resistance:
        levels:
          1: { cost: 30, amplifier: 0, duration: 200 }
          ...
  
  rewards:
    1:
      display-name: "&aReward for 1 wave"
      commands:
        - "give %player% diamond 1"
  
  ranking:
    enabled: true
    weights:
      win: 1000.0
      points: 1.0
      kills: 5.0
      participation: 10.0
    combined-weight: 0.1
```

---

## 🆘 Support

| Platform | Link |
|----------|------|
| 📱 Telegram | [@Fixsirt](https://t.me/Fixsirt) |
| 💬 Discord | [Join Server](https://discord.com/invite/VTZhz2qYVb) |

---

## 📝 Notes

- All text colors are defined in language files — change them per-language
- Raid rewards support any console command via `%player%`, `%player_uuid%`, `%waves%`, `%raid_id%`
- Mob name format configurable: `"§8[§7Lvl.{level}§8] §7{type}"`
- Clan tags support Minecraft color codes (`&0`–`&f`) for colored tags

---

> **ClansFix** — developed by Fixsirt  
> *Last updated: June 2026*
