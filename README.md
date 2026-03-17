# SingleRSC Website

The official website for **RSC Single Player** — a fully self-contained RuneScape Classic sandbox that runs entirely offline on Desktop and Mobile. No server, no database, no internet required.

---

## Downloads

| Platform | Version | Link |
| --- | --- | --- |
| **Desktop** (Windows/macOS/Linux) | v2.4.6 | [Single-RSC-v2.4.6.zip](https://github.com/theKennethy/Single-RSC/releases/download/v2.4.6/Single-RSC-v2.4.6.zip) |
| **Mobile** (Android 7.0+) | v2.5.3 | [Single-RSC.apk](https://github.com/theKennethy/SingleRSC-Mobile/releases/download/v2.5.3/Single-RSC.apk) |

---

## Features

### Core

- 100% single-process design — no external DB, server, or internet required
- All core content including all 50 quests
- 18-skill bot system with auto-banking and combat support
- Batched skill actions (woodcutting, mining, cooking, etc.) using a tick-based batch system
- Resizable UI — drag to any window size (desktop) / pinch zoom (mobile)
- Full music — 55 MIDI tracks mapped to game regions
- Dynamic login screen
- Multi-account capable
- 8x XP multiplier (configurable 1x-50x in source)
- Hardcore mode — death permanently deletes your save

### Quality of Life

- `::bank` — open bank from anywhere
- `::tele <area>` — teleport to named locations or coordinates
- `::stuck` — unstick your character
- Right-click item swapping in the bank interface
- Bob's Axes stocks hatchets (Bronze through Rune) and pickaxes (Bronze through Rune)

---

## Quick Start

### Desktop (Java 17+)

```bash
git clone https://github.com/theKennethy/Single-RSC.git
cd Single-RSC
./run.sh        # Linux/macOS
run.bat         # Windows
```

Or: `java -cp "rsc.jar:lib/*" org.nemotech.rsc.Main`

### Mobile (Android 7.0+, ~6 MB)

1. Download [Single-RSC.apk](https://github.com/theKennethy/SingleRSC-Mobile/releases/download/v2.5.3/Single-RSC.apk)
2. Install (enable "Install from unknown sources" if needed)
3. Launch and create an account

---

## Mobile Touch Controls

| Gesture | Action |
| --- | --- |
| Tap | Left click (walk, interact, select) |
| Long press | Right click (context menu, examine) |
| Double tap | Toggle on-screen keyboard |
| Pinch out/in | Zoom in / zoom out |
| Two-finger drag | Rotate camera |

---

## Commands

### Player Commands

| Command | Description |
| --- | --- |
| `::help` | Show help message |
| `::bank` | Open bank anywhere |
| `::stuck` | Unstick your character |
| `::pos` | Show current coordinates |
| `::toggleroofs` | Toggle roof rendering on/off |
| `::mapedit` | Open the real-time map editor |

### Admin Commands (user: `root`)

| Command | Description |
| --- | --- |
| `::tele <location>` | Teleport to a named location |
| `::tele <x> <y>` | Teleport to coordinates |
| `::item <id> [amount]` | Spawn an item |
| `::npc <id>` | Spawn an NPC |
| `::object <id> [dir]` | Spawn an object |
| `::set <skill> <level>` | Set a skill level |
| `::addbank <id> [amount]` | Add item to bank |
| `::removebank <id> [amount]` | Remove item from bank |
| `::quest <id> <stage>` | Set quest stage |
| `::find <entity> <string>` | Search for entities by name |
| Mini-map right-click | Teleport to clicked location |

> **Tip:** Create a user named exactly `root` (case-sensitive) to unlock all admin commands.

---

## Bot System

A built-in bot framework that automates training for all 18 skills. Bots handle banking, eating, and resource management automatically.

### Bot Management

| Command | Description |
| --- | --- |
| `::bot list` | List all registered bots |
| `::bot start <name>` | Start a bot by name |
| `::bot stop [name]` | Stop a bot (or all bots) |
| `::bot pause` | Pause / resume the active bot |
| `::bot status` | Show status of all bots |

### Gathering Bots

| Command | Skill | Types |
| --- | --- | --- |
| `::woodcut [type]` | Woodcutting | normal, oak, willow, maple, yew, magic |
| `::fish [type]` | Fishing | net, fly, cage, harpoon, shark |
| `::mine [type]` | Mining | copper, tin, iron, coal, gold, mith, addy, rune |

### Combat Bots

| Command | Skill | Details |
| --- | --- | --- |
| `::combat [npc]` | Attack/Strength/Defence | Melee combat with auto-looting |
| `::ranged [npc]` | Ranged | Ranged combat training |
| `::magic [npc]` | Magic | Casts combat spells on NPCs |

### Production Bots

| Command | Skill | Details |
| --- | --- | --- |
| `::cook` | Cooking | Cooks raw food on ranges |
| `::fm` | Firemaking | Burns logs with tinderbox |
| `::smith` | Smithing | Smiths bars at anvils |
| `::fletch` | Fletching | Makes bows and arrows from logs |
| `::craft [mode]` | Crafting | leather, spinning, pottery |
| `::herblaw [mode]` | Herblaw | identify herbs, make potions |

### Support Bots

| Command | Skill | Details |
| --- | --- | --- |
| `::agility [course]` | Agility | gnome, barb, wild |
| `::thieve [target]` | Thieving | Pickpockets NPCs |
| `::prayer` | Prayer | Buries bones from inventory |

### Bot Behavior

- **Auto-banking** — gathering bots walk to the nearest bank when inventory is full
- **Auto-eating** — combat bots eat food when HP drops low
- **Clean shutdown** — bots stop when out of supplies or after repeated banking failures
- **Statistics** — track items collected/processed and XP gained

### Examples

```text
::woodcut willow       Cut willow trees, bank logs
::fish lobster         Catch lobsters, bank them
::mine iron            Mine iron ore, bank it
::combat goblin        Fight goblins, eat food, loot drops
::agility gnome        Run the Gnome Agility Course
::cook                 Cook raw food on a nearby range
::prayer               Bury all bones in inventory
::craft leather        Craft leather items
::herblaw identify     Identify unidentified herbs
```

---

## Hardcore Mode

- Toggle when creating a new account (check the Hardcore box)
- On death: your save file is permanently deleted and the client closes
- Logging in again starts a fresh character
- Back up your save file manually if you want a safety net

---

## Building from Source

### Desktop

Requirements: Java 17+, `lib/gson-2.6.2.jar` (included)

```bash
BUILD_DIR="build" && \
rm -rf "$BUILD_DIR" && \
mkdir -p "$BUILD_DIR" && \
find src -name '*.java' -print0 | xargs -0 javac -source 17 -target 17 -cp lib/gson-2.6.2.jar -d "$BUILD_DIR" && \
jar cfm "rsc.jar" META-INF/MANIFEST.MF -C "$BUILD_DIR" . && \
rm -rf "$BUILD_DIR"
```

### Mobile

Requirements: Android SDK (API 34, Build Tools 34.0.0), JDK 11+

```bash
git clone https://github.com/theKennethy/SingleRSC-Mobile.git
cd SingleRSC-Mobile
export ANDROID_SDK_ROOT=/path/to/android-sdk
./gradlew assembleRelease
```

APK output: `app/build/outputs/apk/release/runescape-classic.apk`

---

## FAQ

**Q: Does this connect to any external server?**
A: No. Everything runs locally — no internet required.

**Q: What Java version do I need for desktop?**
A: Java 17 or newer.

**Q: What Android version for mobile?**
A: Android 7.0+ (API 24).

**Q: Can I resize the window?**
A: Yes (desktop). On mobile, use pinch zoom.

**Q: How do I type commands on mobile?**
A: Double-tap anywhere to open the keyboard, then type your command.

**Q: How do I right-click on mobile?**
A: Long press (hold your finger down for about a second).

**Q: Can I change XP rates?**
A: Edit `EXPERIENCE_MULTIPLIER` in `Constants.java` and rebuild (default is 8x).

**Q: Where are save files stored?**
A: Desktop: `saves/` directory in the working directory. Mobile: app internal storage (uninstalling deletes saves).

**Q: How do I restore a Hardcore character after death?**
A: You can't — that's the point. Back up your save file beforehand.

**Q: Do bot scripts work on mobile?**
A: Yes — all bot commands work identically to desktop.

---

## Website Structure

```text
.
├── index.html      # Main page
├── styles.css      # Styling
├── main.js         # Scripts
└── README.md       # This file
```

---

## Disclaimer

This project is a preservation and educational single-player reimplementation.
All original game assets, names, and concepts belong to their respective owners.
Use responsibly and in accordance with applicable laws.

---

## License

GPL v3.0 — see [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt)

## Contact

For questions, suggestions, or feedback, please open an issue or contact [theKennethy](https://github.com/theKennethy).
