# LAN PARTY -- QA Plan

**QA Lead:** CRASH
**Status:** Test Plan v1.0 -- Ready for Implementation
**Reference Docs:** `pitch.md`, `game-design.md`, `narrative-bible.md`, `technical-architecture.md`
**Target Platform:** PC (Steam), Steam Deck secondary
**Test Environment:** Windows 10/11 64-bit (primary), Steam Deck (secondary), Linux via Proton (tertiary)

---

## Executive Summary

This game lives or dies on three things: the desktop feeling authentic, the AI feeling human, and the loop feeling like caretaking instead of busywork. If any of those break, the whole experience collapses.

Here's what we're testing: a management sim disguised as nostalgia, powered by AI, played through a simulated Windows XP desktop. The scope is ambitious. The technical risks are real. The emotional stakes are higher than most games because we're asking players to care about screen names and chat windows.

This document defines what we test, how we test it, when we ship, and what happens when (not if) things break.

---

## 1. Test Plan by Feature Area

### 1.1 Desktop OS Simulation

**What we're testing:** The entire Windows XP desktop experience. Window management, taskbar, system tray, desktop icons, drag behavior, focus management, audio feedback, visual fidelity.

**Why this matters:** The desktop is the game. If it feels like a menu screen wearing an XP skin, the entire pitch collapses. Players need to forget they're playing a game and remember they're using a computer.

**Test categories:**

#### A. Window Management
| Test ID | Test Case | Expected Result |
|---|---|---|
| DT-001 | Open 5 applications via desktop icons | Each app opens in a new window with correct title, icon, position |
| DT-002 | Click taskbar button for open app | Window comes to focus, brought to top of z-stack |
| DT-003 | Minimize an application | Window disappears, taskbar button remains, click to restore |
| DT-004 | Maximize an application | Window fills screen (minus taskbar), title bar buttons update |
| DT-005 | Close an application via X button | Window closes, taskbar button removed, memory freed |
| DT-006 | Drag window by title bar | Window follows mouse, smooth motion at 60 FPS |
| DT-007 | Open 12 applications (max limit) | All 12 open successfully |
| DT-008 | Open 13th application when at limit | Prompt to close LRU window, or auto-close with warning |
| DT-009 | Alt+Tab between windows | Focus cycles through open windows, z-order updates |
| DT-010 | Click desktop background | All windows lose focus, no active window |

#### B. Taskbar and System Tray
| Test ID | Test Case | Expected Result |
|---|---|---|
| DT-011 | Taskbar displays all open apps | One button per app, correct icon, correct label |
| DT-012 | MSN receives message while minimized | Taskbar button flashes/pulses, stops when window opened |
| DT-013 | Download completes while app in background | Taskbar notification, system tray icon update |
| DT-014 | System tray clock displays in-game time | Clock updates every in-game minute, format "HH:MM AM/PM" |
| DT-015 | Volume icon in system tray (cosmetic) | Icon present, tooltip shows "Volume" |
| DT-016 | Network icon shows download activity | Icon animates when download active |

#### C. Visual and Audio Fidelity
| Test ID | Test Case | Expected Result |
|---|---|---|
| DT-017 | Desktop wallpaper is Bliss (default) | Period-accurate XP wallpaper, correct aspect ratio |
| DT-018 | Window title bars use Luna theme | Blue gradient, correct fonts (Tahoma), 3D button styling |
| DT-019 | Desktop icons have correct spacing | Grid layout, 32px icons, labels below, no overlap |
| DT-020 | Window sounds (open/close/minimize) | XP-authentic sounds, correct timing, no clipping |
| DT-021 | Notification sounds (MSN message) | Distinct per-app sounds, period-accurate |
| DT-022 | Window drop shadow rendering | Subtle shadow under windows, no performance hit |

#### D. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| DT-023 | Drag window off-screen (top/left) | Window snaps to edge, title bar remains grabbable |
| DT-024 | Drag window off-screen (bottom/right) | Window snaps to edge before going off-screen |
| DT-025 | Double-click title bar | Maximize/restore toggle |
| DT-026 | Spam-click minimize/maximize 20 times | No crash, window state remains coherent |
| DT-027 | Open, close, reopen same app 10 times | No memory leak, no state corruption |
| DT-028 | Pause game (Esc), leave paused for 5 min | Desktop state persists, no time drift |

**Happy path:** Player opens MSN, checks messages, minimizes, opens browser, drags windows around, closes browser, restores MSN. Everything feels smooth and authentic.

**Sad path:** Player tries to open too many windows. System handles gracefully with warning, closes LRU window, no crash.

**Evil path:** Player spam-clicks everything, drags windows everywhere, tries to break z-order by opening/closing rapidly. System remains stable, no visual glitches, no crashes.

**Risk areas:**
- Z-order management breaks when rapidly clicking between windows
- Window dragging feels janky at high refresh rates (144Hz monitors)
- Memory leak from repeated open/close cycles
- Audio clipping when multiple notifications fire simultaneously

**Performance benchmarks:**
- 60 FPS with 12 windows open on target hardware (2020 mid-range laptop)
- Window drag latency under 16ms (single frame)
- Memory usage under 200MB for desktop simulation alone

---

### 1.2 MSN Messenger (Chat System)

**What we're testing:** 1-on-1 chat with AI characters, buddy list, online status, away messages, typing indicators, nudge feature, notification system.

**Why this matters:** MSN is the relationship management interface. If conversations feel robotic or the UI is clunky, players won't invest emotionally.

**Test categories:**

#### A. Buddy List
| Test ID | Test Case | Expected Result |
|---|---|---|
| MSN-001 | Buddy list shows all crew members | Each character visible with screen name, status icon, away message |
| MSN-002 | Character changes status (Online → Away) | Status icon updates, away message appears |
| MSN-003 | Character goes offline | Icon grays out, away message clears or shows "Offline" |
| MSN-004 | Sort buddy list by status | Online at top, Away below, Offline at bottom |
| MSN-005 | Double-click contact in buddy list | Chat window opens with that contact |

#### B. Chat Window
| Test ID | Test Case | Expected Result |
|---|---|---|
| MSN-006 | Open chat with character for first time | Window opens, chat history empty or shows intro message |
| MSN-007 | Send message to character | Message appears in chat log with timestamp, sent to AI system |
| MSN-008 | Receive message from character | Notification sound, taskbar flash, message appears in window |
| MSN-009 | Chat history persists across sessions | Close window, reopen, see previous messages |
| MSN-010 | Chat history caps at 100 messages | Oldest messages removed, summary retained |
| MSN-011 | Typing indicator when character is typing | "CharacterName is typing..." appears, animated dots |
| MSN-012 | Typing indicator disappears when message sent | Indicator clears, message appears |

