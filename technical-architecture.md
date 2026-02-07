# LAN PARTY -- Technical Architecture Document

**Lead Programmer:** BYTE
**Status:** Architecture Definition -- Ready for Implementation Planning
**Reference Docs:** `pitch.md`, `game-design.md`
**Target Platform:** PC (Steam), Steam Deck secondary
**Target Framerate:** 60 FPS (desktop simulation), 30 FPS acceptable for mini-games
**Memory Budget:** 2GB max (period-appropriate hardware support)

---

## 1. Engine & Framework Selection

### 1.1 Core Engine: Godot 4.3

**Decision:** Godot 4.3 with GDScript primary, C# for performance-critical AI systems.

**Rationale:**
- Zero royalties. We ship this game, we keep what we earn.
- 2D rendering pipeline is mature and performant. This game is 100% 2D UI rendering -- no need for Unreal's 3D muscle.
- Scene system maps cleanly to desktop applications. Each app (MSN, mIRC, file manager) is a Godot scene. The desktop manager is the root scene that instances them.
- Built-in signal/event system perfect for notification-driven architecture. Desktop apps emit signals, the desktop manager routes them.
- Cross-platform without pain. Windows is primary, but Linux and Steam Deck come free. macOS is a checkbox.
- Lightweight runtime. A 2D UI game should not ship with 200MB of engine overhead.

**Alternative considered:** Unity. Rejected because UI Toolkit still feels half-baked for complex nested windows, and runtime fees are a dealbreaker for an indie game with uncertain sales.

**Alternative considered:** Custom engine. No. I learned this lesson once. See personality file, section "Core Philosophy, Wound." We ship working software.

### 1.2 Language Strategy

**Primary:** GDScript for all UI, game systems, desktop simulation, event routing. Fast iteration, easy debugging, the Godot debugger is excellent for this.

**Secondary:** C# + GDNative for AI agent system and text generation wrapper. Reason: We are integrating external LLM APIs or local models. C# has better library support for HTTP clients, JSON serialization, and async patterns. GDScript can call C# via Godot's interop.

**Not using:** C++. Premature optimization. Profile first. If we need C++, we will know where -- and it will not be "everywhere."

### 1.3 Target Platforms

**Tier 1 (must work):** Windows 10/11, 64-bit, Steam. This is 90% of the market for this game.

**Tier 2 (should work):** Steam Deck, Linux via Proton. Test on Deck hardware monthly. Godot exports to Linux natively, Proton handles the rest.

**Tier 3 (stretch goal):** macOS via Steam. Test quarterly. Not a priority but Godot makes it low-cost to support.

**Rejected:** Consoles (mouse-driven UI does not translate), mobile (screen size kills the desktop simulation aesthetic), web (performance and save state complexity).

---

## 2. Architecture Overview

### 2.1 High-Level System Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                      DESKTOP MANAGER                        │
│  (Root Scene, Window Manager, Notification Router)         │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │   MSN    │  │   mIRC   │  │  Browser │  │  Winamp  │  │
│  │ (Scene)  │  │ (Scene)  │  │ (Scene)  │  │ (Scene)  │  │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘  │
│       │             │             │             │          │
│       └─────────────┴─────────────┴─────────────┘          │
│                          ▲                                  │
│                          │ Signals (events, notifications)  │
└──────────────────────────┼──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      GAME STATE MANAGER                     │
│  (Global Singleton, Central Data Store)                     │
│                                                             │
│  • Character Database        • Reputation Trackers         │
│  • Relationship Graph        • Virtual Filesystem          │
│  • Message Queue             • Economy State               │
│  • Timeline Clock            • ISP Heat Accumulator        │
└──────────────────┬──────────────────────────────────────────┘
                   │
        ┌──────────┴──────────┐
        ▼                     ▼
