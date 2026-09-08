# ClansFix — Documentation

Clan system for **Paper 1.21+** (Java 21). Built as two (optionally three) plugins:

| Plugin | Purpose |
|---|---|
| **FixCore** | Core: API, database, services. Required dependency (the clan API is bundled dormant and is activated at ClansFix startup) |
| **ClansFix** | Main plugin: commands, GUI, clans, levels, quests, treasury, storage, houses, ranking |
| **ClansFixRaids** *(optional)* | Raid system: endless waves, raid core, Shadow Shards, in-raid upgrades |

---

## 1. Installation

1. Make sure the following plugins are installed on the server:
   - [ProtocolLib (SpigotMC)](https://www.spigotmc.org/resources/protocollib.1997/)
   - [PlaceholderAPI (SpigotMC)](https://www.spigotmc.org/resources/placeholderapi.6245/) — optional, required only for placeholders
   - Vault + an economy plugin — for paid clan creation (optional)
2. Put the following jars into the `plugins/` folder:
   - `FixCore.jar` (**required**, must load first — ensured by `depend`)
   - `ClansFix.jar`
   - `ClansFixRaids.jar` — only if you want raids
3. Restart the server.
4. Configure `plugins/ClansFix/config.yml` and `plugins/FixCore/config.yml`.

> On first startup FixCore automatically migrates data from an existing `plugins/ManagerFix/` folder (if present).

---

## 2. Commands

Main command: **`/clan`** (aliases: `/c`, `/cl`, `/clans`). Running `/clan` with no arguments opens the clan management menu.

| Command | Description |
|---|---|
| `/clan create <name>` | Create a clan (pays from balance or requires permission, configurable) |
| `/clan delete` | Disband the clan |
| `/clan join <name>` | Join a clan (if invitations/requests allow it) |
| `/clan leave` | Leave the clan |
| `/clan invite <player>` | Invite a player |
| `/clan accept <player>` | Accept an invitation |
| `/clan decline` | Decline an invitation/request |
| `/clan kick <player>` | Kick a member |
| `/clan house set` | Set the clan house at your current location |
| `/clan house tp` | Teleport to the clan house |
| `/clan deposit <amount>` | Deposit money into the treasury |
| `/clan treasury` | Open the treasury |
| `/clan storage` | Open the clan storage |
| `/clan upgrade` | Clan upgrade/level menu |
| `/clan top` / `/clan ranking` | Clan ranking |
| `/clan info` | Clan information |
| `/clan coat` / `/clan emblem` | Edit the coat of arms / emblem |
| `/clan tphere <player>` | Teleport a player to you (permission-gated) |
| `/clan admin` | Admin panel (clan list, editing) |
| `/clan reload` | Reload the config (`clansfix.reload`) |
| `/clan raids` | Raid management (see below) |

Some commands are gated by `clansfix.*` permissions or per-member clan permissions (`ClanPermission`).

---

## 3. Raids (ClansFixRaids)

| Command | Description |
|---|---|
| `/clan raids start` | Start a raid (cost is taken from the treasury; minimum clan level required) |
| `/clan raids join <id>` | Join an active raid |
| `/clan raids leave` | Leave the raid |
| `/clan raids info` / `/clan raids list` | List active raids (clan, wave, time, leader) |
| `/clan raids top` | Top clans by raid points |
| `/clan raids stats` | Your clan's raid stats |

How a raid works:
- The clan starts a raid at its own location; a countdown runs first (`initialization-time-minutes`).
- **Endless waves** of mobs spawn: each wave spawns more mobs that grow stronger (+10% HP, +5% damage per wave). Every 5th wave is a boss wave.
- The goal is to destroy the **raid core** (base 1000 HP, grows with waves).
- Mobs drop **Shadow Shards** — the in-raid currency.
- Shards are spent on in-raid upgrades:
  - **Battle buffs** — Resistance, Strength, Speed, Regeneration;
  - **Core fortification** — +HP, instant heal, wave shield;
  - **Tactical** — Kill-All (clear all mobs), highlighting, summons.
- Completing waves grants **rewards** (configurable commands, `rewards` in config).
- Raid points/wins feed a separate **raid ranking** (`/clan raids top`).

Settings: `raids.*` in `plugins/ClansFix/config.yml` (cost, radius, waves, core, upgrades, rewards, ranking).

---

## 4. Levels and quests

- A clan has a level from **1 to 5** (configurable under `levels.*`).
- The member limit grows with level: `5 / 10 / 15 / 20 / 25`.
- Level up via `/clan upgrade`; costs money from the treasury (`upgrade_cost`).
- To reach levels 2, 3 and 4 the clan must complete **quests** (kills, gathering, mining, crafting, cooking, fishing, taming, building, trading, ...).

---

## 5. Treasury, storage, house

- **Treasury** — shared clan money; deposit via `/clan deposit`, spent on upgrades and raids.
- **Storage** — a shared 54-slot inventory. It is "live": if several players are viewing it, they all see the same actual contents (dupe protection).
- **Clan house** — set by the leader (`/clan house set`), teleport via `/clan house tp`.

---

## 6. Extra mechanics

- **Clan chat** — a separate channel; format configurable (`clan-chat-format`).
- **Holograms** above players: clan tag + level (TextDisplay) and coat of arms (ItemDisplay) — enable/configure under `holograms.*`.
- **Clan armor** — special named items.
- **Friendly fire** — configurable damage between clan members.
- **Auto-save** — periodic save of all clans (`performance.periodic-save-interval-ticks`).

---

## 7. PlaceholderAPI

Placeholder prefix: **`clans`** (`clansfix_*` variants work too).

| Placeholder | Value |
|---|---|
| `%clans_player_clan%` | Player's clan name |
| `%clans_player_tag%` | Clan tag (color codes) |
| `%clans_player_level%` | Clan level (superscript, e.g. ²) |
| `%clans_player_kills%` / `%clans_player_deaths%` | Clan kills / deaths |
| `%clans_player_kdr%` | Clan K/D |
| `%clans_player_balance%` | Clan balance |
| `%clans_player_members%` | Total members |
| `%clans_player_online%` | Online members |
| `%clans_player_rank%` | Clan position in the ranking |
| `%clans_other_<name>_clan%` | Another player's clan (also `tag`, `level`, `kills`, `rank`, ...) |
| `%clans_top<N>_name%` | Nth clan in the top (also `top1_tag`, `top10_kdr`, `top1_balance`, ...) |
| `%clans_top_<N>_<type>_name%` | Top by type: `overall`, `kills`, `balance`, `level`, `members` |

Example scoreboard: `%clans_player_tag%%clans_player_level% — %clans_player_clan%`.

---

## 8. Permissions

| Permission | Description | Default |
|---|---|---|
| `clansfix.*` | All permissions | op |
| `clansfix.admin` | Admin panel | op |
| `clansfix.create` | Create a clan (paid/free) | false |
| `clansfix.create.free` | Create a clan for free | op |
| `clansfix.join` | Join clans | true |
| `clansfix.leave` | Leave a clan | true |
| `clansfix.invite` | Invite players | true |
| `clansfix.kick` | Kick members | true |
| `clansfix.house` | Manage the clan house | true |
| `clansfix.treasury` | Manage the treasury | true |
| `clansfix.upgrade` | Upgrade the clan | true |
| `clansfix.rank` | View ranking | true |
| `clansfix.reload` | Reload the plugin | op |

---

## 9. Common settings (`plugins/ClansFix/config.yml`)

- `clan_name.pattern` / `max_length` — clan name pattern and max length (default: letters+digits, 3–7).
- `clan_creation.price` — clan creation cost (`-1` = permission only).
- `language` / `per-player-locale` — language (ru, en, de, fr, es, pl, pt) and per-client auto-detection.
- `members.default_max` / `per_level` — base member limit and the bonus per level.
- `levels.*` — levels: member limits, cost, quests.
- `holograms.*` — overhead widget.
- `performance.*` — async saving, save intervals.
- `web.*` — web editor (port 18200, default password `admin123` — **change it**).

---

## 10. Links and build

- Source code: `D:\plagins\remake_clans_fix\ClansFixSplit`
- Ready jars: `build/` folder and each module's `target/` folder.
- Build: `mvnw.cmd -f pom.xml clean install` (JDK 21 required).
- Dependencies: [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/), [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/).

> **Important:** FixCore is a universal core (namespace `ru.managerfix.*` + the dormant clan API `com.clansfix.*`). It serves both the **ManagerFix** modules and clans. Do not rename or remove FixCore — ClansFix will not start without it.
