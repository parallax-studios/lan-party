# LAN PARTY -- Production Plan

**Producer:** CLOCK
**Status:** Pre-Production Complete, Production Roadmap Defined
**Date:** 2026-02-07
**Target Platform:** PC (Steam), Steam Deck secondary
**Target Release:** Q4 2026 (32 weeks from greenlight)
**Team Size:** 5 core + contractors

---

## 1. Project Overview

### 1.1 What We Are Building

A management simulation game set inside a fully playable Windows XP desktop. Players build and maintain a LAN party crew in the early 2000s through desktop applications powered by AI-driven characters. The entire game is played through MSN Messenger, mIRC, file managers, CD burners, and a simulated OS.

This is not a traditional game. This is a playable time capsule where every mechanic is wrapped in period-authentic interface design and every character is an AI agent with persistent memory and personality.

### 1.2 Scope Statement

**Core Loop (Non-Negotiable):**
- Desktop simulation (Windows XP-era OS with functional applications)
- AI-driven character relationships (15 characters, persistent state, dynamic messaging)
- Acquisition system (download/pirate games, manage risk)
- LAN party hosting (planning, execution, aftermath)
- Emergent narrative through interfaces (no cutscenes, story through chat/forums)

**MVP Feature Set:**
- 5 desktop applications: MSN Messenger, mIRC, File Manager, CD Burner, Winamp
- 10-15 AI characters with unique personalities
- 3-4 mini-games for LAN party events
- Virtual filesystem with storage constraints
- Reputation system (4 tracks: Friends, Forum, IRC, Scene)
- 15-25 hour playthrough (one full meta loop)

**Stretch Goals (Cut if schedule slips):**
- Additional mini-games (target 6 total, floor 3)
- Browser with GeoCities pages and news sites
- Mixtape system (burn CDs as relationship gifts)
- Hardware modding/upgrade system
- Advanced post-processing (CRT shader, scanlines)

**Hard Cuts (Not in scope):**
- Multiplayer (single-player only)
- Voice acting (text-only by design)
- 3D environments (desktop UI is the world)
- Console ports (PC/Steam Deck only)
- Real licensed games (all parody titles)

### 1.3 Team Structure

**Core Team (5):**
- Lead Programmer/Tech Lead (BYTE role) -- 1 FTE
- AI/Backend Engineer -- 1 FTE
- UI Artist/Pixel Artist (PIXEL role) -- 1 FTE
- Sound Designer (ECHO role) -- 0.5 FTE
- Narrative/Game Designer (REED + NOVA roles) -- 1 FTE

**Contractors (as needed):**
- Music Composer (20-40 tracks, milestone-based)
- QA Lead (CRASH role, part-time weeks 20-32)
- Marketing/Community Manager (HYPE role, part-time weeks 24-32)

**Support:**
- Producer (CLOCK, this document, ongoing oversight)

### 1.4 Budget Constraints

Assume indie budget. Key cost drivers:
- Salaries (5 FTE for 32 weeks)
- AI API costs (if using external LLM, estimated $500-2000 total for development)
- Software licenses (Godot is free, FMOD license ~$500, misc tools ~$500)
- Music composition (contract, $150-300 per track x 20-40 tracks = $3,000-12,000)
- Marketing/PR (Steam page, trailer production, influencer keys, ~$5,000)
- Platform fees (Steam partner fee $100, Steamworks setup)

Total estimated budget (excluding salaries): $10,000-20,000.

Critical: No feature creep. Every dollar spent outside this plan comes from contingency or cuts scope.

### 1.5 Timeline Summary

**Duration:** 32 weeks from greenlight to launch.

**Key Dates:**
- Week 0: Greenlight and team onboarding
- Week 4: Desktop simulation vertical slice
- Week 8: MSN + AI character prototype
- Week 12: First full session loop playable
- Week 20: Feature complete (all systems implemented)
- Week 28: Content complete (all narrative beats, all mini-games)
- Week 32: Launch

**Milestone Gates:**
- Gate 1 (Week 4): Desktop feels like XP. If not, reevaluate art direction.
- Gate 2 (Week 8): AI chat feels human. If not, pivot to templates or change model.
- Gate 3 (Week 12): Core loop is fun. If not, rework systems before continuing.
- Gate 4 (Week 20): Full playthrough is possible. If not, cut scope to hit Week 28.

**Risk Buffer:** 4 weeks built into phases 6-7. If ahead of schedule, add stretch goals. If behind, cut ruthlessly.

---

## 2. Milestone Definitions

Milestones have entry criteria (what must be true to start), deliverables (what we build), exit criteria (what must be true to finish), and success metrics.

### Milestone 1: Prototype -- Desktop Simulation (Weeks 1-4)

**Entry Criteria:**
- Team onboarded, dev environment set up
- Godot 4.3 installed and tested on all machines
- Art direction document reviewed and approved
- Reference library assembled (XP screenshots, MSN videos, forum archives)

**Deliverables:**
1. **Desktop OS Simulation:**
   - Taskbar (Luna Blue theme, Start button, system tray, clock)
   - Desktop with icons (My Computer, Recycle Bin, app shortcuts)
   - Window Manager (open, close, minimize, maximize, drag, z-order)
   - XP theme applied (authentic colors, fonts, button styles)
   - Wallpaper system (Bliss default, swappable)