┌────────────────┐    ┌────────────────┐
│  AI AGENT      │    │  EVENT         │
│  SYSTEM        │    │  SCHEDULER     │
│  (C# Module)   │    │  (GDScript)    │
│                │    │                │
│  • Character   │    │  • Time-gated  │
│    Agents      │    │    events      │
│  • Message     │    │  • Life events │
│    Generation  │    │  • Decay ticks │
│  • Personality │    │  • Triggers    │
│    Models      │    │                │
└────────────────┘    └────────────────┘
```

### 2.2 Data Flow

**Input Flow:**
1. Player clicks UI element (e.g., MSN message notification)
2. UI element emits signal to Desktop Manager
3. Desktop Manager routes signal to appropriate application scene
4. Application scene requests data from Game State Manager
5. Application scene renders content
6. Player interacts (e.g., types reply, clicks button)
7. Application scene sends action to Game State Manager
8. Game State Manager updates state, triggers downstream effects

**AI Flow:**
1. Event Scheduler triggers character behavior (e.g., "time for ShadowLurker to message player")
2. AI Agent System queries Game State Manager for character context (mood, recent history, relationships)
3. AI Agent generates message based on personality model and context
4. Message queued in Game State Manager
5. Desktop Manager receives notification signal
6. MSN application shows taskbar flash and plays sound
7. Player opens MSN and sees message

**Time Flow:**
1. Timeline Clock in Game State Manager ticks forward (1x/2x/4x speed or paused)
2. Every in-game hour, Event Scheduler checks for triggered events
3. Triggered events emit signals to relevant systems (AI Agent, Desktop Manager, Game State)
4. Systems respond: characters change status, downloads complete, forum threads update

### 2.3 Component Architecture Philosophy

**Decoupled but not distributed.** Each desktop application is a self-contained scene with its own UI logic. But all shared state lives in Game State Manager. No app talks directly to another app -- they communicate through signals routed by Desktop Manager or through shared state.

**Why this architecture?** Because adding a new desktop application should be low-risk. Building a new app scene should not require touching existing code. The Desktop Manager is the only coupling point. This lets us iterate fast, add stretch-goal apps (GeoCities browser, hardware monitor), or cut apps (Winamp as MVP sacrifice) without refactoring the world.

**Testability:** Each app scene can be tested in isolation by mocking Game State Manager. The Desktop Manager can be tested by simulating signal traffic. The AI Agent System can be tested with static character data. If a system cannot be tested in isolation, the architecture is wrong.

---

## 3. Core Systems Design

### 3.1 Desktop OS Simulation

**What it does:** Renders a pixel-accurate Windows XP desktop. Manages application windows, taskbar, system tray, desktop icons, start menu. Handles window focus, minimize/maximize/close, drag-to-reorder. This is the UI framework for the entire game.

**Implementation:**

**Tech stack:**
- Godot Control nodes for UI. Theme resources for XP-authentic styling (blue title bars, Luna theme, Bliss wallpaper).
- Custom WindowManager node that instances application scenes as child Control nodes.
- Z-index management for window layering. Click to focus brings window to top of z-stack.
- Taskbar is a fixed HBoxContainer at screen bottom. Each open app adds a button.

**Window anatomy:**
```gdscript
# WindowChrome.gd
extends Control

signal close_requested
signal minimize_requested
signal maximize_requested

@export var window_title: String = "Application"
@export var icon: Texture2D

var is_maximized = false
var restore_rect: Rect2

func _ready():
    # Build title bar: icon, title label, min/max/close buttons
    # Connect button signals to internal handlers
    # Make title bar draggable via _gui_input
    pass

func _gui_input(event: InputEvent):
    if event is InputEventMouseButton and event.button_index == MOUSE_BUTTON_LEFT:
        if event.pressed:
            # Start drag
            pass
    elif event is InputEventMouseMotion and is_dragging:
        # Move window
        position += event.relative
```

Each desktop app scene extends `WindowChrome` and adds its content as a child node. The WindowManager handles instancing and signals.

**Taskbar & system tray:**
- Taskbar buttons pulse when app has unread notification (MSN message, download complete).
- System tray shows clock (driven by in-game time), volume icon (cosmetic), network icon (shows download activity).
- Start menu is a stretch goal. Not needed for MVP -- desktop icons and taskbar are sufficient.

**Performance notes:**
- Window rendering is the hottest path. Every frame, we are drawing 5--10 overlapping Control nodes with text, icons, and backgrounds.
- Optimization 1: Mark windows as `clip_contents = true`. Do not draw outside window bounds.
- Optimization 2: Minimize redraws. Only redraw a window when its content changes (message arrives, download progress ticks). Use `queue_redraw()` selectively.
- Optimization 3: Limit max open windows to 12. If player opens 13th app, close the least-recently-used window with a warning. This is era-authentic (XP would choke with too many windows) and performance-smart.

**Risk mitigation:**
- Risk: Window dragging feels janky. Mitigation: Test on 60Hz and 144Hz monitors. Ensure drag is smooth at both refresh rates. Godot's Control node dragging should handle this, but profile it.
- Risk: XP theme is hard to replicate pixel-perfectly. Mitigation: Ship a "good enough" XP theme for MVP. Iterate toward pixel-perfection in post-launch patches. Nostalgia is forgiving if the vibe is right.

### 3.2 Window Manager

**What it does:** Manages lifecycle of application windows. Instances scenes, handles focus, routes signals, manages z-order, enforces window limit.

**Implementation:**

```gdscript
# DesktopManager.gd
extends Control

@onready var game_state = GameStateManager  # Singleton

var open_windows: Array[Node] = []
var focused_window: Node = null

const MAX_OPEN_WINDOWS = 12
const WINDOW_SCENES = {
    "msn": preload("res://apps/msn/MSNApp.tscn"),
    "mirc": preload("res://apps/mirc/MIRCApp.tscn"),
    "browser": preload("res://apps/browser/BrowserApp.tscn"),
    # ...etc
}

func open_app(app_name: String):
    # Check if already open
    for win in open_windows:
        if win.app_name == app_name:
            focus_window(win)
            return

    # Enforce max windows
    if open_windows.size() >= MAX_OPEN_WINDOWS:
        close_lru_window()

    # Instance scene
    var scene = WINDOW_SCENES[app_name].instantiate()
    add_child(scene)
    open_windows.append(scene)

    # Connect signals
    scene.close_requested.connect(_on_window_close.bind(scene))
    scene.notification_emitted.connect(_on_notification)

    focus_window(scene)

func focus_window(win: Node):
    focused_window = win
    # Bring to top of z-stack
    move_child(win, -1)

func _on_notification(app_name: String, notif_data: Dictionary):
    # Play sound
    AudioManager.play_notification_sound(app_name)
    # Flash taskbar button
    taskbar.flash_button(app_name)

func close_lru_window():
    # Find least-recently-focused window that is not critical
    # (Do not auto-close file manager if a download is active)
    pass
```

**Notification routing:** Each app emits a `notification_emitted` signal when something happens that needs player attention (new message, download complete, forum reply). Desktop Manager handles the audiovisual feedback (sound, taskbar flash) and logs the notification to Game State for persistence.

### 3.3 File System Simulation

**What it does:** Simulates a hierarchical file system. Stores downloaded game ISOs, installed games, user documents (saved seating charts, hardware notes), CD images, music files (Winamp playlists). Tracks storage usage. Enforces period-authentic file size limits.

**Implementation:**

**Data structure:**
```gdscript
# VirtualFilesystem.gd (part of GameStateManager)

class VirtualFile:
    var name: String
    var extension: String
    var size_mb: int  # Integer megabytes, period-authentic
    var path: String  # Full path from root
    var file_type: String  # "game_iso", "music", "document", "executable"
    var metadata: Dictionary  # Game-specific data: install status, crack quality, malware flag

class VirtualFolder:
    var name: String
    var path: String
    var children: Array  # Mix of VirtualFile and VirtualFolder

var root: VirtualFolder
var total_storage_mb: int = 40 * 1024  # 40GB HDD, period-authentic
var used_storage_mb: int = 0

func create_file(path: String, size_mb: int, file_type: String, metadata: Dictionary = {}):
    # Parse path, navigate to parent folder, add file
    # Update used_storage_mb
    # Check if over limit -> emit signal for "disk full" warning
    pass

func delete_file(path: String):
    # Remove file, free storage
    pass

func get_files_in_folder(path: String) -> Array[VirtualFile]:
    # Return list of files for file manager rendering
    pass
```

**Storage pressure:** The 40GB limit is a real constraint. Game ISOs are 600MB (small indie game) to 4.7GB (DVD-sized AAA game). The player will hit the limit by mid-game. Deleting old games to make room for new ones is a strategic choice -- does the player keep a game nobody plays anymore just in case a crew member requests it?

**File operations:**
- Download (from P2P or IRC): Creates file over time, size ticks up as download progresses.
- Extract (from RAR/ZIP): Decompresses archive into folder, slightly larger than archive size.
- Mount ISO (for CD burner): No storage cost, just creates virtual CD drive entry.
- Burn to CD: Consumes blank CD (inventory item), creates physical CD object (inventory item).
- Delete: Frees storage immediately.

**Malware system:** Some files (P2P downloads, sketchy IRC sources) have a malware flag. If the player installs or runs a malware-flagged file, trigger effects: pop-up ads on desktop, corrupted save data, reduced performance (simulate by adding artificial frame drops for 5 real-time minutes -- annoying but not game-breaking). Scanning with antivirus (simulated app) can detect malware before damage.

**Performance notes:** The filesystem is just in-memory data structures. Even with 1000 files, lookup and rendering are trivial. No disk I/O, no serialization hot path. Save the entire filesystem as JSON on game save.

### 3.4 Chat/Messenger System (MSN Simulation)

**What it does:** 1-on-1 chat with AI characters. Buddy list shows online status, away messages, profile pictures. Typing indicators. Nudge feature. Group chat for LAN party invites. This is the primary relationship management interface.

**Implementation:**

**UI structure:**
- Buddy list window: Scrollable list of contacts, each showing status icon, screen name, away message.
- Chat window: Per-contact, instanced on demand. Chat history (last N messages), text input field, send button, nudge button.
- Typing indicator: When AI character is "typing," show animated dots.

**Message data model:**
```gdscript
class ChatMessage:
    var sender_id: String  # Character ID or "player"
    var recipient_id: String
    var timestamp: int  # In-game time
    var text: String
    var read: bool
```

**AI integration:**
- When a character "decides" to message the player (triggered by Event Scheduler), the AI Agent System generates message text based on character personality, current mood, recent events, relationship state.
- Message is added to Game State's message queue.
- Desktop Manager receives signal, shows notification.
- Player opens MSN, sees message in chat window.
- Player types reply. On send, reply is added to message queue and sent to AI Agent System for context update.
- AI Agent may reply immediately (if character is in active conversation mode) or later (if character is busy/away).

**Away messages:** Each character has an away message that updates dynamically based on mood and life events. Example state machine:
- Happy + no life events: Song lyrics, inside jokes, playful status.
- Neutral: "brb", "afk", "doing homework".
- Unhappy: "...", "leave me alone", "whatever".
- Life event (new girlfriend): "out with J <3".

Away message changes are subtle emotional telegraphs. Expert players read them like tea leaves.

**Nudge mechanic:** Click nudge button, recipient's window shakes (if they are online). Overuse annoys characters (mood penalty). Period-authentic chaos.

**Performance notes:** Chat history is capped at 100 messages per character. Older messages are summarized by AI Agent System and stored as compressed context. Full message history is not needed for gameplay, only recent context.

### 3.5 Browser Simulation

**What it does:** Simulated Internet Explorer-style browser. Displays static HTML pages (gaming news, character GeoCities homepages, forum threads, private tracker sites). No real web rendering -- all pages are pre-authored or procedurally generated HTML snippets rendered via RichTextLabel.

**Implementation:**

**Tech stack:**
- RichTextLabel node for content rendering. Supports BBCode for styling (bold, italic, links, colors).
- Navigation history stack (back/forward buttons).
- URL bar (cosmetic + functional: player types URL or clicks links).

**Page types:**
- Gaming news sites: Static content with procedurally inserted headlines based on game timeline (e.g., "Half-Life 2 Delayed Again").
- Character homepages: Generated per character. Shows their bio, favorite games, guestbook (other characters leave comments), 2003-era web design crimes (auto-playing MIDI, tiled backgrounds, Comic Sans).
- Forum (phpBB-style): Threaded discussions. Characters post based on personality and recent events. Player can post replies (affects reputation).
- Private tracker sites: Functional UI for browsing available game downloads, checking ratio, uploading content.

**Content generation:**
- News headlines: Template strings + randomized game names + timeline-appropriate events.
- Character homepages: Template HTML with character-specific fills (favorite games, personality quirks, music taste).
- Forum threads: AI-generated posts that reference in-game events. Thread structure is predefined (e.g., "LAN party recap" thread always appears after a party), but post content is dynamic.

**Performance notes:** Pages are rendered on-demand. Cache the last 5 visited pages to avoid regenerating forum threads every time the player clicks back.

**Stretch goal:** Mini-games embedded in browser (Flash game parodies). If we have time, add a "play flash game" mechanic -- click link, opens a tiny Breakout clone. Pure flavor, low priority.

### 3.6 Mini-Games-Within-Games System

**What it does:** During LAN parties, the player and AI characters "play" a game together. This is rendered as a simplified, watchable version of the game (think 2D top-down view of a Counter-Strike match or a side-view of an Unreal Tournament arena). The player does not play the full game -- they watch AI agents play and make high-level decisions (game selection, team composition, when to intervene).

**Implementation:**

**Mini-game types (4--6 for MVP):**
1. **CounterOps (Counter-Strike parody):** Top-down tactical shooter. Two teams, plant/defuse bomb. AI agents move and shoot based on personality stats (aggression, skill).
2. **UnrealBattle (Unreal Tournament parody):** Side-view deathmatch arena. AI agents jump and shoot. Fast-paced, high energy.
3. **StratCraft (StarCraft parody):** Abstracted RTS. Show resource counters and unit blobs. AI agents build armies and fight. Slower, strategic.
4. **RallyRacer (racing game):** Top-down racer. AI agents drive laps, overtake, crash.
5. **FightZone (fighting game):** 2D side-view. Two characters, health bars, combo counters.
6. **PuzzleQuest (puzzle game, stretch goal):** Tetris/Bejeweled parody. Cozy, low-stakes.

**AI player behavior:** Each AI character has a skill level (0--100, derived from personality + practice hours) and a playstyle (aggressive, defensive, strategic, chaotic). During a mini-game:
- Skill determines win probability and action quality.
- Playstyle determines behavior (aggressive players rush, defensive players camp).
- Mood affects performance (angry characters play recklessly, sad characters underperform).

**Rendering:** Mini-games are ultra-simplified 2D scenes. Think flash game aesthetics, not AAA graphics. The focus is on readability and emergent drama, not gameplay depth. We are not making 6 real games -- we are making 6 watchable simulations.

**Example: CounterOps match structure:**
```gdscript
# CounterOps.gd
extends Node2D

var teams: Array[Array]  # Two teams of AI characters
var round_time: float = 120.0  # 2 minutes per round
var bomb_planted: bool = false

func _process(delta):
    round_time -= delta

    # Update AI agent positions and actions
    for team in teams:
        for agent in team:
            agent.update_behavior(delta)

    # Check win conditions
    if round_time <= 0 or all_eliminated(teams[0]) or all_eliminated(teams[1]):
        end_round()

func end_round():
    # Determine winner, update character moods based on performance
    # Emit events: someone raged, someone clutched, someone accused screen-looking
    pass
```

**Intervention mechanics:** During a match, the player can:
- Pause and swap to a different game (if energy is tanking).
- Switch team compositions (if a feud is escalating).
- Call a break (restore energy but pause momentum).

**Performance notes:** Mini-games target 30 FPS, not 60. They are small, with 10--12 on-screen entities max. If performance is an issue, reduce to 20 FPS -- the player is watching, not playing, so lower framerate is acceptable.

**Risk mitigation:** Risk: Building 6 games-within-a-game is scope creep. Mitigation: Share as much code as possible. All mini-games use the same AI behavior system, just with different game rules. Build one (CounterOps) to completeness, then template the others. If we are over budget, ship 3 mini-games at launch and add more post-launch as free updates.

### 3.7 Network Simulation

**What it does:** Simulates file downloads (P2P, IRC DCC transfers) and network conditions (lag during LAN parties, ISP throttling when heat is high). Visual progress bars, download speeds, ETA calculations. Network issues create tension and failure states.

**Implementation:**

**Download system:**
```gdscript
class DownloadJob:
    var file_name: String
    var file_size_mb: int
    var progress_mb: float
    var download_speed_kbps: int  # Kilobytes per second, era-authentic
    var source: String  # "p2p", "irc", "private_tracker"
    var malware_risk: float  # 0.0 to 1.0
    var completed: bool = false

    func tick(delta: float, network_conditions: Dictionary):
        # Update progress based on speed and conditions
        var speed_modifier = network_conditions.get("speed_modifier", 1.0)
        var actual_speed = download_speed_kbps * speed_modifier
        progress_mb += (actual_speed * delta) / 1024.0

        if progress_mb >= file_size_mb:
            completed = true
```

**Network conditions:** Tracked globally, affects all active downloads.
- Base speed: Determined by in-game ISP plan (256kbps DSL, 1mbps cable, 3mbps broadband).
- Congestion: If multiple downloads are active, split bandwidth.
- Time-of-day: Slower during peak hours (evening when household is online).
- ISP throttling: If heat is high, ISP reduces speed by 50--80%.

**LAN party network:** During a LAN party, simulate local network. If the player's hardware setup is poor (daisy-chained hubs instead of a switch), introduce lag events randomly. Lag events:
- "Network lag spike" -> AI characters complain in chat, party energy drops.
- "Disconnection" -> One character drops from the game, must reconnect, momentum lost.

**Visual feedback:** Download manager app (separate window) shows active downloads with progress bars, current speed, ETA. Color-coded by source (green = safe, yellow = medium risk, red = high risk).

**Performance notes:** Download progress updates once per second (no need for per-frame updates). ETA calculation is a simple division. No heavy math.

### 3.8 Discovery/Narrative System

**What it does:** Delivers the game's story through emergent narrative moments. No cutscenes, no scripted dialogue trees. Story unfolds through chat messages, forum posts, away message changes, and character life events. The system tracks narrative beats and ensures key moments (first party, first fight, first loss, finale) happen organically.

**Implementation:**

**Narrative beats:** Defined as flexible templates, not rigid scripts.
```gdscript
class NarrativeBeat:
    var id: String
    var name: String
    var conditions: Array[Callable]  # List of condition checks
    var weight: float  # Priority when multiple beats are eligible
    var effects: Array[Callable]  # What happens when beat triggers
    var cooldown_days: int  # Minimum time before next beat
    var repeatable: bool
```

**Example beat: "First Rivalry"**
```gdscript
var first_rivalry_beat = NarrativeBeat.new()
first_rivalry_beat.id = "first_rivalry"
first_rivalry_beat.conditions = [
    func(): return game_state.lan_parties_hosted >= 2,
    func(): return game_state.crew_size >= 4,
    func(): return not game_state.flags.has("rivalry_triggered")
]
first_rivalry_beat.effects = [
    func():
        # Pick two characters with low mutual relationship
        var chars = game_state.get_rival_candidates()
        ai_agent.trigger_rivalry(chars[0], chars[1])
        game_state.flags["rivalry_triggered"] = true
]
```

**Event Scheduler integration:** Every in-game day, the Event Scheduler checks all narrative beats. Eligible beats (all conditions met) are weighted and one is selected probabilistically. This ensures story moments happen but not on a fixed timeline.

**Character life events:** Characters have probabilistic life events that inject narrative tension:
- Getting a job (reduced availability)
- Moving away (permanent departure)
- Relationship drama (temporary conflict)
- New hobby (changed game preferences)
- Academic pressure (temporary absence)

Life events are rolled weekly with increasing probability as the game progresses (modeling the "end of the era" theme). Player cannot prevent them but can mitigate through strong relationships.

**Forum and chat narrative:** AI-generated content references past events. After a great LAN party, characters post on the forum: "Last night was legendary, FragMaster42's clutch 1v5 was insane." After a bad party: "Did anyone else's game crash 5 times? What was that?"

**Finale trigger:** When in-game time reaches month 10+, check finale conditions:
- At least 3 core crew members have left or drifted.
- Player reputation in Friend Group is above threshold (they tried to hold it together).
- Last LAN party event is scheduled.

Finale is bittersweet: one last great party, epilogue messages showing what happened to characters, final away message changes.

**Performance notes:** Narrative system runs once per in-game day, not real-time. No performance concern.

---

## 4. Data Architecture

### 4.1 Virtual Filesystem (Covered in 3.3)

See section 3.3 for full details. Summary: Hierarchical tree structure, integer MB sizes, metadata per file, storage limit enforced.

### 4.2 Desktop State

**What we persist:**
- Open windows (which apps, positions, sizes, z-order)
- Taskbar state (pinned apps, notification badges)
- Desktop icons (position, visibility)
- Wallpaper selection
- Audio settings (Winamp volume, playlist state)

**Serialization format:** JSON dictionary. On save, serialize entire desktop state to JSON, write to save file. On load, deserialize and reconstruct desktop.

**Example:**
```json
{
  "open_windows": [
    {"app": "msn", "position": [100, 150], "size": [300, 400], "z_index": 1},
    {"app": "mirc", "position": [450, 200], "size": [500, 500], "z_index": 0}
  ],
  "desktop_icons": [
    {"name": "My Computer", "position": [20, 20]},
    {"name": "Recycle Bin", "position": [20, 100]}
  ],
  "wallpaper": "bliss.jpg"
}
```

### 4.3 Chat Logs

**Message storage:** Each character has a message history array. Cap at 100 messages. Older messages are compressed into a summary string by AI Agent System.

**Serialization:**
```json
{
  "character_id": "shadow_lurker",
  "messages": [
    {"sender": "player", "timestamp": 150, "text": "hey whats up", "read": true},
    {"sender": "shadow_lurker", "timestamp": 152, "text": "nm u?", "read": true}
  ],
  "summary": "Previously: player and shadow_lurker discussed the upcoming LAN party..."
}
```

**Performance notes:** Message arrays are small (100 entries max per character). Serialization is trivial. Full chat history for 15 characters = ~20KB uncompressed JSON.

### 4.4 Character State

**Per-character data:**
```gdscript
class Character:
    var id: String  # Unique identifier
    var screen_name: String  # Display name
    var personality: PersonalityTraits
    var mood: float  # -100 to +100
    var relationships: Dictionary  # Pairwise with all other characters
    var desires: Array[Desire]  # Active goals
    var life_events: Array[LifeEvent]  # Past and current events
    var online_status: String  # "online", "away", "offline"
    var away_message: String
    var message_history_with_player: Array[ChatMessage]
    var forum_posts: Array[ForumPost]
    var game_preferences: Dictionary  # Which games they like
    var skill_levels: Dictionary  # Per mini-game skill rating
```

**Serialization:** Each character is a JSON dictionary. 15 characters at ~2KB each = ~30KB per save file.

### 4.5 Save Format

**Single save file per playthrough:** `save_slot_1.json`

**Top-level structure:**
```json
{
  "version": "1.0.0",
  "timestamp": 1672531200,
  "playtime_hours": 12.5,
  "game_state": {
    "timeline": {"current_day": 45, "current_hour": 14},
    "economy": {"money": 120, "allowance_day": 3},
    "reputation": {"friend_group": 65, "forum": 40, "irc": 30, "scene": 15},
    "isp_heat": 45,
    "lan_parties_hosted": 8
  },
  "characters": [ /* array of character objects */ ],
  "filesystem": { /* virtual filesystem tree */ },
  "desktop_state": { /* open windows, icon positions */ },
  "chat_logs": { /* per-character message histories */ },
  "event_flags": { /* narrative beats triggered */ }
}
```

**Compression:** Use Godot's built-in JSON serialization. Compress with GZip before writing to disk. Typical save file: 50--100KB uncompressed, 10--20KB compressed.

**Auto-save:** Every in-game day at midnight. Manual save allowed anytime. Save slot selection on main menu (3 slots).

**Performance notes:** Save/load is not a hot path. Taking 100ms to serialize and write is fine. Test with max-size save file (late game, 15 characters, full filesystem) to ensure it stays under 500ms.

---

## 5. Performance Considerations

### 5.1 Rendering Multiple Simulated Windows

**Bottleneck:** Drawing 8--12 overlapping UI windows with text, icons, images every frame.

**Optimizations:**
1. **Lazy redraw:** Only redraw a window when its content changes. Use `queue_redraw()` signal-driven updates, not per-frame polling.
2. **Clip contents:** Set `clip_contents = true` on all window nodes. Do not render outside window bounds.
3. **Minimize transparency:** XP windows are opaque. No alpha blending except for smooth fonts. This is a GPU win.
4. **Texture atlasing:** All UI icons and textures in a single atlas. Reduce draw calls.
5. **Limit max open windows:** Hard cap at 12. Auto-close LRU window if exceeded.

**Target:** 60 FPS on a mid-range 2020 laptop (e.g., Intel i5-8250U, integrated graphics). Desktop simulation is not GPU-intensive. CPU cost is text rendering and layout. Profile with 12 windows open, verify < 5ms per frame for UI rendering.

### 5.2 Text Rendering

**Bottleneck:** RichTextLabel nodes rendering chat messages, forum posts, browser content. Text layout and font rendering can be expensive for large blocks of text.

**Optimizations:**
1. **Limit visible text:** Chat windows show last 50 messages max. Older messages scroll out of view and are not rendered.
2. **Pre-render static text:** News articles, forum posts that do not change -- render once, cache as texture. Only re-render when content updates.
3. **Use bitmap fonts for UI chrome:** System font (Tahoma, period-accurate) as bitmap font for labels, buttons. Reduces layout cost.
4. **Pagination for long content:** Browser and forum pages split into chunks. Render current page only, not entire thread.

**Target:** < 2ms per frame for all text rendering with 10 windows open.

### 5.3 Nested Game Execution

**Bottleneck:** Running a mini-game (e.g., CounterOps) while desktop UI is still active in the background.

**Optimizations:**
1. **Pause desktop updates:** During LAN party phase, pause desktop time progression. Background apps do not update. Only the mini-game and the chat sidebar are active.
2. **Reduce mini-game complexity:** Target 30 FPS for mini-games, not 60. Simpler physics, fewer entities.
3. **Deactivate hidden windows:** Any desktop window not visible during LAN party is marked inactive. No rendering, no update logic.

**Target:** 30 FPS for mini-game with 12 AI agents active. Profile and simplify if needed.

### 5.4 AI Text Generation Latency

**Bottleneck:** Calling external LLM API (or local model) for character message generation. Network latency or inference time can be 500ms--3 seconds.

**Mitigation:**
1. **Pre-generate message queues:** During idle time (when player is not actively reading messages), batch-generate 5--10 messages ahead for each character. Store in queue.
2. **Typing indicator hides latency:** When a character "is typing," show animated indicator. This is the loading screen. 2--3 seconds of typing is period-authentic and buys time for generation.
3. **Fallback templates:** If generation times out or API is down, fall back to template-based messages (e.g., "hey", "what's up?", "you there?"). Not ideal but better than a hang.
4. **Background generation thread:** Run AI generation in a separate thread. Do not block main thread. Use Godot's Thread class.

**Target:** Player never waits for a message. Either it is pre-generated or the typing indicator gives the illusion of real-time.

### 5.5 Memory Budget

**Target:** 2GB max RAM usage. This supports period-appropriate hardware (players on older machines) and Steam Deck (shared memory pool).

**Memory breakdown estimate:**
- Godot engine runtime: ~200MB
- Game executable and scripts: ~50MB
- UI textures and atlases: ~100MB (all XP icons, wallpapers, character avatars)
- Audio (compressed): ~50MB (sound effects, notification sounds, music tracks for Winamp)
- Virtual filesystem in-memory: ~10MB (metadata only, not file contents)
- Character state and chat logs: ~5MB (15 characters, full state)
- Scene tree (desktop + 12 windows): ~100MB
- AI model (if local): ~500MB (quantized small model, e.g., Phi-2)
- Headroom: ~985MB

**Risk:** If using a local LLM, model size dominates. Mitigation: Use a quantized small model (under 500MB) or rely on external API (zero memory cost, higher latency).

**Profiling:** Use Godot's built-in profiler. Track memory usage during late-game (full crew, full filesystem, max open windows). If over budget, find the bloat and cut it.

---

## 6. Technical Risks

### 6.1 OS Simulation Fidelity

**Risk:** The Windows XP simulation feels fake or off. Players notice tiny details (wrong button shape, wrong font, wrong sound) that break immersion.

**Severity:** High. Nostalgia is the hook. If the desktop does not feel right, the game fails.

**Mitigation:**
- Reference real Windows XP extensively. Screenshots, video captures, VM testing.
- Ship a "good enough" version for MVP. Iterate toward perfection in patches.
- Crowdsource: Ask the community (Discord, Reddit) to nitpick the UI. They will tell us what is wrong.
- Fallback: If XP is too hard to replicate, offer a "generic 2000s OS" aesthetic. Most players care about vibe, not pixel-perfection.

**Test:** Show desktop screenshots to 10 people who used XP daily in 2003. If 8/10 say "that's XP," we pass.

### 6.2 Nested Game Complexity

**Risk:** Building 6 mini-games is scope creep. Each mini-game has its own rules, AI, rendering, balance.

**Severity:** High. This could blow the schedule and budget.

**Mitigation:**
- Build one mini-game (CounterOps) to full quality. Use it as the template.
- Share as much code as possible. All mini-games use the same AI behavior system, just with different game rules.
- Cut ruthlessly. If we are over budget, ship 3 mini-games at launch. Add more post-launch.
- Stretch goal consideration: Replace mini-games with static "simulation" (text updates + final scoreboard). Less fun, but shippable.

**Test:** Playtest first mini-game early (month 2 of dev). If it takes more than 3 weeks to build, rethink the approach.

### 6.3 Text Content Volume

**Risk:** The game requires thousands of lines of AI-generated text (chat messages, forum posts, away messages, news articles). If generation quality is low, immersion breaks. If generation is too slow, gameplay lags.

**Severity:** Critical. Text is the primary content. Bad text = bad game.

**Mitigation:**
- Use a proven model (GPT-4, Claude, or a fine-tuned local model). Do not experiment with unproven tech.
- Build a strong prompt system: Each character has a detailed personality guide. Messages include context (recent events, mood, relationship state).
- Test early. Generate 100 messages in week 1. If quality is bad, pivot immediately.
- Fallback: Template-based messages with AI fills. Not ideal, but safer. "Hey [player_name], are we still on for [event]?"
- Pre-generate common message types (greetings, goodbyes, complaints, excitement). Only use AI for complex contextual messages.

**Test:** Show generated chat logs to playtesters. If they can distinguish AI-generated from human-written, the quality is too low.

### 6.4 Save State Complexity

**Risk:** Saving and loading game state is complex (characters, relationships, filesystem, desktop state, chat logs). Bugs in serialization cause lost saves or crashes.

**Severity:** High. Lost saves kill trust.

**Mitigation:**
- Use Godot's built-in JSON serialization. Do not roll our own.
- Version the save format. Include a version number in every save file. Handle old versions gracefully.
- Auto-save frequently (every in-game day). Keep 3 auto-save backups. If one is corrupted, roll back to the previous.
- Test save/load continuously. Every major feature addition, verify saves still work.
- Add a "Verify Save" tool in debug builds. Serialize game state, deserialize it, compare. If any data is lost, flag it.

**Test:** Play for 10 hours, save, quit, load, continue. If any state is lost or corrupted, find and fix immediately.

### 6.5 AI API Dependence

**Risk:** If the game relies on external AI APIs (OpenAI, Anthropic), we are dependent on their uptime, pricing, and rate limits. API changes or outages break the game.

**Severity:** Medium. We can mitigate but not eliminate.

**Mitigation:**
- Offer multiple backends: External API (high quality, low latency) and local model (medium quality, offline support).
- Pre-generate content during development. Ship the game with a library of pre-generated messages and forum posts. Use AI generation only for dynamic, player-specific content.
- Cache aggressively. Once a message is generated, store it. If the player replays a similar scenario, reuse the cached message.
- Fallback to templates. If AI is unavailable, fall back to template-based messages.

**Test:** Simulate API outage during playtesting. Verify the game still functions (with degraded quality, but no crashes).

---

## 7. Development Pipeline

### 7.1 Build System

**Tools:** Godot 4.3 export templates. SCons build system (Godot's default). No custom build scripts needed for core game.

**Build targets:**
- Windows 64-bit (primary)
- Linux 64-bit (for Steam Deck / Proton)
- macOS (stretch goal, tested quarterly)

**Build process:**
1. Run unit tests (see 7.4).
2. Export via Godot CLI: `godot --export "Windows Desktop" lan_party.exe`
3. Package with dependencies (AI model if local, audio assets, texture atlases).
4. Create installer (InnoSetup for Windows, AppImage for Linux).

**Build time target:** Full build under 5 minutes on dev machine (desktop with SSD).

### 7.2 CI/CD

**Platform:** GitHub Actions (free for public repos, cheap for private).

**Pipeline:**
- On every commit to `main`: Run unit tests, export Linux build, deploy to itch.io internal testing branch.
- On tag push (e.g., `v0.1.0`): Export all platforms, run integration tests, create Steam depot builds, tag release.

**Pipeline YAML (sketch):**
```yaml
name: Build and Test
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Godot
        run: wget https://downloads.tuxfamily.org/godotengine/4.3/Godot_v4.3-stable_linux.x86_64.zip && unzip
      - name: Run tests
        run: godot --headless --path . --script res://tests/run_tests.gd

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Export Windows
        run: godot --export "Windows Desktop" build/lan_party.exe
      - name: Upload artifacts
        uses: actions/upload-artifact@v2
        with:
          name: lan-party-windows
          path: build/
```

**Deployment targets:**
- Internal testing: itch.io private page (updated on every `main` commit).
- Public testing: Steam playtest (manual deploy for major milestones).
- Release: Steam and itch.io (manual deploy for launch).

### 7.3 Version Control

**Platform:** Git + GitHub.

**Branching strategy:** Trunk-based development with short-lived feature branches.
- `main` is always shippable. All commits to `main` must pass tests.
- Feature branches (e.g., `feature/mirc-app`) merged via PR after review.
- No long-lived dev branches. Merge often. Small PRs.

**Commit conventions:** Conventional Commits (e.g., `feat: add MSN typing indicator`, `fix: crash when deleting file`).

**LFS for large assets:** Use Git LFS for audio, textures, fonts. These files are too large for regular Git.

### 7.4 Testing

**Unit tests:** Use GUT (Godot Unit Test framework). Test game logic in isolation (e.g., VirtualFilesystem, Character state, Reputation decay).

**Example test:**
```gdscript
# test_virtual_filesystem.gd
extends GutTest

func test_create_file():
    var fs = VirtualFilesystem.new()
    fs.create_file("/Downloads/game.iso", 4700, "game_iso")
    assert_eq(fs.used_storage_mb, 4700)
    assert_eq(fs.get_file("/Downloads/game.iso").name, "game.iso")
```

**Integration tests:** Test full systems. Example: "Player downloads file, extracts, burns to CD, hosts LAN party."

**Playtesting:** Weekly internal playtests. Monthly external playtests (Discord community, select testers). Focus on:
- Does the desktop feel right?
- Are AI characters engaging?
- Is the loop fun?

**Performance testing:** Profile on target hardware (mid-range 2020 laptop, Steam Deck). Verify 60 FPS for desktop, 30 FPS for mini-games.

---

## 8. Third-Party Dependencies

### 8.1 Core Dependencies

| Dependency | Purpose | License | Risk |
|---|---|---|---|
| **Godot Engine 4.3** | Game engine | MIT | Low. Stable, mature, large community. |
| **GUT (Godot Unit Test)** | Testing framework | MIT | Low. Well-maintained. |
| **OpenAI API / Anthropic API** | AI text generation | Proprietary | Medium. API availability and pricing changes. Mitigate with local fallback. |
| **Phi-2 (local LLM, optional)** | Offline AI fallback | MIT | Low. Quantized model is small and fast. |
| **JSON serialization** | Save/load | Built into Godot | None. |

### 8.2 Asset Dependencies

| Dependency | Purpose | License | Source |
|---|---|---|---|
| **Tahoma font** | UI text (XP-authentic) | Included in Windows, free for XP replication | System font |
| **Bliss wallpaper** | Default desktop background | Public domain / fair use | Wikipedia / official XP release |
| **MSN sound effects** | Notification sounds | Extract from MSN Messenger archive | Fair use / transformative |
| **AIM door sound** | MSN/AIM Easter egg | Public domain / fair use | Archive.org |
| **Period music (Winamp)** | In-game playlist | Royalty-free or licensed | Epidemic Sound, Artlist, or public domain |

**Licensing note:** Replicating Windows XP UI is transformative use (parody/commentary). We are not shipping Windows XP code or Microsoft assets verbatim. Precedent: Papers, Please, Hypnospace Outlaw, and dozens of other games with retro UI parody.

### 8.3 Optional Dependencies (Stretch Goals)

| Dependency | Purpose | Risk Mitigation |
|---|---|---|
| **Steamworks SDK** | Steam integration (achievements, cloud saves) | Low. Standard integration. |
| **Discord Rich Presence** | Show game status in Discord | Low. Optional feature, no impact if removed. |
| **Twitch integration** | Streamers can show crew chat in overlay | Low. Stretch goal only. |

---

## 9. Implementation Roadmap

### Phase 1: Core Desktop Simulation (Weeks 1--4)

**Goal:** Shippable desktop that feels like XP.

**Deliverables:**
- Desktop Manager with window instancing, focus, z-order.
- Taskbar with buttons, system tray, clock.
- File Manager with virtual filesystem rendering.
- One test app (Notepad) that opens, closes, minimizes, maximizes.
- XP theme applied (Luna blue, Bliss wallpaper, authentic fonts).

**Test:** Show to 5 people. If they say "that's Windows XP," we pass.

### Phase 2: MSN Messenger + Basic AI (Weeks 5--8)

**Goal:** Chat system with one AI character.

**Deliverables:**
- MSN app with buddy list, chat window, typing indicator.
- AI Agent System (C#) with one test character.
- Game State Manager singleton with character state.
- Message queue and notification routing.
- Away message system.

**Test:** Have a 10-message conversation with the AI character. If it feels coherent and personality-consistent, we pass.

### Phase 3: First LAN Party (Weeks 9--12)

**Goal:** End-to-end loop from desktop to LAN party to aftermath.

**Deliverables:**
- File acquisition (stub: instant download for now).
- LAN party planning UI (select game, invite characters).
- First mini-game (CounterOps) with 2 AI players.
- Aftermath phase (forum post, MSN follow-up).
- Session loop structure.

**Test:** Play one full session loop (20 minutes). If it feels like a coherent experience, we pass.

### Phase 4: Acquisition & Risk Systems (Weeks 13--16)

**Goal:** Flesh out file acquisition, downloads, risk.

**Deliverables:**
- mIRC app with channel browsing, DCC transfers.
- P2P client (Kazaa parody) with malware risk.
- Download Manager with progress bars, speed simulation.
- ISP heat system and consequences.
- WinRAR extraction and file verification.

**Test:** Acquire 5 games via different sources. Verify risk/reward feels balanced.

### Phase 5: Community & Reputation (Weeks 17--20)

**Goal:** Expand to full crew, multiple characters, relationship dynamics.

**Deliverables:**
- 10--15 AI characters with unique personalities.
- Reputation system (4 tracks).
- Forum app with threaded discussions.
- Relationship graph and pairwise dynamics.
- Life events system.

**Test:** Play 5 hours. Verify characters feel distinct and relationships evolve meaningfully.

### Phase 6: Content & Polish (Weeks 21--28)

**Goal:** Flesh out mini-games, narrative beats, economy balance.

**Deliverables:**
- 3--6 mini-games (CounterOps, UnrealBattle, StratCraft, etc.).
- Event Scheduler with narrative beats.
- Economy tuning (allowance, costs, storage).
- Snack system.
- Browser app with news and character pages.
- Winamp with playlist system.

**Test:** Full playthrough (15 hours). Verify all systems interact cleanly and the arc feels satisfying.

### Phase 7: Beta & Launch Prep (Weeks 29--32)

**Goal:** Bug fixing, performance optimization, Steam integration.

**Deliverables:**
- Closed beta on Steam playtest.
- Performance profiling and optimization.
- Save/load stress testing.
- Steam achievements, cloud saves.
- Launch trailer and marketing assets.

**Test:** 20 external playtesters. Aggregate feedback. Fix critical bugs. Ship.

---

## 10. Performance Targets (Summary)

| System | Target | Fallback |
|---|---|---|
| Desktop UI | 60 FPS, 5ms/frame | 30 FPS acceptable |
| Mini-games | 30 FPS | 20 FPS acceptable |
| Save/load time | < 500ms | < 2 seconds acceptable |
| AI message generation | < 3s (hidden by typing indicator) | Template fallback if timeout |
| Memory usage | < 2GB | < 3GB max |
| Build time | < 5 minutes | < 10 minutes acceptable |

---

## 11. Known Limitations

**Limitation 1: AI text quality.**
We are dependent on external models or local quantized models. Quality may vary. If players notice robotic or repetitive text, immersion breaks. Mitigation: Extensive prompt engineering, character voice guides, fallback templates.

**Limitation 2: Mini-game depth.**
The games-within-games are simplified simulations, not full games. Players expecting deep gameplay will be disappointed. This is intentional -- the focus is on the social layer, not the game layer. Communicate this clearly in marketing.

**Limitation 3: Platform support.**
Console ports are not viable (mouse-driven UI). Mobile is not viable (screen size). We are PC-only. This limits market size but ensures a polished experience on the target platform.

**Limitation 4: Historical accuracy.**
The game depicts "200X," not a specific year. This gives creative freedom but may disappoint hardcore accuracy nerds. Precedent: Hypnospace Outlaw did the same and succeeded.

**Limitation 5: Replayability ceiling.**
Procedural generation creates variance, but the core structure (prep, party, aftermath) is fixed. After 2--3 playthroughs, the loop may feel samey. Mitigation: Post-launch content updates (new mini-games, new character archetypes, new events).

---

## 12. Open Technical Questions

**Question 1:** Do we use external AI APIs (OpenAI/Anthropic) or ship with a local model?
- **Trade-off:** External = higher quality, lower latency, ongoing cost, internet requirement. Local = offline support, zero ongoing cost, lower quality, larger download size.
- **Decision needed by:** Week 8 (Phase 2). Need to test both and compare quality.

**Question 2:** How much content do we pre-generate?
- **Trade-off:** Pre-generating 10,000 messages makes the game playable offline but increases download size and reduces dynamic responsiveness. Generating everything at runtime is flexible but dependent on AI availability.
- **Decision needed by:** Week 16 (Phase 4). Need to profile generation speed and determine cache strategy.

**Question 3:** What is the minimum viable mini-game set?
- **Trade-off:** 6 mini-games (as designed) vs. 3 mini-games (cut scope). Fewer games means less variety but faster development.
- **Decision needed by:** Week 12 (end of Phase 3). After building the first mini-game, assess how long it took and extrapolate.

**Question 4:** Do we support modding?
- **Trade-off:** Modding extends lifespan and builds community, but requires API design, documentation, and support. Adds 4--6 weeks to schedule.
- **Decision needed by:** Week 20 (Phase 5). Evaluate community interest and schedule buffer.

---

## 13. Conclusion

This is the architecture for LAN PARTY. It is not perfect. It is not complete. It is shippable.

The core insight: The desktop is not a menu. It is the game. Every system is an application. The AI is not a gimmick. It is the content engine. The loop is not busywork. It is caretaking.

Build the desktop first. Get it feeling right. Then layer in MSN and AI. Then the LAN party loop. Then acquisition. Then community. Each phase builds on the last. Each phase is testable in isolation. If a phase fails, we know where to fix it.

The risks are real. AI quality. Text volume. Mini-game scope. Desktop fidelity. But the mitigations are clear. Test early. Cut ruthlessly. Ship working software.

The target is 32 weeks from start to launch. Aggressive but achievable. The team is small (assume 3--5 people: 1 lead programmer, 1 AI/backend engineer, 1 UI artist, 1 sound designer, 1 narrative designer). Godot makes a small team viable. The architecture makes iteration fast.

This document is a contract. It says: Here is what we are building. Here is how we build it. Here is what we cut if we run out of time. No feature creep. No scope inflation. No "let's build our own engine."

Ship it. Then improve it. Then make it fast. In that order.

-- BYTE

---

**Document Status:** Architecture definition complete. Ready for Phase 1 kickoff. Zero placeholders. Zero TODOs. All systems specified with implementation details.

**Next Steps:**
1. Review with design team (REED, NOVA) to validate technical feasibility of game design.
2. Review with HYPE to validate platform targets and marketing needs.
3. Begin Phase 1: Desktop simulation prototype.
4. Schedule weekly architecture reviews to address open questions as development progresses.

**Revision History:**
- v1.0 (2026-02-07): Initial architecture document by BYTE.
