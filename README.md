# 🎮 CommandMenu

An in-game command menu for Roblox featuring a modern UI, fuzzy search, and chat-based command execution (`;`, `:`, `/`).

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Lua](https://img.shields.io/badge/language-Lua-blue)
![Roblox](https://img.shields.io/badge/platform-Roblox-red)
![License](https://img.shields.io/badge/license-MIT-purple)

---

## 📖 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Installation](#-installation)
- [Usage](#-usage)
- [Commands](#-commands)
- [Code Structure](#️-code-structure)
- [Legal Notice](#️-legal-notice)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📌 About

**CommandMenu** is a **Roblox GUI script** that adds a fully-featured command panel accessible through a floating button, keyboard shortcut, or chat input.

It was designed to run inside **script executors** and provides a wide range of utility commands for manipulating the local character, camera, lighting, and player visualization.

The entire interface is built **from scratch** using `ScreenGui` and `Instance.new` — no external UI libraries or dependencies.

> 💡 **In short:** Whether you want to quickly toggle **GodMode**, inspect another player with **ESP**, or teleport across the map with **Goto**, CommandMenu gives you a **clean, searchable, and extensible** command center without ever leaving the game.

---

## ✨ Features

- 🎨 **Modern UI** — dark theme with rounded corners, smooth tweens, and hover states
- 🔍 **Fuzzy search** — intelligent matching that finds commands even with typos
- ⌨️ **Quick access** — open via the `cmds` button, chat keywords (`cmds` / `comandos`), or prefixes (`;`, `:`, `/`)
- 📜 **Chat execution** — run any command by typing `;speed 100` in chat
- 🧩 **Extensible** — adding new commands is as simple as appending to the `COMMANDS` table
- 🖱️ **Draggable** — the main button can be repositioned anywhere on screen
- 🌐 **Dual chat support** — works with both the legacy chat and `TextChatService`
- ⚡ **Performance-friendly** — only active features run connections; toggles clean up after themselves

---

## 🚀 Installation

### Method 1 — Executor (quick)

Paste the following line into any compatible executor and run it inside the game:

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/YOUR_USERNAME/CommandMenu/main/CommandMenu.lua"))()
```

### Method 2 — Local

1. Download `CommandMenu.lua`
2. Paste it into your preferred executor
3. Execute inside the game

### Requirements

- A Roblox executor supporting `loadstring`, `game:HttpGet`, and `UserInputService`
- Recommended: an executor with `setclipboard`, `firetouchinterest`, and `sethiddenproperty` support for advanced commands

---

## 🎯 Usage

### Opening the menu

| Action | How |
|--------|-----|
| Button | Click the `cmds` button at the top of the screen |
| Chat keyword | Type `cmds` or `comandos` in chat |
| Chat prefix | Type `;command args`, `:command args`, or `/command args` |

### Running a command

**Via the GUI:**

1. Open the panel
2. Type the command name in the search bar
3. Click the command (it fills the input field)
4. Press `Enter` to execute

**Via chat prefix:**

```lua
;Speed 100
:JumpPower 200
/Fly 5
```

---

## 📜 Commands

### 🏃 Movement

```lua
Speed           -- Sets WalkSpeed
JumpPower       -- Sets JumpPower
InfiniteJump    -- Infinite jumping
AutoJump        -- Auto-jumps on collision
EdgeJump        -- Jumps when leaving platforms
AirWalk         -- Walk in the air (gravity 0)
WallClimb       -- Climb walls
Dash            -- Dash on jump
Fly             -- Fly (E = up, Q = down)
CFrameFly       -- CFrame-based flight
Noclip          -- Walk through walls
Swim            -- Swim mode
```

### 👤 Character

```lua
Sit             -- Sit down
Lay             -- Lie down
SitWalk         -- Walk with sit animation
Spasm           -- Spasm animation (R6)
HeadThrow       -- Throws head (R6)
Animation       -- Plays custom animation
AnimSpeed       -- Adjusts animation speed
NoAnim          -- Disables animations
Reanim          -- Enables animations
R6              -- Simulates R6 on R15
```

### 🛡️ Defense

```lua
GodMode         -- Infinite local health
AntiFling       -- Anti-fling protection
AntiVoid        -- Prevents void falls
AntiStun        -- Anti-stun / ragdoll
AntiSit         -- Anti-sit
AntiAFK         -- Anti-idle kick
AntiKick        -- Hooks Kick/Ban (client-side)
AntiRing        -- Anti-ring
AntiFallDamage  -- Anti-fall damage
```

### 👁️ Visual / ESP

```lua
ESP             -- Highlights all players
ESPTarget       -- ESP a specific player
ItemESP         -- Item ESP
NPCEsp          -- NPC ESP
VehicleESP      -- Vehicle ESP
LootESP         -- Chest / loot ESP
TeamESP         -- Team-colored ESP
PlayerName      -- Names above players
HealthBar       -- Health bars
HealthNumber    -- Health numbers
Distance        -- Distance to players
EquippedTool    -- Equipped tool display
Tracer          -- Line to a player
View            -- Spectate a player
```

### 🌍 World

```lua
Fullbright      -- Full lighting
RemoveFog       -- Removes fog
Time            -- Sets server time (client)
Fov             -- Field of View
MaxZoom         -- Camera max zoom
MinZoom         -- Camera min zoom
NoclipCam       -- Camera through walls
```

### 🎵 Sound / Music

```lua
Music           -- Plays music
ClientMusic     -- Plays client-side music
Sound           -- Looping swim sound
Volume          -- Master volume (0-10)
```

### 🎯 Combat

```lua
Fling           -- Flings players
kill            -- Fling in kill mode
HandleKill      -- Kills using tool handle
SpinFling       -- Spinning fling
KillAllNpc      -- Kills all NPCs
clientKill      -- Client-side tool kill
Aimbot          -- Loads external aimbot
```

### 🔧 Utilities

```lua
Goto            -- Teleports to a player
Orbit           -- Orbits around a player
Spin            -- Spins your character
Offset          -- Moves in XYZ
TpPosition      -- Teleports to (n, n, n)
MouseTp         -- Teleports to mouse
Thru            -- Phases toward camera
Reset / Re      -- Resets character
Chat            -- Sends a chat message
Spam            -- Loops a chat message
AntiLag         -- Reduces visual lag
SetFpsCap       -- Limits FPS
```

> 📎 For the full list, check the `COMMANDS` table inside the source code.

---

## 🏗️ Code Structure

```lua
CommandMenu.lua
├── Services & global variables
├── Color palette
├── ScreenGui + "cmds" button
├── Generic drag handler
├── Panel (overlay + frame + search + list)
├── Fuzzy search (Levenshtein)
├── buildRow / refreshList
├── openPanel / closePanel
├── Events (input, chat hooks, prefixes)
└── COMMANDS = { ... }  ← extensible table
```

### Adding a new command

```lua
{
    name = "MyCommand",
    desc = "Optional description",
    args = true,  -- true if it accepts a parameter
    run = function(value)
        -- value = string or number (auto-converted)
        print("Executed with:", value)
    end,
},
```

---

## ⚠️ Legal Notice

> **This project is provided for educational and research purposes only.**
>
> - Using exploits/cheats in games may violate the **Roblox Terms of Service** and specific game rules.
> - The author is **not responsible** for bans, punishments, or any damage caused by using this script.
> - **Do not use** it in games where you don't have explicit permission.
> - Some commands (like `AntiKick`, `Fling`, `HandleKill`) may be considered abuse and result in a **permanent ban**.

---

## 🤝 Contributing

1. **Fork** the project
2. Create a branch: `git checkout -b feature/MyCommand`
3. Commit: `git commit -m "Add command X"`
4. Push: `git push origin feature/MyCommand`
5. Open a **Pull Request**

### Code Guidelines

- Use `PascalCase` for command names
- Always clean up connections in toggle commands (`_G.XxxConn:Disconnect()`)
- Prefer `workspace:Raycast` over the deprecated `FindPartOnRay`
- Add a `desc` field when the command takes arguments

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 👤 Author

**Your Name**

- GitHub: [@your_username](https://github.com/your_username)
- Discord: `your_discord`

---

⭐ If this project helped you, drop a star on the repository!