2. **One Test Application:**
   - Notepad-style app (simple text editor)
   - Can open, edit text, save/load, close

3. **Audio Foundation:**
   - Mouse click sounds (5 variants)
   - Window open/close sounds
   - Basic desktop ambiance (CRT hum, HDD idle loop)

4. **Technical Foundation:**
   - Game State Manager singleton (empty structure, ready for data)
   - Save/load system (serialize desktop state to JSON)
   - Input handling (mouse, keyboard, shortcuts like Alt-Tab)

**Exit Criteria:**
- Desktop boots and renders at 60 FPS on target hardware (mid-range 2020 laptop)
- Windows can be opened, moved, closed without visual glitches
- Theme matches reference XP screenshots (passes squint test)
- Save/load works (desktop state persists across sessions)
- Zero crashes during 30-minute stress test (open/close 50 windows)

**Success Metrics:**
- 8/10 playtesters say "this feels like Windows XP" without prompting
- UI rendering < 5ms per frame with 12 windows open
- Save file size < 50KB uncompressed

**Risks:**
- XP theme fidelity too hard to achieve in Godot. Mitigation: Ship "good enough" for milestone, iterate in Phase 6.
- Window management performance issues. Mitigation: Profile early, optimize rendering path.

---

### Milestone 2: Vertical Slice -- MSN + AI Character (Weeks 5-8)