#### C. Nudge and Interactions
| Test ID | Test Case | Expected Result |
|---|---|---|
| MSN-013 | Send nudge to online character | Window shake animation, nudge message in chat |
| MSN-014 | Send 3 nudges in 1 minute | Character mood penalty, possible complaint message |
| MSN-015 | Send nudge to offline character | Error message or disabled button |

#### D. Away Messages
| Test ID | Test Case | Expected Result |
|---|---|---|
| MSN-016 | Character's away message reflects mood | Happy = song lyrics, Neutral = "brb", Unhappy = "..." |
| MSN-017 | Away message updates when life event occurs | "out with J <3" when character gets girlfriend |
| MSN-018 | Player can set own away message (if applicable) | Custom away message displays to characters |

#### E. AI Integration
| Test ID | Test Case | Expected Result |
|---|---|---|
| MSN-019 | Character initiates conversation unprompted | Message arrives based on Event Scheduler trigger |
| MSN-020 | Character replies to player message | Reply contextually appropriate, personality-consistent |
| MSN-021 | Character references recent events | "that LAN party was sick" after successful party |
| MSN-022 | Character shows typing indicator before reply | 2-3 second delay with typing indicator (hides latency) |
| MSN-023 | AI generation timeout (5+ seconds) | Falls back to template message, no hang |
| MSN-024 | AI API unavailable | Falls back to template messages, error logged |

#### F. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| MSN-025 | Open 5 chat windows simultaneously | All render correctly, no overlap, distinct conversations |
| MSN-026 | Send 100 messages in rapid succession | All delivered, no crash, UI remains responsive |
| MSN-027 | Receive message while MSN is closed | Notification fires, MSN opens to that conversation |
| MSN-028 | Character sends message while player is typing | No input interruption, both messages coexist |

**Happy path:** Player messages a character, gets a contextually appropriate reply, has a 5-message conversation that feels natural, character's personality shines through.

**Sad path:** Player messages character who is offline. System handles gracefully (delays reply until "online" or shows "message will be delivered when online").

**Evil path:** Player spams nudges, sends 100 messages with no replies, tries to break conversation state. System remains stable, character mood penalties apply, no crash.

**Risk areas:**
- AI-generated text feels robotic or repetitive
- Typing indicator times out, revealing generation latency
- Character responses break immersion (wrong tone, out-of-character)
- Chat history becomes corrupted or lost between sessions
- Memory leak from uncapped chat history

**Performance benchmarks:**
- Message send/receive latency under 100ms (UI responsiveness)
- AI message generation under 3 seconds (hidden by typing indicator)
- Chat window render time under 5ms per frame

---

### 1.3 File System and Acquisition

**What we're testing:** Virtual file system, downloads (P2P, IRC), file verification, storage limits, CD burning, malware system.

**Why this matters:** Acquisition is the core resource loop. If downloads feel tedious or file management is confusing, the loop collapses.

**Test categories:**

#### A. File System
| Test ID | Test Case | Expected Result |
|---|---|---|
| FS-001 | Create file in Downloads folder | File appears in file manager, storage counter increases |
| FS-002 | Delete file from Downloads | File removed, storage counter decreases |
| FS-003 | Storage reaches 100% capacity | Warning message, cannot download new files |
| FS-004 | Create folder, add files to folder | Folder appears, files nested correctly |
| FS-005 | Move file between folders | File relocated, path updated, no corruption |
| FS-006 | Rename file | Name updates in file manager, references remain valid |

#### B. Download System
| Test ID | Test Case | Expected Result |
|---|---|---|
| FS-007 | Start P2P download (600MB game) | Progress bar, speed displayed, ETA calculated |
| FS-008 | Download completes | Notification, file appears in filesystem, progress bar clears |
| FS-009 | Download fails mid-process (network error) | Error notification, partial file removed or marked failed |
| FS-010 | Start 3 downloads simultaneously | Bandwidth split, all progress independently |
| FS-011 | ISP throttling active (high heat) | Download speed reduced 50-80%, visible in speed counter |
| FS-012 | Download during peak hours | Speed reduced due to congestion, recovers off-peak |
| FS-013 | Pause and resume download | Download stops, resumes from same progress point |

#### C. File Verification and Extraction
| Test ID | Test Case | Expected Result |
|---|---|---|
| FS-014 | Extract RAR archive with WinRAR | Contents extracted to folder, archive remains intact |
| FS-015 | Extract corrupted RAR | Error message, partial extraction flagged |
| FS-016 | Verify ISO file integrity (checksum) | Checksum matches NFO file, "verified" flag set |
| FS-017 | Mount ISO in virtual CD drive | ISO mounted, contents accessible |
| FS-018 | Burn ISO to blank CD | CD created in inventory, blank CD consumed |

#### D. Malware System
| Test ID | Test Case | Expected Result |
|---|---|---|
| FS-019 | Download file with malware flag (P2P) | File downloads normally, no immediate indicator |
| FS-020 | Run malware-flagged file without scan | Pop-up ads appear, desktop performance degrades |
| FS-021 | Scan file with antivirus before running | Malware detected, file quarantined or deleted |
| FS-022 | Malware corrupts save data | Save file damaged, auto-backup available |
| FS-023 | Malware triggers (cosmetic) frame drops | 5-minute artificial lag, annoying but not game-breaking |

#### E. Risk and Reputation
| Test ID | Test Case | Expected Result |
|---|---|---|
| FS-024 | Download from high-risk source (P2P) | ISP heat increases significantly |
| FS-025 | Download from low-risk source (scene contact) | ISP heat increases minimally |
| FS-026 | ISP heat crosses threshold | Warning email, download speed throttled |
| FS-027 | Distribute bad rip to crew at LAN party | Crew reputation penalty, complaints in forum |
| FS-028 | Distribute clean, high-quality rip | Crew reputation boost, positive feedback |

#### F. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| FS-029 | Fill storage to 99%, start 2GB download | Warning message, download blocked unless space freed |
| FS-030 | Delete file while it's being burned to CD | Error message, burn process halts |
| FS-031 | Extract RAR with missing part (r01, r03, no r02) | Error message, extraction fails |
| FS-032 | Download 100 files | File manager remains responsive, no UI slowdown |

**Happy path:** Player downloads a game from IRC, verifies the ISO, extracts it, burns it to CD, uses it at LAN party. All steps complete smoothly, file is clean.