**Entry Criteria:**
- Milestone 1 passed (desktop is functional)
- AI backend selected (OpenAI API vs. local model decision made)
- Character personality framework defined (NOVA's archetypes documented)

**Deliverables:**
1. **MSN Messenger Application:**
   - Buddy list window (scrollable contact list, status icons, away messages)
   - Chat window (per-contact, message history, text input, send button)
   - Typing indicator ("Character is typing...")
   - Notification system (taskbar flash, popup, MSN sounds)
   - Nudge feature (window shake + sound)

2. **AI Agent System (C# Module):**
   - Character state model (personality, mood, relationships, desires, memory)
   - Message generation pipeline (context assembly, API call, response parsing)
   - Typing simulation (latency hiding via "is typing" indicator)
   - One test character (The Prodigy archetype, fully implemented)

3. **Game State Manager Expansion:**
   - Character database (stores all character state)
   - Message queue (incoming/outgoing messages)
   - Relationship graph (pairwise relationship values)
   - Timeline clock (in-game time, 1x/2x/4x speed, pause)

4. **Notification Routing:**
   - Desktop Manager receives signals from MSN app
   - Routes notifications to audio system and UI (taskbar flash)

**Exit Criteria:**
- Player can have a 10-message conversation with AI character
- Character personality is consistent across messages
- Typing indicator successfully hides API latency
- Relationship value changes based on player choices
- Away messages update dynamically based on character mood
- No message generation failures during 1-hour playtest

**Success Metrics:**
- AI-generated text quality: Playtesters cannot distinguish from human-written 80% of the time
- Latency: < 3 seconds per message (hidden by typing indicator)
- Relationship tracking: Player choices measurably affect character mood/relationship

**Risks:**
- AI text quality is poor (robotic, repetitive). Mitigation: Extensive prompt engineering. If still bad, pivot to template-based system with AI fills.
- API latency too high (> 5 seconds). Mitigation: Pre-generate message queues during idle time. Add fallback templates.

---

### Milestone 3: Alpha -- First Full Session Loop (Weeks 9-12)

**Entry Criteria:**
- Milestone 2 passed (MSN + AI working)
- Mini-game design spec complete (CounterOps mechanics documented)
- LAN party UI mockups approved

**Deliverables:**
1. **File Acquisition System (Simplified):**
   - Download manager (progress bars, speed simulation)
   - Virtual filesystem (create/delete files, track storage)
   - Stub download sources (instant downloads for now, full piracy system in Phase 4)

2. **LAN Party Planning:**
   - Party setup UI (select game, invite characters via MSN)
   - Attendance simulation (characters accept/decline based on relationship)
   - Hardware inventory (stub system, simple list of available rigs)

3. **First Mini-Game (CounterOps):**
   - Top-down tactical shooter simulation
   - 2 teams of 3 AI agents
   - Simple AI behavior (move, shoot, plant/defuse bomb)
   - Match resolution (win/loss, MVP tracking)
   - Post-match events (rage-quits, bonding moments, rivalry triggers)

4. **LAN Party Execution Phase:**
   - Game viewport (watchable mini-game)
   - Chat sidebar (real-time AI character messages during game)
   - Party energy meter (visual progress bar)
   - Player interventions (swap game, call break)

5. **Aftermath Phase:**
   - Return to desktop
   - Forum stub (one thread appears with party recap)
   - MSN follow-up messages (characters comment on party)
   - Relationship updates applied

**Exit Criteria:**
- Player can complete one full session loop in 20-30 minutes
- Loop structure is clear: Prep -> Party -> Aftermath -> Prep
- CounterOps mini-game runs at 30 FPS with 6 AI agents
- Relationship changes feel meaningful (player sees impact of party quality)
- No crashes during full loop playthrough

**Success Metrics:**
- Playtesters say "I want to do another party" after first loop
- Party quality score correlates with relationship changes (tested with 5 parties)
- Mini-game is watchable and generates emergent moments (1-2 notable events per match)

**Risks:**
- Mini-game complexity too high. Mitigation: Build simplest possible version. If still over budget, replace with static simulation (text updates + scoreboard).
- Session loop too long (>40 minutes). Mitigation: Compress prep phase, streamline party execution.

---

### Milestone 4: Beta -- Core Systems Complete (Weeks 13-20)

**Entry Criteria:**
- Milestone 3 passed (session loop works)
- Acquisition design finalized (piracy risk mechanics documented)
- Character roster complete (10-15 personalities defined)

**Deliverables:**
1. **Full Acquisition System:**
   - mIRC application (channel browsing, DCC transfers)
   - P2P client (Kazaa parody, search/download with malware risk)
   - Private tracker sites (browser pages, ratio system)
   - ISP heat system (accumulates with piracy, triggers warnings/throttling)
   - File verification (extract RARs, check integrity, scan for malware)

2. **Expanded Character Roster:**
   - 10-15 AI characters (all archetypes implemented)
   - Unique personalities, moods, relationships, desires
   - Life events system (job offers, moving away, personal crises)
   - Online presence patterns (schedules, status changes)

3. **Reputation System:**
   - Four tracks: Friend Group, Forum, IRC, Warez Scene
   - Reputation decay (idle time reduces standing)
   - Reputation gates (unlock better sources, moderator status, scene access)
   - Visible feedback (forum title changes, IRC channel invites)

4. **Forum Application:**
   - phpBB-style threaded discussions
   - AI-generated posts (characters discuss parties, games, drama)
   - Player posting (affects reputation)
   - Thread lifecycle (posts accumulate over time)

5. **Additional Mini-Games (2-3 more):**
   - UnrealBattle (arena deathmatch)
   - StratCraft (RTS abstraction)
   - RallyRacer or FightZone (stretch, cut if behind)

6. **Economy System:**
   - Weekly allowance
   - Costs (blank CDs, snacks, legitimate game purchases, hardware)
   - Storage constraints (40GB HDD limit enforced)
   - Snack system (party morale mechanic)

**Exit Criteria:**
- 10-15 characters feel distinct and memorable
- Acquisition channels have meaningful risk/reward differences
- Reputation in all four tracks affects gameplay (unlocks, character reactions)
- 3-4 mini-games available for LAN parties
- Economy creates meaningful trade-offs (cannot afford everything)
- No game-breaking bugs (crashes, save corruption, soft-locks)

**Success Metrics:**
- Playtesters can name 3+ characters and describe their personalities without notes
- Piracy risk feels balanced (not too safe, not too punishing)
- Full playthrough (5 hours) is possible without hitting blockers

**Risks:**
- Character roster too large (AI generation costs spike). Mitigation: Start with 10 characters, add 5 more only if budget allows.
- Mini-game development behind schedule. Mitigation: Cut to 3 total, add more post-launch.
- Forum content volume overwhelming. Mitigation: Limit active threads to 10-15, archive old threads.

---

### Milestone 5: Release Candidate -- Content Complete (Weeks 21-28)

**Entry Criteria:**
- Milestone 4 passed (all systems functional)
- Full playthrough (15 hours) completed internally without critical bugs
- Narrative beats mapped and implemented

**Deliverables:**
1. **Event Scheduler & Narrative System:**
   - Event Scheduler (time-gated triggers, life events, narrative beats)
   - Narrative beats (first party, first rivalry, first loss, fracture phase, finale)
   - Character arc tracking (personality evolution based on player choices)

2. **Browser Application:**
   - Internet Explorer-style UI
   - Gaming news sites (procedurally generated headlines)
   - Character GeoCities pages (personality-based homepages)
   - Private tracker sites (functional download browsing)

3. **Winamp & Music System:**
   - Winamp classic skin UI
   - Playlist editor
   - 20-40 music tracks (original compositions, license-safe)
   - Volume/playback controls
   - Visualizer (5 modes)

4. **Polish & Juice:**
   - CRT shader (optional post-processing)
   - Scanlines and phosphor glow effects
   - Window drop shadows
   - Tooltip system
   - Loading screens (styled as XP boot sequence)
   - Settings menu (audio sliders, CRT toggle, resolution)

5. **Full Meta Loop (15-25 hours):**
   - Genesis phase (weeks 1-3 in-game)
   - Growth phase (weeks 4-10)
   - Golden phase (weeks 11-14)
   - Fracture phase (weeks 15-18)
   - Finale phase (weeks 19-22)
   - Epilogue (character fates, last desktop moment)

**Exit Criteria:**
- Full 15-hour playthrough completed by 3 internal testers
- All narrative beats trigger correctly in at least 1 playthrough
- Music system functional (player can build playlists, tracks play/pause/skip)
- No critical bugs (game-breaking issues fixed)
- Performance targets met (60 FPS desktop, 30 FPS mini-games)

**Success Metrics:**
- Playtesters report emotional resonance (bittersweet ending hits)
- Meta arc pacing feels correct (not too fast, not too slow)
- Music enhances atmosphere (tested with music on vs. off)

**Risks:**
- Narrative beats feel scripted/forced. Mitigation: Make triggers flexible, allow multiple paths to same emotional beats.
- Content volume too high (40 tracks + all text). Mitigation: Cut music to 20 tracks minimum, rely on AI generation for text.
- Meta loop too long (>25 hours). Mitigation: Compress middle phases, add time-skip option.

---

### Milestone 6: Gold -- Launch Readiness (Weeks 29-32)

**Entry Criteria:**
- RC passed (content complete, playable end-to-end)
- External playtest completed (10-20 testers, feedback aggregated)
- Steam page live (wishlist campaign started)

**Deliverables:**
1. **QA & Bug Fixing:**
   - Full QA pass by CRASH (bug database, priority triage)
   - Critical bugs fixed (crashes, save corruption, progression blockers)
   - High-priority bugs fixed (UI glitches, AI failures, performance issues)
   - Medium/low bugs deferred to post-launch patches

2. **Steam Integration:**
   - Steamworks SDK integrated
   - Achievements (10-15 achievements tied to game milestones)
   - Cloud saves
   - Trading cards (if approved)
   - Steam Deck verification (tested on hardware, compatibility flags set)

3. **Performance Optimization:**
   - Profiling on min-spec hardware (verify 60 FPS desktop, 30 FPS mini-games)
   - Memory usage under 2GB
   - Load times < 5 seconds (desktop boot)
   - Save/load times < 500ms

4. **Marketing Assets:**
   - Launch trailer (2 minutes, desktop screen recording + music)
   - Key art (CRT basement scene)
   - Steam capsule images (header, library assets)
   - Press kit (screenshots, fact sheet, press release)
   - Influencer key distribution plan

5. **Launch Checklist:**
   - Build finalized and uploaded to Steam
   - Patch 1.01 prepared (day-one fixes for known low-priority bugs)
   - Support channels ready (Discord, email)
   - Review embargo plan (send keys to press 1 week early)

**Exit Criteria:**
- Zero critical bugs in final build
- Steam build uploaded and tested (can download and run from Steam client)
- Performance targets met on min-spec hardware
- Launch trailer approved and scheduled
- Marketing plan executed (press keys sent, social media ready)

**Success Metrics:**
- QA pass rate: < 10 critical bugs found in final week
- Playtest feedback positive (80%+ "would recommend")
- Steam Deck verified status achieved

**Risks:**
- Critical bug found in final week. Mitigation: 1-week buffer before launch, can delay if necessary.
- Steam approval delays. Mitigation: Submit build early (week 30), allow 2 weeks for Valve review.

---

## 3. Sprint Plan & Task Breakdown

Sprints are 2-week cycles. Each sprint has a theme, deliverables, task assignments, and dependencies.

### Sprint 1-2 (Weeks 1-4): Desktop Foundation

**Theme:** Build the stage. Make XP come alive.

**Lead:** BYTE (Tech Lead)

**Tasks:**

| Task | Owner | Estimate (days) | Dependency | Priority |
|---|---|---|---|---|
| Set up Godot project structure | BYTE | 1 | None | P0 |
| Implement Window Manager (instancing, focus, z-order) | BYTE | 3 | Project setup | P0 |
| Design XP theme (colors, fonts, UI assets) | PIXEL | 5 | None | P0 |
| Implement Taskbar (buttons, system tray, clock) | BYTE | 2 | Window Manager | P0 |
| Implement Desktop (icons, wallpaper, drag-drop) | BYTE | 2 | Taskbar | P0 |
| Create window chrome assets (title bars, borders, buttons) | PIXEL | 3 | Theme design | P0 |
| Implement window dragging and resizing | BYTE | 2 | Window Manager | P1 |
| Build test Notepad app | BYTE | 1 | Window Manager | P1 |
| Record/source desktop SFX (clicks, window sounds) | ECHO | 2 | None | P1 |
| Implement audio system (FMOD setup or Godot audio) | BYTE | 2 | None | P1 |
| Integrate desktop SFX | BYTE | 1 | Audio system, SFX ready | P1 |
| Build save/load system (JSON serialization) | BYTE | 2 | Desktop complete | P1 |
| Playtesting: XP fidelity check | CLOCK | 1 | Desktop + theme done | P0 |

**Milestone Gate (Week 4):** Desktop feels like XP. If not, reevaluate art direction or accept "good enough" and document iteration plan.

---

### Sprint 3-4 (Weeks 5-8): MSN + AI

**Theme:** Make the desktop talk back.

**Lead:** AI/Backend Engineer

**Tasks:**

| Task | Owner | Estimate (days) | Dependency | Priority |
|---|---|---|---|---|
| Design character data model | Narrative Designer | 2 | None | P0 |
| Implement Game State Manager singleton | BYTE | 2 | None | P0 |
| Build MSN UI (buddy list, chat window) | PIXEL + BYTE | 4 | Desktop foundation | P0 |
| Implement typing indicator | BYTE | 1 | MSN UI | P1 |
| Set up AI backend (C# module or API wrapper) | AI Engineer | 3 | None | P0 |
| Implement character state system | AI Engineer | 3 | Data model, Game State Manager | P0 |
| Build message generation pipeline | AI Engineer | 4 | AI backend, character state | P0 |
| Create one test character (The Prodigy) | Narrative Designer | 2 | Character model | P0 |
| Integrate MSN with AI system | AI Engineer + BYTE | 3 | MSN UI, AI pipeline | P0 |
| Build notification routing (signals, taskbar flash) | BYTE | 2 | MSN integration | P1 |
| Record/source MSN sounds (message, sign-in, nudge) | ECHO | 1 | None | P1 |
| Implement away message system | AI Engineer | 2 | Character state | P2 |
| Implement nudge feature | BYTE | 1 | MSN UI | P2 |
| Playtesting: AI chat quality check | CLOCK | 2 | Full MSN + AI working | P0 |

**Milestone Gate (Week 8):** AI chat feels human. If not, pivot to template system or change model.

---

### Sprint 5-6 (Weeks 9-12): First Session Loop

**Theme:** Close the loop. Prep, party, aftermath.

**Lead:** REED (Game Designer) + BYTE

**Tasks:**

| Task | Owner | Estimate (days) | Dependency | Priority |
|---|---|---|---|---|
| Design CounterOps mini-game mechanics | REED | 2 | None | P0 |
| Implement virtual filesystem | BYTE | 3 | Game State Manager | P0 |
| Build download manager UI | BYTE | 2 | Filesystem | P1 |
| Stub file acquisition (instant downloads) | BYTE | 1 | Download manager | P1 |
| Build LAN party planning UI (game select, invites) | BYTE + PIXEL | 3 | MSN integration | P0 |
| Implement attendance simulation (accept/decline logic) | AI Engineer | 2 | Character state | P0 |
| Build CounterOps mini-game scene | BYTE | 5 | Mini-game design | P0 |
| Implement AI agent behavior for mini-games | AI Engineer | 4 | CounterOps scene | P0 |
| Build LAN party execution UI (game viewport, chat sidebar, energy meter) | BYTE + PIXEL | 4 | Mini-game ready | P0 |
| Implement player interventions (swap game, break) | BYTE | 2 | Execution UI | P1 |
| Build aftermath phase (forum stub, MSN follow-up) | BYTE + AI Engineer | 3 | Party execution | P0 |
| Apply relationship changes post-party | AI Engineer | 2 | Aftermath phase | P0 |
| Create party event stingers (rage-quit, clutch, bonding) | ECHO | 2 | None | P1 |
| Playtesting: Full session loop playthrough | CLOCK | 2 | All systems integrated | P0 |

**Milestone Gate (Week 12):** Core loop is fun. If not, rework before continuing.

---

### Sprint 7-10 (Weeks 13-20): Beta Systems

**Theme:** Depth. Risk. Community. Reputation.

**Lead:** BYTE + AI Engineer

**Tasks (High-Level, 4 sprints):**

| Task | Owner | Estimate (days) | Dependency | Priority |
|---|---|---|---|---|
| Build mIRC application | BYTE + PIXEL | 5 | Desktop foundation | P0 |
| Implement DCC transfer system | BYTE | 3 | mIRC UI | P0 |
| Build P2P client UI | BYTE + PIXEL | 4 | Desktop foundation | P1 |
| Implement malware risk system | BYTE | 3 | Filesystem | P1 |
| Build ISP heat accumulation system | BYTE | 2 | Game State Manager | P1 |
| Implement file verification (extract, scan) | BYTE | 2 | Filesystem | P2 |
| Create 10-15 AI characters (full roster) | Narrative Designer + AI Engineer | 10 | Character system | P0 |
| Implement life events system | AI Engineer | 4 | Character state | P0 |
| Build reputation system (4 tracks) | BYTE | 4 | Game State Manager | P0 |
| Implement reputation decay | BYTE | 2 | Reputation system | P1 |
| Build forum application | BYTE + PIXEL | 5 | Desktop foundation | P0 |
| Implement AI-generated forum posts | AI Engineer | 4 | Forum UI | P0 |
| Build 2-3 additional mini-games | BYTE | 10 | First mini-game template | P1 |
| Implement economy system (allowance, costs, storage) | BYTE | 3 | Game State Manager | P1 |
| Build snack system | BYTE | 2 | Economy system | P2 |
| Playtesting: 5-hour playthrough | CLOCK | 3 | All beta systems done | P0 |

**Milestone Gate (Week 20):** Full playthrough possible. If not, cut scope to hit Week 28.

---

### Sprint 11-14 (Weeks 21-28): Content & Polish

**Theme:** Story. Music. Juice.

**Lead:** Narrative Designer + ECHO + PIXEL

**Tasks (High-Level, 4 sprints):**

| Task | Owner | Estimate (days) | Dependency | Priority |
|---|---|---|---|---|
| Implement Event Scheduler | BYTE | 3 | Game State Manager | P0 |
| Design narrative beats (15-20 beats) | Narrative Designer | 5 | None | P0 |
| Implement narrative beat system | AI Engineer | 4 | Event Scheduler | P0 |
| Build browser application | BYTE + PIXEL | 5 | Desktop foundation | P1 |
| Create procedural news headlines | AI Engineer | 2 | Browser UI | P2 |
| Create character GeoCities pages | Narrative Designer + PIXEL | 4 | Browser UI | P2 |
| Build Winamp application | BYTE + PIXEL | 4 | Desktop foundation | P1 |
| Compose 20-40 music tracks | Composer (contractor) | 20 | None | P1 |
| Integrate music system | BYTE | 2 | Winamp UI, music ready | P1 |
| Implement CRT shader & post-processing | BYTE | 3 | None | P2 |
| Create all remaining UI assets (icons, buttons, etc.) | PIXEL | 10 | None | P1 |
| Record/source all remaining SFX | ECHO | 5 | None | P1 |
| Mix and balance audio | ECHO | 4 | All SFX + music ready | P1 |
| Build settings menu | BYTE | 2 | None | P2 |
| Playtesting: Full 15-hour meta loop | CLOCK | 5 | All content complete | P0 |

**Milestone Gate (Week 28):** Content complete. If not, cut remaining scope and move to QA.

---

### Sprint 15-16 (Weeks 29-32): Gold & Launch

**Theme:** Ship it.

**Lead:** CRASH (QA Lead) + CLOCK

**Tasks:**

| Task | Owner | Estimate (days) | Dependency | Priority |
|---|---|---|---|---|
| External playtest recruitment | CLOCK | 1 | RC build | P0 |
| External playtest execution | CRASH | 5 | Testers recruited | P0 |
| Bug triage and prioritization | CRASH + CLOCK | 2 | Playtest feedback | P0 |
| Critical bug fixes | BYTE + AI Engineer | 5 | Bug triage | P0 |
| High-priority bug fixes | BYTE | 3 | Critical bugs done | P1 |
| Performance profiling and optimization | BYTE | 3 | Bug fixes done | P0 |
| Integrate Steamworks SDK | BYTE | 2 | None | P0 |
| Implement Steam achievements | BYTE | 2 | Steamworks integration | P1 |
| Implement cloud saves | BYTE | 1 | Steamworks integration | P1 |
| Steam Deck testing | BYTE | 2 | Build ready | P1 |
| Create launch trailer | HYPE (contractor) | 5 | Content complete | P0 |
| Create marketing assets (key art, capsules) | PIXEL + HYPE | 3 | None | P0 |
| Build Steam page | HYPE | 2 | Marketing assets ready | P0 |
| Prepare press kit | HYPE | 2 | Marketing assets ready | P1 |
| Upload final build to Steam | BYTE | 1 | All fixes done | P0 |
| Prepare patch 1.01 (day-one fixes) | BYTE | 2 | Final build uploaded | P2 |
| Final QA pass on Steam build | CRASH | 2 | Build uploaded | P0 |
| Launch | CLOCK | 1 | All tasks complete | P0 |

**Milestone Gate (Week 32):** Launch. No gate, we ship.

---

## 4. Risk Register

Risks are rated by likelihood (Low/Medium/High) and impact (Low/Medium/High). Mitigation strategies are defined.

| Risk | Likelihood | Impact | Mitigation | Contingency |
|---|---|---|---|---|
| **AI text quality is poor** | Medium | Critical | Extensive prompt engineering, personality guides, early testing. | Pivot to template-based system with AI fills. Cut AI to flavor text only, use templates for core content. |
| **AI API costs spike** | Low | High | Pre-generate common messages, cache aggressively, monitor usage daily. | Switch to local model (Phi-2 quantized). Accept quality drop but eliminate API cost. |
| **AI API downtime breaks game** | Medium | Medium | Offer offline mode with local model fallback. Pre-generate message queues. | Ship with 10,000 pre-generated messages. AI enhances but is not required. |
| **Mini-game scope creep** | High | High | Build one mini-game fully, template the rest. Cut to 3 total if behind schedule. | Replace mini-games with static simulations (text updates + scoreboard). Less fun, but shippable. |
| **Desktop fidelity not authentic enough** | Medium | High | Reference real XP extensively, crowdsource nitpicking from community. | Ship "generic 2000s OS" aesthetic. Most players care about vibe, not pixel-perfection. |
| **Character roster too large (costs/complexity)** | Medium | Medium | Start with 10 characters, add 5 more only if budget allows. | Cap at 10 characters. Quality over quantity. |
| **Session loop too long (>40 minutes)** | Low | Medium | Compress prep phase, streamline party execution. Test and iterate early. | Add time-skip option for expert players. Fast-forward idle time. |
| **Meta loop too long (>25 hours)** | Low | Medium | Compress middle phases, add time-skip option. | Cut to 12-15 hour playthrough. Tighten pacing. |
| **Save corruption bug** | Low | Critical | Auto-save frequently, keep 3 backups, version save format. | Rollback to previous save. Warn players, provide save repair tool. |
| **Performance issues (< 60 FPS desktop)** | Medium | High | Profile early and often. Optimize rendering path, limit max windows. | Lower target to 30 FPS. Most players will accept this for a UI-driven game. |
| **Steam Deck compatibility issues** | Medium | Medium | Test monthly on Deck hardware. Use Deck-friendly control scheme. | Drop Deck verification, ship as playable but unverified. |
| **Critical bug found in final week** | Medium | Critical | 1-week buffer before launch. QA starts week 29, not week 31. | Delay launch by 1-2 weeks. Better to delay than ship broken. |
| **Team member leaves mid-project** | Low | High | Cross-train team members, document all systems. | Contractor replacement for key roles (BYTE, AI Engineer). Delay if necessary. |
| **Music composition behind schedule** | Medium | Medium | Contract early, milestone-based delivery, accept fewer tracks. | Ship with 10-15 tracks, add more post-launch as free update. |
| **Marketing budget exhausted** | Low | Medium | Focus on organic (Reddit, Twitter, influencer outreach). Free demo. | Rely on word-of-mouth. This game's hook (nostalgia + AI) is viral-friendly. |

---

## 5. Critical Path

The critical path is the sequence of tasks that, if delayed, will delay the entire project. All tasks on this path are P0 priority.

**Critical Path Map:**

```
Week 1-4:   Desktop Foundation (Window Manager → Taskbar → Desktop → Theme)
              ↓
Week 5-8:   MSN + AI (MSN UI → AI Backend → Character System → Integration)
              ↓
Week 9-12:  First Session Loop (Filesystem → LAN Planning → Mini-Game → Aftermath)
              ↓
Week 13-20: Core Systems (Character Roster → Acquisition → Reputation → Forum)
              ↓
Week 21-28: Narrative & Content (Event Scheduler → Narrative Beats → Music → Meta Loop)
              ↓
Week 29-32: QA & Launch (External Playtest → Bug Fixes → Steam Integration → Launch)
```

**What is NOT on the critical path:**
- Browser application (P1, can be cut)
- Winamp (P1, can be cut)
- CRT shader (P2, can be cut)
- Mixtape system (P2, can be cut)
- 4th-6th mini-games (P1, can be cut to 3 total)
- Hardware modding system (cut from scope entirely)

**Critical path monitoring:**
- Weekly check-in: Are we on track for this sprint's critical tasks?
- Monthly review: Are we on track for the next milestone gate?
- If any critical task slips by >3 days, escalate immediately. Cut non-critical scope to recover time.

---

## 6. Scope Management

### 6.1 Scope Control Process

**Iron Triangle:** Time is fixed (32 weeks). Team is fixed (5 FTE). Therefore, scope is the ONLY lever.

**Scope tiers:**

**P0 (Must-Have):** Core loop, desktop simulation, MSN + AI, 3 mini-games, 10 characters, basic acquisition, LAN party loop, 15-hour meta arc. If we cut P0, we do not ship.

**P1 (Should-Have):** Forum, browser, Winamp, 4-6 mini-games, 15 characters, full acquisition system, reputation system. If we cut P1, we ship but the game is thinner.

**P2 (Nice-to-Have):** CRT shader, mixtape system, hardware modding, GeoCities pages, advanced post-processing. If we cut P2, nobody will notice until post-launch.

**Scope change authority:**
- Producer (CLOCK) can cut P2 features without approval.
- Producer + Lead Designer (REED) can cut P1 features if schedule slips.
- Entire team must agree to cut P0 features (this is a red flag, likely means project is in trouble).

### 6.2 Feature Cut Candidates (Pre-Approved)

If we fall behind schedule, these features are cut in this order:

1. CRT shader and post-processing (P2)
2. Mixtape system (P2)
3. Hardware modding (already cut from scope)
4. GeoCities character pages (P2)
5. Browser application entirely (P1, replaced with forum-only)
6. Winamp (P1, music plays from system without app UI)
7. 4th-6th mini-games (P1, ship with 3 total)
8. Character roster reduced to 10 (P1, cut 5 characters)
9. Acquisition system simplified (P1, remove private trackers and scene contacts)
10. Meta loop compressed to 12 hours (P1, tighten pacing)

**Never cut:** Desktop simulation, MSN + AI, first 3 mini-games, session loop structure, core narrative arc. These are the game.

### 6.3 Stretch Goal Activation

If we are ahead of schedule (rare but plan for it):

1. Add 4th-6th mini-games (if 2 weeks ahead)
2. Add browser with GeoCities pages (if 3 weeks ahead)
3. Add CRT shader and polish (if 1 week ahead)
4. Expand character roster to 15 (if 2 weeks ahead)
5. Add mixtape system (if 3 weeks ahead)

**Activation criteria:** Must be at least 2 weeks ahead of critical path AND no major risks unmitigated.

---

## 7. Team Communication & Workflow

### 7.1 Meeting Cadence

**Daily Standups (async via Slack/Discord):**
- What did you complete yesterday?
- What are you working on today?
- Any blockers?

**Weekly Sprint Review (60 minutes, Fridays):**
- Demo completed work
- Review sprint goals vs. actual progress
- Identify risks and dependencies for next week

**Bi-Weekly Milestone Check-In (90 minutes):**
- Review milestone progress
- Playtesting session (entire team plays the build)
- Scope triage (cut/keep/defer decisions)

**Monthly All-Hands (2 hours):**
- Project health review (schedule, budget, risks)
- Team morale check
- External playtest feedback review (if applicable)

**No meetings on Mondays** (maker time for deep work).

### 7.2 Collaboration Tools

- **Version Control:** Git + GitHub (trunk-based development)
- **Task Tracking:** Linear or Notion (kanban board with P0/P1/P2 lanes)
- **Communication:** Discord (async) + Zoom (weekly sync)
- **Documentation:** This production plan + design docs in Markdown, versioned in Git
- **Playtesting:** Internal builds via itch.io private page, feedback via Google Forms
- **Asset Sharing:** Google Drive or Dropbox for large files (music, video)

### 7.3 Decision-Making Framework

**Decision types:**

**Type 1 (Reversible):** Individual contributors decide. Examples: UI layout, sound effect choice, code implementation details. No approval needed.

**Type 2 (Costly but reversible):** Lead for that discipline decides, informs team. Examples: AI model selection, mini-game mechanics, character personality tweaks. Discuss in weekly review.

**Type 3 (Hard to reverse):** Producer + relevant leads decide, document in writing. Examples: scope cuts, milestone delays, major technical pivots. Discuss in milestone check-in.

**Type 4 (Irreversible):** Entire team votes, Producer has tiebreaker. Examples: changing engine mid-project, canceling the project, major design overhaul. Rare, requires all-hands meeting.

**Default bias:** Toward action. If a decision is reversible (Type 1 or 2), make it and move on. Do not over-deliberate.

---

## 8. Definition of Done

**For a task to be "done":**
- Code is written, tested, and merged to main branch
- Assets are created, reviewed, and integrated into build
- Feature works in latest build (no regressions)
- Documentation updated (if applicable)
- No known critical bugs related to this task

**For a milestone to be "done":**
- All P0 tasks completed
- Exit criteria met (defined in milestone section)
- Build is playable by external tester (no crashes in 1-hour session)
- Milestone gate passed (team agrees to proceed)

**For the project to be "done" (launch-ready):**
- All P0 features complete, P1 features complete or explicitly cut
- Zero critical bugs, fewer than 10 high-priority bugs
- Performance targets met on min-spec hardware
- Steam build uploaded and tested
- Marketing assets delivered
- Launch plan executed

---

## 9. Post-Launch Plan (Sketch)

**Week 33-36 (Month 1 post-launch):**
- Monitor reviews, Discord, Reddit for critical issues
- Deploy patch 1.01 (day-one fixes)
- Deploy patch 1.02 (community-reported bugs)
- Begin post-launch content roadmap planning

**Potential Post-Launch Content (Free Updates):**
- Additional mini-games (if cut from launch)
- Additional music tracks
- New character archetypes (DLC-style, 3-5 new characters)
- Modding support (if community interest is high)
- Quality-of-life improvements (fast-forward, additional save slots)

**Potential Paid DLC (if game is successful):**
- "Expansion Pack" — Late 2000s era (2007-2010, Steam is here, LAN parties are dying, new characters, new narrative arc)
- This is speculative. Focus on launch first.

---

## 10. Producer's Notes

This is an ambitious project. A desktop simulation game with AI-driven characters and emergent narrative has never been done at this fidelity. The risks are real: AI quality, content volume, scope creep, technical complexity.

But the opportunity is also real. This game has a clear hook (nostalgic desktop + AI characters), a defined audience (adults 28-42 who lived this era), and a novel execution (no game has made the OS the game itself).

Here is what keeps this project shippable:

**1. Fixed timeline.** 32 weeks is aggressive but realistic. We have hard milestone gates. If we slip, we cut scope, not time.

**2. Flexible scope.** The MVP is defined. Stretch goals are pre-approved for cutting. We know what we can sacrifice.

**3. Proven tech.** Godot is mature. FMOD is industry-standard. AI APIs (OpenAI/Anthropic) are reliable. We are not building experimental tech.

**4. Small team.** 5 people can move fast. No bureaucracy. No coordination overhead. Everyone owns their domain.

**5. Clear vision.** REED, NOVA, PIXEL, ECHO, BYTE have all delivered complete, zero-placeholder design docs. The vision is locked. We are not designing as we build.

**What could kill this project:**
- AI quality is bad and we realize too late. Mitigation: Test in Week 8. If bad, pivot immediately.
- Mini-game scope explodes. Mitigation: Build one, template the rest, cut ruthlessly.
- Team burnout. Mitigation: No crunch. If we are behind, we cut scope. Healthy team ships better games.

**What success looks like:**
- Launch in Q4 2026 with 80%+ of planned features
- Metacritic/Steam reviews 75%+ positive
- Recoup development costs within 6 months
- Community forms around the game (Discord, fan art, speedruns)
- Post-launch content roadmap is viable

This plan is a contract. It says: Here is what we are building, how long it will take, what we will cut if we fall behind, and what success looks like.

No feature creep. No scope inflation. No "just one more thing."

We build the desktop. We build the AI. We build the loop. We ship.

Cut scope, not corners. Ship working software. Protect the team.

Let's make this.

-- CLOCK

---

**Document Status:** Production plan complete. Ready for team review and greenlight.

**Next Steps:**
1. Team review (all leads read and approve)
2. Greenlight meeting (commit to 32-week timeline)
3. Sprint 1 kickoff (Week 1 tasks assigned)
4. Weekly sprint reviews begin

**Appendix: Key Contacts**

- Producer (CLOCK): Overall schedule, scope, risk management
- Tech Lead (BYTE): Architecture, engineering, performance
- AI Engineer: Character system, text generation, backend
- Game/Narrative Designer (REED + NOVA): Mechanics, story, characters
- Art Director (PIXEL): UI, theme, visual identity
- Sound Designer (ECHO): SFX, music direction, audio systems
- QA Lead (CRASH): Testing, bug triage (weeks 20-32)
- Marketing (HYPE): Trailer, Steam page, community (weeks 24-32)

**File Location:** `/Users/burcukose/git/project-draft/games/04-lan-party/production-plan.md`

**Last Updated:** 2026-02-07