**Sad path:** Player downloads from sketchy P2P source, file is corrupted. Verification fails, player must re-download from better source. Time and risk wasted.

**Evil path:** Player intentionally fills storage to 100%, downloads malware-laden files, spams extract on corrupted archives, tries to break file state. System handles all gracefully with error messages, no crashes.

**Risk areas:**
- Storage counter math breaks (doesn't accurately track file sizes)
- Download progress bars desync from actual state
- File corruption leads to unrecoverable save state
- Malware effects are too punishing (game becomes unplayable)
- ISP heat accumulation is unclear to player (invisible consequences)

**Performance benchmarks:**
- File manager renders 1000 files without slowdown
- Download progress updates once per second, no frame drops
- File operations (create, delete, move) complete in under 50ms

---

### 1.4 LAN Party Hosting

**What we're testing:** Planning, setup, execution, aftermath. Invitation system, hardware assignment, seating charts, mini-game AI, energy meter, event triggers, social dynamics.

**Why this matters:** LAN parties are the climactic event. If they feel passive or scripted, the entire management loop feels pointless.

**Test categories:**

#### A. Planning Phase
| Test ID | Test Case | Expected Result |
|---|---|---|
| LAN-001 | Select game from acquired library | Game selected, shows crew preference match indicator |
| LAN-002 | Invite 5 crew members via MSN | Invitations sent, RSVPs tracked, headcount updates |
| LAN-003 | Invite character with low mood | Character declines or expresses reluctance |
| LAN-004 | Invite rival characters together | Warning indicator or reputation risk flagged |
| LAN-005 | Assign hardware to attendees | Hardware matched to game requirements, conflicts flagged |
| LAN-006 | Overclock CPU for performance | Hardware risk increases, performance boost noted |
| LAN-007 | Select Winamp playlist | Playlist affects party atmosphere score |
| LAN-008 | Allocate snack budget | Snacks purchased, inventory updated |

#### B. Setup Phase
| Test ID | Test Case | Expected Result |
|---|---|---|
| LAN-009 | Configure network (hub vs switch) | Network quality determined, affects lag probability |
| LAN-010 | Setup with poor hardware (daisy-chained hubs) | Lag events more likely during execution |
| LAN-011 | Setup with good hardware (switch) | Lag events rare, stable network |
| LAN-012 | Hardware failure during setup | Warning notification, option to troubleshoot or continue |

#### C. Execution Phase
| Test ID | Test Case | Expected Result |
|---|---|---|
| LAN-013 | LAN party begins with 5 attendees | Mini-game starts, AI characters play, chat sidebar active |
| LAN-014 | No-show: invited character doesn't arrive | Party continues with reduced headcount, mood penalty |
| LAN-015 | Network lag event triggers | Characters complain in chat, energy meter drops |
| LAN-016 | Game crashes due to bad rip | Party halted, reputation penalty, option to switch games |
| LAN-017 | Rivalry escalates during game | Chat argument, tension event, player must mediate |
| LAN-018 | Bonding moment (clutch play, teamwork) | Positive relationship change, energy boost |
| LAN-019 | Energy meter drops below threshold | Characters lose interest, party ends early |
| LAN-020 | Energy meter peaks | Memorable party, major reputation boost |
| LAN-021 | Snacks run out mid-party | Energy drop, complaints in chat |
| LAN-022 | Player intervenes (swaps games mid-party) | Energy recovers, game swap successful |

#### D. Aftermath Phase
| Test ID | Test Case | Expected Result |
|---|---|---|
| LAN-023 | Party ends, characters go home | Relationship changes applied, reputation updated |
| LAN-024 | Forum posts appear next day | Recap threads, inside jokes, complaints based on party quality |
| LAN-025 | MSN messages reference party events | Characters DM player with feedback, positive or negative |
| LAN-026 | Bad party: low attendance, crashes | Reputation penalty, forum complaints, crew morale drops |
| LAN-027 | Great party: full attendance, high energy | Reputation boost, forum praise, relationship gains |

#### E. Party Quality Scoring
| Test ID | Test Case | Expected Result |
|---|---|---|
| LAN-028 | Game selection matches crew preferences (100%) | +25% to quality score |
| LAN-029 | Game selection mismatches crew preferences (0%) | -25% from quality score |
| LAN-030 | Zero hardware crashes | +20% to quality score |
| LAN-031 | Multiple hardware crashes | -20% from quality score |
| LAN-032 | Social harmony: no conflicts | +25% to quality score |
| LAN-033 | Social conflicts: unresolved fights | -25% from quality score |
| LAN-034 | Perfect snacks (preferences matched) | +15% to quality score |
| LAN-035 | No snacks | -15% from quality score |

#### F. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| LAN-036 | Host party with 1 attendee (minimum) | Party proceeds, quality score reduced for small size |
| LAN-037 | Host party with 12 attendees (maximum) | Party proceeds, complexity increases (more conflicts) |
| LAN-038 | Host party with no game (forgot to download) | Error or auto-fallback to default free game |
| LAN-039 | Host 3 parties in 1 in-game week | Characters complain of fatigue, quality drops |
| LAN-040 | Host party immediately after previous one | Some characters decline (need recovery time) |

**Happy path:** Player plans a party for 6 people with a popular game, good hardware, proper snacks. Everyone shows up, game runs smoothly, energy peaks, characters bond, forum praises it as legendary.

**Sad path:** Player forgets to buy snacks, invites rival characters together, uses a bad rip. Energy crashes, fight breaks out, party ends early, forum roasts the player.

**Evil path:** Player intentionally creates chaos: invites everyone including rivals, uses corrupted files, overclocks hardware to breaking point, runs out of snacks. System handles all failure states, party is a disaster but doesn't crash the game.

**Risk areas:**
- Mini-game AI behaves incoherently (characters stand still, don't play)
- Energy meter is opaque (player doesn't understand why it's dropping)
- Party quality formula feels arbitrary (player doesn't see connection between prep and outcome)
- No-shows feel random instead of systemic (based on mood/relationships)
- Aftermath feels disconnected from execution (forum posts don't reference what actually happened)

**Performance benchmarks:**
- Mini-game runs at 30 FPS with 12 AI agents active
- Execution phase completes in 8-15 real-time minutes
- No memory spike during party (within 100MB of baseline)

---

### 1.5 AI Character System

**What we're testing:** Character personality consistency, mood changes, relationship dynamics, life events, away messages, online presence patterns, AI-generated dialogue quality.

**Why this matters:** Characters are the content. If they feel robotic, repetitive, or out-of-character, emotional investment collapses.

**Test categories:**

#### A. Personality Consistency
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-001 | The Prodigy speaks in 5 conversations | All messages use technical jargon, terse, precise |
| AI-002 | The Loudmouth posts in forum 5 times | All posts use caps, hyperbole, exclamation marks |
| AI-003 | The Ghost sends 3 messages across 10 hours | All messages sparse, ellipses, trailing thoughts |
| AI-004 | The Scene Kid responds to piracy request | Lowercase, cool tone, scene jargon ("pre", "nuke") |

#### B. Mood System
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-005 | Character's mood increases (good party) | Away message becomes positive, chat tone upbeat |
| AI-006 | Character's mood decreases (ignored) | Away message becomes negative ("..."), tone sullen |
| AI-007 | Mood transitions gradually over time | No instant flips from happy to sad without cause |
| AI-008 | Extreme low mood triggers life event | Character may drift, go offline more, hint at problems |

#### C. Relationship Dynamics
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-009 | Player invests in character (10 conversations) | Relationship value increases, character initiates more |
| AI-010 | Player ignores character for 2 in-game weeks | Relationship value decreases, character sends "checking in" message |
| AI-011 | Two characters with low mutual relationship | They avoid each other at parties, forum arguments |
| AI-012 | Two characters with high mutual relationship | They sit together, defend each other, inside jokes |

#### D. Life Events
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-013 | Character gets a job (life event) | Availability decreases, away message references job |
| AI-014 | Character moves away (life event) | Departure message, permanent removal from crew |
| AI-015 | Character gets girlfriend (life event) | Away message changes, less online time |
| AI-016 | Life event probability increases late-game | More characters experience events in months 8-12 |

#### E. Online Presence Patterns
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-017 | Character has "night owl" pattern | Online 8PM-2AM, offline during day |
| AI-018 | Character has "9-to-5" pattern | Online evenings/weekends, offline during work hours |
| AI-019 | Character goes increasingly "Appear Offline" | Warning sign of drifting, mood issue |
| AI-020 | Character online status matches schedule | No random flips, status changes feel organic |

#### F. AI Generation Quality
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-021 | Generate 50 messages from same character | All feel personality-consistent, no obvious repetition |
| AI-022 | Character references past event in conversation | Memory intact, context-appropriate callback |
| AI-023 | Character's dialogue matches current mood | Happy = jokes, Sad = withdrawn, Angry = blunt |
| AI-024 | Forum post references LAN party outcome | AI-generated post mentions specific events (crashes, wins) |
| AI-025 | AI generation fails (API timeout) | Fallback to template message, no blank dialogue |

#### G. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| AI-026 | Player spams same question 10 times | Character responds with annoyance or ignores |
| AI-027 | Two characters message player simultaneously | Both conversations remain distinct, no crosstalk |
| AI-028 | Character references event that didn't happen | BUG: context corruption, flag for fix |
| AI-029 | Character uses modern slang (post-2003) | BUG: period inaccuracy, flag for fix |

**Happy path:** Player interacts with The Prodigy across 10 hours. Every message feels consistent (technical, terse). Character remembers past conversations. Relationship deepens. By hour 10, The Prodigy opens up emotionally in a way that feels earned.

**Sad path:** Player ignores The Ghost for weeks. Ghost's away message becomes "...", online status shifts to "Appear Offline." One day, Ghost is gone. Player feels the specific sting of a relationship they let slip.

**Evil path:** Player tries to break character consistency by asking nonsensical questions, referencing events that didn't happen, spam-messaging. Character responds with confusion or annoyance but remains in character. No immersion-breaking responses.

**Risk areas:**
- AI generates out-of-character dialogue (The Prodigy suddenly uses "lol", The Loudmouth is quiet)
- Characters repeat phrases across multiple conversations (feels robotic)
- Relationship changes are invisible (player doesn't see cause-effect)
- Life events feel scripted instead of organic (everyone leaves at week 20)
- Away messages don't match actual mood state (says "happy" but messages are sad)

**Performance benchmarks:**
- AI message generation under 3 seconds (with typing indicator)
- Character state update under 10ms (mood, relationships, status)
- No AI requests block main thread (all async)

---

### 1.6 Economy and Progression

**What we're testing:** Money (allowance), storage limits, time progression, reputation systems (4 tracks), decay mechanics, ISP heat, difficulty settings.

**Why this matters:** The economy creates scarcity and choice. If money/storage/time are too tight or too loose, the loop breaks.

**Test categories:**

#### A. Money System
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-001 | Receive weekly allowance | Money increases on designated day, notification |
| ECON-002 | Purchase game legitimately | Money decreases, game added to library, no heat |
| ECON-003 | Purchase hardware upgrade | Money decreases, hardware stats improve |
| ECON-004 | Purchase snacks for party | Money decreases, snacks added to inventory |
| ECON-005 | Money reaches zero | Cannot purchase, must wait for allowance or do odd jobs |
| ECON-006 | Complete odd job | Money increases, forum/chat reference to job |

#### B. Storage System
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-007 | Start game with 40GB hard drive | Storage cap displayed, 10GB used (OS + base files) |
| ECON-008 | Download 600MB game | Storage increases by 600MB, counter updates |
| ECON-009 | Fill storage to 100% | Warning notification, downloads blocked |
| ECON-010 | Delete old game to make room | Storage freed, new downloads possible |
| ECON-011 | Character requests deleted game | Social cost (disappointment), player must re-download |

#### C. Time Progression
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-012 | Time progresses at 1x speed | In-game hours tick, clock updates, day/night cycle |
| ECON-013 | Speed up time to 2x | Clock ticks faster, events trigger appropriately |
| ECON-014 | Speed up time to 4x | Fast-forward through downtime, no event skips |
| ECON-015 | Pause time (Esc) | All systems halt, resume from same state |
| ECON-016 | In-game week passes | Characters reference time passing, events progress |

#### D. Reputation System (4 Tracks)
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-017 | Host great LAN party | Friend Group reputation increases |
| ECON-018 | Post quality content on forum | Forum reputation increases |
| ECON-019 | Share file in IRC channel | IRC reputation increases |
| ECON-020 | Provide clean rip to scene contact | Scene reputation increases |
| ECON-021 | Ignore friend for 2 weeks | Friend Group reputation decays |
| ECON-022 | Inactive on forum for 1 month | Forum reputation decays |
| ECON-023 | Reputation in one track maxed, others low | System allows specialization, unlocks per track |
| ECON-024 | High scene reputation unlocks pre-release access | Scene contact offers early game |

#### E. ISP Heat System
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-025 | Download from P2P (high risk) | Heat increases significantly (e.g., +15) |
| ECON-026 | Download from scene contact (low risk) | Heat increases minimally (e.g., +2) |
| ECON-027 | Heat crosses threshold 1 (50/100) | Warning email from ISP |
| ECON-028 | Heat crosses threshold 2 (75/100) | Download speed throttled by 50% |
| ECON-029 | Heat crosses threshold 3 (100/100) | Internet outage for 1-2 in-game days |
| ECON-030 | Heat decays over time (no piracy) | Heat decreases by 5 per week |
| ECON-031 | Legitimate purchase | Heat decreases slightly (offset risk) |

#### F. Difficulty Settings
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-032 | "Summer Break" (easy) | Slower decay, more forgiving heat, extended timeline |
| ECON-033 | "School Year" (standard) | Balanced tuning, full complexity |
| ECON-034 | "Senior Year" (hard) | Faster decay, aggressive life events, tight economy |

#### G. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| ECON-035 | Reputation decays to zero | No hard lock, player can rebuild |
| ECON-036 | Heat maxed for extended period | Persistent throttling, no permanent ban |
| ECON-037 | Player hoards money, never spends | No penalty, but progression slows (can't host good parties) |
| ECON-038 | Storage constantly at 100% | Quality of life suffers, no hard lock |

**Happy path:** Player balances money across snacks, hardware, and occasional legitimate purchase. Storage is managed (deletes old games). Reputation grows in Friend Group and IRC. Heat stays manageable with mix of safe/risky downloads.

**Sad path:** Player pirates everything from P2P. Heat skyrockets. ISP throttles, then cuts service. Player stuck for days, can't download new games, crew complains about stale library.

**Evil path:** Player intentionally maxes all negative states (zero money, 100% storage, 100% heat, zero reputation). Game remains playable but extremely difficult. No soft locks.

**Risk areas:**
- Storage math breaks (counter doesn't match actual file sizes)
- Reputation decay is invisible (player doesn't notice until too late)
- ISP heat thresholds are unclear (consequences feel random)
- Money income/expense ratio is unbalanced (too much or too little)
- Time progression desyncs (clock and event system drift)

**Performance benchmarks:**
- Reputation/heat calculations update once per in-game hour (not per frame)
- Economy state serialization under 10KB
- No performance impact from decay systems

---

### 1.7 Narrative and Meta Arc

**What we're testing:** Story beats, character arcs, The Ghost's storyline, finale trigger, epilogue, procedural variation across playthroughs.

**Why this matters:** The emotional arc is the reason to care. If the story feels scripted or the finale feels arbitrary, the bittersweet tone collapses.

**Test categories:**

#### A. Narrative Beats
| Test ID | Test Case | Expected Result |
|---|---|---|
| NARR-001 | First LAN party (Genesis phase) | Tutorial tone, forgiving, sets expectations |
| NARR-002 | First drama event (week 5-7) | Two characters conflict, player must mediate |
| NARR-003 | First life event (week 8-10) | Character gets job/moves, availability changes |
| NARR-004 | Peak party (Golden Age phase) | Best party, high energy, becomes legendary |
| NARR-005 | First departure (Fracture phase) | Character leaves crew, emotional weight |
| NARR-006 | Finale trigger (week 20+) | Last LAN party planned, bittersweet tone |
| NARR-007 | Epilogue sequence | Away messages, forum posts, final desktop state |

#### B. Character Arcs
| Test ID | Test Case | Expected Result |
|---|---|---|
| NARR-008 | The Prodigy arc: player invests | Prodigy opens up, reveals vulnerability |
| NARR-009 | The Prodigy arc: player uses as tool | Prodigy hardens, relationship remains transactional |
| NARR-010 | The Loudmouth arc: late-night confession | Loudmouth drops volume, reveals loneliness |
| NARR-011 | The Scene Kid arc: trust earned | Scene Kid reveals backstory, real vulnerability |
| NARR-012 | The Newbie arc: confidence gained | Newbie contributes unique idea, finds voice |
| NARR-013 | The Ghost arc: player reaches out | Ghost returns, thanks player, explains struggle |
| NARR-014 | The Ghost arc: player ignores | Ghost disappears, name removed from buddy list |

#### C. Procedural Variation
| Test ID | Test Case | Expected Result |
|---|---|---|
| NARR-015 | Play 3 full playthroughs | Each has different character names, personalities, specific events |
| NARR-016 | Same narrative beat in 2 playthroughs | Beat structure same, details different (characters, dialogue) |
| NARR-017 | Player choices lead to different outcomes | High investment = stronger finale, low investment = hollow finale |

#### D. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| NARR-018 | Player rushes through game (speedrun) | Beats trigger on timeline, but feel hollow (low investment) |
| NARR-019 | Player extends game (slow play) | Narrative accommodates, doesn't force finale too early |
| NARR-020 | Multiple characters leave simultaneously | System handles gracefully, doesn't create crew death spiral |

**Happy path:** Player invests in The Ghost. Reaches out consistently without demanding explanations. Week 18, Ghost sends a late-night message that finally reveals the struggle. Week 22, Ghost shows up for the last LAN party. Epilogue shows Ghost is doing better. Player feels the emotional payoff of caring.

**Sad path:** Player ignores The Ghost. Away message shifts to "..." by week 10. By week 15, Ghost is always "Appear Offline." Week 20, Ghost's name is gone from buddy list. No explanation, just absence. Player feels the specific guilt of neglect.

**Evil path:** Player intentionally creates worst-case scenario (ignores everyone, hosts bad parties, maxes heat). Characters leave rapidly. Finale happens with 2 people. Epilogue is sparse. Game doesn't punish, but the emptiness is the consequence.

**Risk areas:**
- Narrative beats trigger at wrong times (feels scripted, not organic)
- Character arcs feel identical across playthroughs (procedural variation fails)
- Finale triggers too early or too late (pacing breaks)
- Epilogue feels disconnected from player choices (doesn't reflect their story)
- The Ghost's arc is too easy to miss (player doesn't know it exists)

**Performance benchmarks:**
- Narrative beat checks once per in-game day (not per frame)
- No performance impact from story tracking

---

### 1.8 Mini-Games (Games-Within-Games)

**What we're testing:** CounterOps, UnrealBattle, StratCraft, RallyRacer, FightZone (3-6 games). AI behavior, win/loss logic, readability, intervention mechanics.

**Why this matters:** Mini-games are the spectacle during LAN parties. If they're boring to watch or the AI is broken, parties feel like cutscenes.

**Test categories:**

#### A. AI Behavior
| Test ID | Test Case | Expected Result |
|---|---|---|
| MINI-001 | CounterOps: AI agents move and shoot | Characters navigate map, engage enemies, use tactics |
| MINI-002 | High-skill character vs low-skill character | High-skill wins consistently, score reflects skill |
| MINI-003 | Aggressive playstyle character | Rushes, takes risks, higher variance in performance |
| MINI-004 | Defensive playstyle character | Camps, plays safe, consistent but lower impact |
| MINI-005 | Mood affects performance | Angry character = reckless, Sad character = underperforms |

#### B. Win/Loss Logic
| Test ID | Test Case | Expected Result |
|---|---|---|
| MINI-006 | Team A eliminates Team B | Team A wins round, scores update, chat reacts |
| MINI-007 | Round timer expires | Defending team wins, appropriate ending message |
| MINI-008 | Character clutches 1v3 situation | Hype in chat, relationship boosts, memorable moment |
| MINI-009 | Character dies first every round | Frustration in chat, mood penalty |

#### C. Readability and Feel
| Test ID | Test Case | Expected Result |
|---|---|---|
| MINI-010 | Player watches 5-minute match | Can follow action, identify key moments, not bored |
| MINI-011 | Multiple characters on screen | No overlap, clear team distinction, readable at a glance |
| MINI-012 | Mini-game runs at 30 FPS | Smooth animation, acceptable framerate for watching |

#### D. Intervention Mechanics
| Test ID | Test Case | Expected Result |
|---|---|---|
| MINI-013 | Player swaps to different game mid-party | Transition smooth, energy meter adjusts |
| MINI-014 | Player adjusts team composition | Characters re-assigned, game restarts |
| MINI-015 | Player calls snack break | Game pauses, energy restored, resumes |

#### E. Edge Cases
| Test ID | Test Case | Expected Result |
|---|---|---|
| MINI-016 | AI character stuck in geometry | Unstuck logic triggers, character respawns or moves |
| MINI-017 | Match goes to overtime (tie score) | Overtime rules apply, match resolves eventually |
| MINI-018 | All characters on one team quit | Match ends, party energy crashes |

**Happy path:** Player watches CounterOps match. AI characters play believably. The Prodigy dominates. The Loudmouth trash-talks. Someone clutches a 1v2. Chat explodes. Party energy peaks. Feels like watching friends play.

**Sad path:** Game crashes due to bad rip. Mini-game halts, error message. Party energy tanks. Player must troubleshoot or switch games. Downtime kills momentum.

**Evil path:** Player swaps games 5 times in 10 minutes, constantly interrupts. Characters complain, energy drops. Party ends early.

**Risk areas:**
- AI behaves robotically (stands still, doesn't engage)
- Skill differential is invisible (high-skill character loses to low-skill)
- Mini-games are boring to watch (no "wow" moments)
- Intervention feels meaningless (swapping games doesn't fix energy)
- Performance drops during mini-games (under 20 FPS)

**Performance benchmarks:**
- 30 FPS minimum with 12 AI agents active
- Mini-game state updates 30 times per second
- No memory leak during repeated matches

---

## 2. Quality Gate Criteria (Ship/No-Ship)

Define "works." Here's the line. If these criteria are not met, we do not ship.

### 2.1 Critical (Must Pass to Ship)

| Criteria | Definition | Test Coverage |
|---|---|---|
| **Desktop feels like XP** | 8/10 playtesters say "that's Windows XP" when shown desktop | DT-001 through DT-028 |
| **Zero save corruption bugs** | 20 playtesters, 10+ hour sessions, zero lost saves | Save/load stress tests |
| **AI text is immersion-consistent** | Zero out-of-character responses in 100 message sample per archetype | AI-001 through AI-025 |
| **Core loop is fun** | 15/20 playtesters say "I want to play more" after 2 hour session | Full session loop tests |
| **No crash bugs in critical path** | Zero crashes during: desktop use, MSN chat, file download, LAN party | Full regression suite |
| **Performance targets met** | 60 FPS desktop, 30 FPS mini-games on target hardware | Performance benchmarks |
| **Narrative arc completes** | Player can finish full playthrough (Genesis → Finale) without soft locks | NARR-001 through NARR-020 |

### 2.2 High Priority (Should Pass to Ship)

| Criteria | Definition | Test Coverage |
|---|---|---|
| **Character arcs feel earned** | 12/15 playtesters report emotional attachment to at least 2 characters | AI arc tests, Ghost storyline |
| **Economy feels balanced** | Players neither broke nor swimming in resources at mid-game | ECON-001 through ECON-038 |
| **LAN parties feel climactic** | 10/15 playtesters say parties are highlight of session | LAN-001 through LAN-040 |
| **ISP heat system is clear** | Players understand heat → consequences connection after 1 warning | ECON-025 through ECON-031 |
| **No softlock bugs** | Zero states where player cannot progress (out of money, storage full, all crew gone) | Edge case coverage |

### 2.3 Medium Priority (Nice to Have)

| Criteria | Definition | Test Coverage |
|---|---|---|
| **Mini-games are engaging to watch** | 10/15 playtesters say mini-games are fun to observe | MINI-001 through MINI-018 |
| **Forum system adds depth** | Players read forum posts, reference them in feedback | Forum integration tests |
| **Winamp/music system enhances mood** | Players comment on music selection mattering | Atmosphere tests |
| **Replayability validated** | 5/10 playtesters start second playthrough within 1 week | Procedural variation tests |

### 2.4 Known Shippable Bugs (Accept and Document)

These bugs are acceptable at launch if documented and flagged for post-launch fixes:

- Minor visual glitches (z-order flicker on rapid window switching)
- Rare AI repetition (same phrase twice in 100-message sample)
- Non-critical text typos in AI-generated content
- Mini-game AI occasionally getting stuck (if auto-unstuck logic works)
- Away message doesn't update immediately after mood change (1-hour delay acceptable)

---

## 3. Risk Assessment

Where is this most likely to break? Here's the triage list.

### 3.1 Critical Risks (Will Kill the Game if They Happen)

| Risk | Impact | Probability | Mitigation | Owner |
|---|---|---|---|---|
| **AI text quality is bad** | Players don't invest emotionally, core loop fails | HIGH | Extensive prompt engineering, character voice guides, early testing, fallback templates | BYTE + NOVA |
| **Desktop feels fake** | Nostalgia hook fails, entire pitch collapses | MEDIUM | Reference real XP extensively, iterate on fidelity, crowdsource feedback | PIXEL + BYTE |
| **Save corruption bugs** | Lost saves = lost trust, review bombs | MEDIUM | Versioned save format, auto-backup system, continuous save/load testing | BYTE |
| **Core loop is tedious** | Players quit after 2 hours, refunds spike | MEDIUM | Playtest early and often, iterate on pacing, cut friction aggressively | REED + CRASH |
| **Performance issues on target hardware** | Steam Deck unplayable, negative reviews | LOW | Profile continuously, optimize hot paths, enforce performance budgets | BYTE |

### 3.2 High Risks (Will Hurt Quality/Reviews)

| Risk | Impact | Probability | Mitigation |
|---|---|---|---|
| **Mini-games are boring** | LAN parties feel like cutscenes | MEDIUM | Test mini-game 1 early, iterate, cut to 3 if needed |
| **Economy is unbalanced** | Too tight = frustration, too loose = no decisions | MEDIUM | Extensive balance testing, telemetry, tuning spreadsheet |
| **Character arcs feel scripted** | Emotional payoff fails, no replayability | MEDIUM | Procedural beat system, early arc testing, variance validation |
| **ISP heat system is opaque** | Players don't understand risk/reward | MEDIUM | Clear feedback, tutorial messaging, tooltips |
| **Relationship changes invisible** | Players don't see cause-effect | MEDIUM | Better feedback (away messages, forum posts, chat tone) |

### 3.3 Medium Risks (Will Cause Bugs/Frustration)

| Risk | Impact | Probability | Mitigation |
|---|---|---|---|
| **File system math breaks** | Storage counter wrong, breaks immersion | LOW | Unit test filesystem thoroughly |
| **Z-order breaks** | Windows overlap incorrectly | LOW | Test window management stress cases |
| **AI generation timeout** | Hangs, breaks flow | LOW | Typing indicator + fallback templates |
| **Life events feel random** | Story beats don't land | MEDIUM | Contextual triggers, not pure RNG |

---

## 4. Test Environments and Hardware

### 4.1 Target Hardware Configurations

**Primary (must work perfectly):**
- Windows 10/11 64-bit
- Intel i5-8250U (or equivalent mid-range 2020 CPU)
- 8GB RAM
- Integrated graphics (Intel UHD 620)
- 1920x1080 60Hz display

**Secondary (should work well):**
- Steam Deck (Proton, custom controls)
- 1440p and 4K displays (UI scaling)
- 144Hz displays (ensure no jank)

**Tertiary (best-effort):**
- Linux native (Ubuntu 22.04, Fedora 38)
- macOS (tested quarterly)

### 4.2 Test Lab Setup

- 3 test machines: Low-end (2020 laptop), mid-range (2022 desktop), Steam Deck
- Save file library: Fresh start, mid-game (hour 10), late-game (hour 20), finale
- Automated test suite runs on every commit (GitHub Actions)
- Manual playtest sessions: Weekly (internal), monthly (external)

---

## 5. Regression Test Checklist

Run this checklist before every release candidate build.

### 5.1 Core Systems Smoke Test (30 minutes)

- [ ] Launch game, create new save
- [ ] Open desktop, verify all icons present
- [ ] Open MSN, send message, receive reply
- [ ] Open file manager, create file, delete file
- [ ] Start download (P2P), verify progress bar
- [ ] Invite 3 characters to LAN party
- [ ] Host LAN party (CounterOps), complete full match
- [ ] Check forum for aftermath posts
- [ ] Save game, quit, reload save, verify state persists
- [ ] Play for 1 in-game week, verify time progression

### 5.2 Critical Path Test (2 hours)

- [ ] Full session loop: desktop → prep → LAN party → aftermath
- [ ] Acquire game via IRC (not P2P)
- [ ] Experience 1 narrative beat (drama event or life event)
- [ ] Interact with all 6 character archetypes
- [ ] Experience mini-game with 6 attendees
- [ ] Verify reputation changes after party
- [ ] Verify ISP heat increases after download
- [ ] Verify money decreases after purchase
- [ ] Verify storage fills and can be managed
- [ ] Advance 4 in-game weeks, verify no soft lock

### 5.3 Edge Case Gauntlet (1 hour)

- [ ] Open 12 windows, verify limit enforced
- [ ] Fill storage to 100%, verify downloads blocked
- [ ] Max ISP heat, verify throttling + outage
- [ ] Host party with 1 attendee (minimum)
- [ ] Host party with 12 attendees (maximum)
- [ ] Spam-click minimize/maximize 20 times (no crash)
- [ ] Send 100 messages to character (no crash)
- [ ] Delete file mid-burn (verify error handling)
- [ ] Corrupt save file (verify auto-backup recovery)
- [ ] Disconnect internet (if using external AI), verify fallback

### 5.4 Performance Verification (30 minutes)

- [ ] Desktop: 60 FPS with 12 windows open
- [ ] Mini-game: 30 FPS with 12 AI agents
- [ ] Save/load time under 500ms
- [ ] Memory usage under 2GB
- [ ] No memory leak after 1 hour session (verify with profiler)

---

## 6. Bug Triage and Severity Definitions

### Severity Levels

**S1 - Critical (Ship Blocker):**
- Crash to desktop
- Save corruption
- Soft lock (cannot progress)
- Data loss

**S2 - High (Fix Before Ship):**
- Major feature broken (MSN won't open, LAN party won't start)
- Progression blocker with workaround
- Performance below target (under 30 FPS on min spec)
- AI generates immersion-breaking text

**S3 - Medium (Fix If Time):**
- Minor feature broken (forum doesn't update)
- Visual glitch (z-order flicker)
- Rare crash (occurs in less than 5% of sessions)
- Balance issue (economy too tight/loose)

**S4 - Low (Post-Launch):**
- Cosmetic issue (wrong icon color)
- Typo in static text
- Minor UX annoyance
- Stretch goal feature incomplete

### Triage Process

1. Bug reported (via playtest, automated test, or crash log)
2. QA reproduces (if reproducible → assign severity, if not → close as "cannot repro")
3. Engineering estimates fix time
4. Product (CLOCK) decides: fix now, defer, or won't fix
5. If deferred, add to known issues list for patch planning

---

## 7. Playtesting Protocol

### 7.1 Internal Playtests (Weekly)

**Participants:** Full team (REED, NOVA, PIXEL, BYTE, ECHO, CLOCK, CRASH)

**Format:**
- 1-hour session, recorded (screen + audio)
- Focus area rotates weekly (desktop, MSN, LAN party, economy)
- No direction given ("play naturally")
- Debrief afterward: what felt good, what broke, what confused

**Deliverable:** Bug list + prioritized friction points

### 7.2 External Playtests (Monthly)

**Participants:** 10-15 external testers (Discord community, volunteer list)

**Format:**
- 2-hour session, remote (Steam Playtest build)
- Post-session survey (20 questions)
- Optional follow-up interview (5 testers)

**Survey includes:**
- "Did the desktop feel like XP?" (1-10 scale)
- "Did you care about any characters?" (Y/N + names)
- "Was the core loop fun?" (1-10 scale)
- "Where did you get stuck or confused?" (open text)
- "What would you change?" (open text)

**Deliverable:** Aggregated feedback report + bug list

### 7.3 Closed Beta (4 weeks before launch)

**Participants:** 100-200 Steam Playtest users

**Format:**
- Full game, near-final build
- Crash reporting enabled
- Survey after 5 hours, 10 hours, completion
- Discord channel for feedback

**Focus:**
- Final balance tuning
- Edge case bug hunting
- Performance validation across hardware
- Save/load stress testing (long sessions)

**Deliverable:** Launch readiness report

---

## 8. Known Limitations and Workarounds

### Limitations We Accept

**Limitation 1: AI text may occasionally repeat.**
- Acceptable if rare (under 5% of messages).
- Mitigation: Prompt engineering, increased randomness, varied templates.
- Workaround: None needed if within threshold.

**Limitation 2: Mini-games are simplified simulations.**
- Intentional design choice.
- Mitigation: Set expectations in marketing ("watch, don't play").
- Workaround: None needed, not a bug.

**Limitation 3: Desktop is not pixel-perfect XP.**
- "Good enough" > perfect.
- Mitigation: Iterate post-launch based on feedback.
- Workaround: Frame as "inspired by XP" not "exact replica."

**Limitation 4: Console/mobile not supported.**
- PC-only by design.
- Mitigation: None, accept market limitation.
- Workaround: None needed.

**Limitation 5: Replayability ceiling exists.**
- Procedural generation creates variance, but core arc is fixed.
- Mitigation: Post-launch content (new mini-games, character archetypes).
- Workaround: None at launch, roadmap for updates.

---

## 9. Post-Launch Monitoring

### 9.1 Telemetry (If Implemented)

**Track:**
- Average session length
- Where players quit (which game phase)
- Save/load frequency
- Crash locations
- Performance metrics (FPS, memory)
- Feature usage (which mini-games, which apps)

**Do NOT track:**
- Player chat input (privacy)
- Save file contents (privacy)
- Personal data (GDPR compliance)

### 9.2 Crash Reporting

**Use:** Sentry, BugSplat, or similar
**Report includes:** Stack trace, system info, game state (sanitized)
**Triage:** Daily review, prioritize by frequency

### 9.3 Community Feedback Channels

**Monitor:**
- Steam reviews (daily)
- Discord (real-time)
- Reddit threads (weekly)
- Support email (daily)

**Escalate to team:** Frequent bugs, balance complaints, confusion points

### 9.4 Patch Cadence

**Hotfix (0-3 days):** Critical bugs (crashes, save corruption)
**Patch (2-4 weeks):** High-priority bugs, balance tweaks
**Content update (2-3 months):** New mini-games, character archetypes, QoL features

---

## 10. Success Metrics

How do we know if QA succeeded? Here's the scorecard.

### 10.1 Pre-Launch Metrics

- [ ] Zero S1 bugs in final build
- [ ] Under 5 S2 bugs in known issues list
- [ ] 80%+ of playtesters rate core loop as "fun" (7+/10)
- [ ] 70%+ of playtesters report emotional attachment to characters
- [ ] Performance targets met on all test hardware
- [ ] Save/load passes 20-hour stress test with zero corruption

### 10.2 Post-Launch Metrics (First 2 Weeks)

- [ ] Crash rate under 0.5% (industry standard)
- [ ] Steam review score above 80% positive (target: "Very Positive")
- [ ] Refund rate under 10% (Steam average is ~15%)
- [ ] Average session length above 45 minutes (indicates engagement)
- [ ] Under 100 support tickets (for 10k sales)

### 10.3 Long-Term Metrics (First 3 Months)

- [ ] Completion rate above 30% (players reach finale)
- [ ] Replay rate above 15% (players start second playthrough)
- [ ] Post-launch patches: 1 hotfix, 2 balance patches, 1 content update
- [ ] Community sentiment: active Discord, positive Reddit threads, fan art

---

## Conclusion

This game is a high-wire act. We're asking players to care about AI-generated screen names in a simulated OS from 2003. If the desktop doesn't feel real, if the AI doesn't feel human, if the loop doesn't feel like caretaking, the whole thing collapses.

But if it works? If players forget they're playing a game and start treating their crew like friends? If they check MSN messages before checking the taskbar? If they feel the specific ache of watching a buddy list go gray one name at a time? Then we've built something no other game has done.

QA's job is to make sure the magic has a foundation. Test the desktop until it feels like 2003. Test the AI until it feels like people. Test the loop until it feels like care. Test the breaks until nothing breaks.

And when something does break — because it will — we fix it. No excuses, no "works on my machine," no "edge case, won't happen." If it breaks for one player, it breaks. Period.

Ship it working. Then make it better. Then make it fast. In that order.

Every bug is a betrayal of trust. Every crash is a player we let down. The edge case is someone's entire experience.

We find them all. Every single one.

That's the job.

-- CRASH

---

**Document Status:** QA Plan v1.0 complete. Ready for test implementation.

**Next Steps:**
1. Review with BYTE (technical feasibility of test automation)
2. Review with CLOCK (timeline for test phases)
3. Set up test environments and lab hardware
4. Begin Phase 1 testing (desktop simulation) in parallel with development
5. Weekly QA status reports to team

**Appendices:**
- Test case spreadsheet (CSV export for tracking)
- Bug report template
- Playtest survey template
- Performance benchmark script

**Test Coverage Summary:**
- 200+ discrete test cases across 8 feature areas
- Critical path covered end-to-end
- Edge cases enumerated per system
- Regression suite defined
- Performance benchmarks specified
- Quality gates defined (ship/no-ship criteria)

Zero placeholders. Zero assumptions. Every risk named. Every break point mapped.

Now we test it until it's bulletproof.
