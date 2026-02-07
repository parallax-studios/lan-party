# LAN PARTY — Audio Design Document

**Sound Designer:** ECHO
**Date:** 2026-02-07
**Project:** LAN PARTY — Management sim inside a 2000s desktop
**References:** `pitch.md`, `game-design.md`
**Target Platform:** PC (Steam), Steam Deck
**Audio Philosophy:** Audio IS game feel. The desktop must sound alive.

---

## 1. Sonic Identity Statement

**LAN PARTY sounds like digital archaeology — the specific electromagnetic hum of CRT monitors, mechanical hard drives seeking data, and the plastic click of a mouse navigating a world that existed entirely inside glowing screens.**

The audio is not nostalgic pastiche. It is period-accurate reconstruction. Every sound must pass the test: would this exact frequency have existed in a suburban basement in 2003?

---

## 2. Sonic Palette

### 2.1 Keynote: The Desktop Orchestra

The keynote is **electromagnetic presence** — the layered drone of technology at idle. A 2003 desktop was never silent. There was always:

- CRT monitor @ 15.75kHz (audible whine for those who remember)
- Hard drive platters spinning @ low rumble (40-60Hz)
- Case fans cycling (broadband whoosh, slightly irregular)
- The occasional HDD seek (mechanical click-tick-click)
- Distant household ambiance bleeding through (muffled TV, footsteps above, refrigerator hum)

This keynote is ever-present, mixed low but perceptible. It is the **room tone of the game**. When the player boots the desktop, this layer fades in like powering on a machine. Close your eyes — what do you hear? A bedroom with a computer in it. Not silence. Presence.

### 2.2 Texture: Warm Plastic and Cold Data

The sonic texture splits into two domains:

**Physical (warm, organic, imperfect):**
- Mouse clicks: plastic shell resonance, slight variation per click (not perfectly uniform)
- Keyboard typing: membrane keys, not mechanical — softer, mushier, the sound of a 2003 Dell keyboard
- CD tray ejection: motor whir + plastic latch + slight rattle
- Tactile interactions: dragging windows (friction metaphor), minimizing (zip down with pitch drop), right-click context menus (light pop)

**Digital (cold, precise, synthetic):**
- System beeps: pure sine tones, no warmth, 1000Hz notification chime
- Download progress: no sound until completion (then chime + brief HDD write burst)
- Error dialogs: harsh alert tones, slightly unpleasant (the Windows XP critical stop sound is 783Hz sawtooth — reference this)
- Network activity: subtle data stream texture (think dial-up residue, even though it is broadband — a ghost of the previous era)

The contrast between physical and digital is intentional. Physical sounds root the experience in a body sitting at a desk. Digital sounds remind you that the world you are navigating is made of light and voltage.

### 2.3 Space: Intimate, Enclosed, Teenage Bedroom

The spatial signature is **small room reverb** — bedroom acoustics. Not a studio. Not a cathedral. A 10x12 foot room with carpet, posters on the walls, and a closed door. Reflections are soft, decay times are short (0.3-0.6s), and the space feels **close**. You are always aware that you are in a room with this machine.

During LAN party phases, the space **expands but does not open**. Now it is basement acoustics — concrete floor, exposed ceiling joists, slightly more reflective surfaces. The reverb gets slightly longer (0.8-1.2s) and brighter. The room has **filled with people and machines**, and the acoustic signature changes to match.

### 2.4 Reference Tracks and Games

These are the sonic touchstones. Not for direct imitation, but for **emotional frequency**.

**Games:**

1. **Hypnospace Outlaw** — Nailed the late-90s digital interface audio. Every click, every page load, every MIDI jingle. Proof that period-accurate audio can carry a game. Listen to: the way MIDI music plays through the in-game OS with slightly compressed fidelity, the modem handshake sequence, the desktop icon sounds.

2. **Papers, Please** — Sparse, functional, rhythmic. Every stamp, every checkbox, every denied entry has weight. Listen to: the way repetitive actions (stamping) have enough sonic variation that 1000 repetitions do not drive you insane, the document sliding sound (paper on desk), the use of silence between intense moments.

3. **The Sims (2000)** — The ambient soundscape of domestic life. Listen to: background presence of a household (muffled conversations, appliance hums, distant music from a stereo), layered ambiance that fills space without demanding attention, the way environment audio shifts based on room and activity.

4. **Emily is Away** — Chat interface audio. Listen to: typing sounds that feel like another person is on the other end (variable rhythm, pauses for thought), the AIM door open/close sound (iconic), away message change notification, the silence that makes you wait for a reply.

**Music/Soundtracks:**

5. **Boards of Canada — Music Has the Right to Children (1998)** — Warm analog nostalgia, VHS tracking artifacts, childhood memory through degraded media. This is the emotional frequency of looking back at a technological moment that has passed. Listen to: "Roygbiv" for wistful optimism, "Telephasic Workshop" for the ghostly presence of recorded voices, the textural warmth throughout.

6. **The Postal Service — Give Up (2003)** — Exactly the right year. Electronic indie, laptop production, bedroom-recorded vocals. This album WAS on Winamp playlists in 2003. Listen to: "Such Great Heights" for the blend of synthetic and human, "Clark Gable" for glitchy nostalgia, the intentional lo-fi digital artifacts.

7. **Linkin Park — Hybrid Theory (2000)** — Not because LAN PARTY sounds like nu-metal, but because this album contextualizes the era's audio landscape. High dynamic range (whisper to scream), heavy compression, digital distortion as texture, aggression as catharsis. This is what teenage players were listening to through Winamp while downloading warez. Reference track: "Papercut" for the tension build.

8. **Ambientsoundscapes — "2000s Computer Lab"** (field recording archival projects) — Literal reference material. The sound of 20 CRT monitors humming in a room, hard drives seeking in chorus, chair squeaks, distant keyboard clatter. This is documentary audio.

### 2.5 What This Palette Excludes

**No orchestral swells.** No cinematic bombast. No EDM drops. No modern production sheen. If it could not have come out of a 2003 bedroom setup — a desktop PC, maybe a MIDI keyboard, maybe a cheap mic and pirated Fruity Loops — it does not belong.

---

## 3. Sound Effects Design

SFX are organized by **interface layer**, not by category. In LAN PARTY, there are no "combat sounds" or "enemy sounds" — there are only desktop sounds, LAN party event sounds, and environmental room tone.

### 3.1 Desktop Interface — Core Loop (90% of playtime)

These sounds must sustain 15-25 hours of repetition without causing fatigue. Every sound needs **micro-variation** — 3 to 5 variants per action, rotated dynamically.

#### Mouse & Keyboard Input

| Action | Description | Emotional Function | Variants |
|---|---|---|---|
| **Mouse Click (default)** | Hollow plastic click, ~50ms duration, light tactile pop. Mid frequency (800-1200Hz fundamental). No reverb. | Confirms intent. Must feel responsive, immediate. | 5 variants: slight pitch/timbre variation, none longer than 60ms |
| **Mouse Double-Click** | Two clicks at 120ms interval, second slightly quieter. | Signals "opening" an object. Faster rhythm = urgency. | Same variants as single click but paired |
| **Mouse Drag Start** | Subtle grab (brief friction texture + slight pitch drop 50Hz). | Feels like picking something up. | 3 variants |
| **Mouse Drag Release** | Light thud (drop onto surface), depends on what is dropped. Window = thud + rattle. Icon = lighter click. | Completes the physical metaphor. | Contextual per object type |
| **Right-Click (context menu)** | Slightly sharper click than default + soft menu pop (synthetic, ~300Hz low sine burst, 40ms). | Signals "more options available." Slightly different texture flags secondary action. | 3 variants |
| **Keyboard Typing** | Soft membrane key press, muffled, 120-300Hz range. Rhythm irregular (human typing pattern). Each keypress 20-35ms duration with slight key return sound (softer). | Creates presence of the player as a body. You are there, typing. | 12 variants (full character set variations) + rhythm variation algorithm |
| **Keyboard Enter/Return** | Slightly louder and longer than standard key (45ms), additional small plastic resonance tail. | Sends the message. Confirmation + finality. | 4 variants |
| **Backspace/Delete** | Reverse texture — key press + very subtle reverse envelope (attack on release), slightly higher pitch. | Feels like undoing. Audio metaphor for erasure. | 4 variants |

#### Window Management

| Action | Description | Emotional Function | Variants |
|---|---|---|---|
| **Window Open** | Brief system chime (~600Hz sine, 80ms) + soft whoosh as window appears (white noise envelope, 200ms fade-in). Light HDD seek click at end (2-3 clicks in 150ms burst). | Signals new context opened. The HDD click sells the illusion of data being loaded. | 4 variants (slight timing variation) |
| **Window Close** | Inverse of open: soft whoosh out (white noise fade-out, 150ms) + brief system beep (700Hz, 60ms). No HDD sound (closing does not write). | Completion. Returns attention to previous layer. | 4 variants |
| **Window Minimize** | Zip-down: descending pitch glide (800Hz -> 200Hz over 180ms) + compressed whoosh. Window "falls" into taskbar. Cartoonish but period-accurate (XP had this energy). | Playful. Satisfying. Encourages active window management. | 3 variants (slight glide curve differences) |
| **Window Maximize/Restore** | Quick two-tone beep (500Hz -> 700Hz, 100ms total) + brief expansion whoosh (inverse of minimize, rising pitch). | Spatial change. Window now fills the world. | 3 variants |
| **Window Drag** | Continuous subtle friction texture while dragging (granular noise, low-pass filtered, tied to mouse velocity). Stops on release. | Maintains tactile illusion. You are moving a physical thing. | Dynamic (generated based on drag speed) |
| **Alt-Tab (window switch)** | Soft swoosh + beep (1000Hz, 40ms), very fast. Designed for rapid repetition. | Expert player action. Must be fast and unobtrusive. | 2 variants |

#### Application-Specific Sounds

These sounds are critical. They define each app's personality.

**MSN Messenger:**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Message Received** | Two-tone beep (ascending, 800Hz -> 1000Hz, 120ms total) + brief window pop if minimized. Lower volume if window is open. | Instant dopamine. Someone is talking to you. This sound must feel GOOD. | 3 variants (slight timbre shifts) |
| **Contact Signs In** | Door opening sound (real door creak + latch, 600ms, warm and friendly). Iconic. This is THE sound. | Presence. Your world just got bigger. | 2 variants (slight creak variation) |
| **Contact Signs Out** | Door closing sound (softer, 500ms, slightly sad frequency content — door closing always feels like goodbye). | Absence. Designed to create slight melancholy. | 2 variants |
| **Typing Indicator (buddy is typing)** | Soft mechanical type texture loop (quiet, 30% volume of regular typing, irregular rhythm suggesting someone else's pattern). | Anticipation. They are about to say something. | 1 continuous loop with variation algorithm |
| **Nudge Received** | Window shake + loud alert buzz (450Hz sawtooth, 300ms, slightly annoying). | Attention demand. Designed to be impossible to ignore. | 1 variant (consistency is the point) |
| **Status Change** | Subtle UI chime (400Hz, 60ms) + brief rustle (like paper shifting). | Passive information. Buddy list is alive and changing. | 3 variants |

**mIRC (IRC Client):**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Channel Join** | Soft blip (900Hz, 50ms) + username text printing sound (fast typewriter burst, 100ms). | Someone entered the room. Not as emotionally weighted as MSN. | 2 variants |
| **Channel Part/Quit** | Descending blip (900Hz -> 600Hz, 70ms). | Someone left. Neutral. | 2 variants |
| **Message in Active Channel** | Soft tick (700Hz, 30ms). Repeats per message. If player is in the channel, lower volume. If player is in a different channel, louder. | Keeps channels feeling alive. Background conversation hum. | 4 variants |
| **Private Message (PM/Query)** | Harsher alert beep (1200Hz, 100ms) + brief text print. More urgent than channel message. | Direct communication. Demands attention. | 2 variants |
| **DCC Transfer Request** | Synthetic alert (two-tone, 600Hz -> 900Hz, 200ms) + dialog box pop. | High importance. File transfer is a big deal. | 1 variant |
| **DCC Transfer Progress** | No continuous sound. Silence except for periodic HDD write bursts (every 10-15% progress, brief click-tick-click, 100ms). | Progress is background. Completion is foreground. | Dynamic |
| **DCC Transfer Complete** | Success chime (ascending arpeggio, 600-800-1000Hz, 250ms total) + HDD write finalization (longer burst, 300ms). | Victory sound. You got the file. | 2 variants |

**File Manager (Explorer):**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Folder Open** | Soft rustle (paper folder opening, 150ms) + brief HDD seek if folder has many files. | Navigation. Physical metaphor. | 3 variants |
| **Folder Close** | Inverse rustle (shorter, 100ms). | Closing a drawer. | 3 variants |
| **File Select** | Single click (same as mouse click but with additional select confirmation, 600Hz beep 30ms). | Highlight. This is the active object. | 3 variants |
| **File Copy Start** | Brief confirmation beep (700Hz, 60ms) + HDD activity starts (continuous random seek pattern). | Operation initiated. Machine is working. | 2 variants |
| **File Copy Progress** | HDD activity continues (low rumble + periodic seeks). Progress bar is visual, audio is atmospheric. | Machine labor. Selling the illusion of data moving. | Dynamic loop |
| **File Copy Complete** | Completion chime (bright, 1000Hz, 100ms) + HDD activity stops abruptly. | Task done. Clean resolution. | 2 variants |
| **File Delete** | Trash can rustle (plastic bag crinkle, 200ms) + brief HDD write (file table update). | Slight guilt texture. Deletion is not free. | 3 variants |
| **File Open/Execute** | Double-click sound + loading sequence (HDD seek burst, 300-500ms) + application-specific launch sound if available. | Starting something. Transition to new context. | Contextual per file type |

**CD Burner (Nero-style):**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Burn Start** | CD tray close sound (motor whir + plastic latch, 800ms) + drive spin-up (low rumble rising in pitch over 2 seconds). | Ritual beginning. This is important. | 2 variants |
| **Burn Progress** | Continuous CD drive rumble (low frequency, 80-120Hz, with periodic speed variations as drive adjusts). Hypnotic. Layer occasional HDD read bursts (source data). | Duration sound. This takes time. Player can walk away. | Dynamic loop (5-10 min duration) |
| **Burn 25% / 50% / 75% Marks** | Brief confirmation beep (rising pitches: 600Hz / 700Hz / 800Hz, each 50ms) over the rumble. | Progress markers. Reassurance that it is working. | 1 each |
| **Burn Complete** | Drive spin-down (rumble descends over 3 seconds) + success fanfare (three-tone ascending, 700-900-1100Hz, 400ms total) + tray eject (motor + latch). | Victory. You made a thing. This should feel GOOD. | 2 variants |
| **Burn Failure** | Abrupt drive stop (rumble cuts) + harsh error beep (400Hz sawtooth, 500ms) + tray eject (same as success but now sounds like shame). | Gut punch. You wasted a CD. This should sting. | 1 variant (consistency = emotional weight) |

**Winamp:**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Play/Resume** | Soft analog click (tape deck start metaphor, 80ms) + music fades in over 200ms. | Music begins. Atmosphere shifts. | 2 variants |
| **Pause** | Inverse click (tape deck stop, 60ms) + music fades out over 150ms. | Stillness. Foregrounds other audio. | 2 variants |
| **Track Change (Skip)** | Brief whoosh (100ms) + new track fades in. No silence gap. | Seamless transition. Maintains energy. | 2 variants |
| **Volume Adjustment** | No sound (visual only). Audio volume change IS the feedback. | — | — |
| **Playlist Scroll** | Soft scroll texture (paper rustle, quiet, tied to scroll speed). | Browsing your library. Tactile. | Dynamic |

**P2P Client (Kazaa-style):**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Search Initiated** | Brief modem-esque chirp (digital noise burst, 200ms, filtered) + loading. | Reaching out into the network. Slightly mysterious. | 2 variants |
| **Search Results Populate** | Soft pings as each result appears (800Hz, 30ms per result, rapid succession). | Data arriving. Possibility. | 1 variant |
| **Download Start** | Confirmation beep (600Hz, 80ms) + network activity starts (subtle broadband static texture, very quiet). | Connection established. Risky. | 2 variants |
| **Download Progress** | Network activity continues (quiet static layer) + periodic HDD write bursts (every 5-10%). No music. Tension. | Waiting. Vulnerable. This audio should feel slightly uneasy. | Dynamic loop |
| **Download Complete** | Success chime (same as DCC transfer) + HDD finalization + network activity stops. | Relief. But did you get the right file? | 2 variants |
| **Download Failed** | Error buzz (400Hz, 300ms) + network activity stops abruptly. | Frustration. Connection lost. | 2 variants |

**Web Browser:**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Page Load Start** | Brief click (navigation) + network activity (modem ghost texture, 500ms). | Loading. Patience required. | 2 variants |
| **Page Load Complete** | Soft chime (done loading, 900Hz, 70ms). | Page is ready. | 2 variants |
| **Link Click** | Standard mouse click + brief navigation sound (400Hz blip, 40ms). | Hyperlink jump. Transition. | 3 variants |

**System Tray / Notifications:**

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **Background Notification** | Bubble pop sound (soft, 500Hz, 100ms) + balloon tooltip SFX (paper unfold, 150ms). | Passive information. Does not demand immediate attention. | 3 variants |
| **Critical Alert** | Loud error sound (harsh sawtooth, 783Hz like XP critical stop, 400ms). | Emergency. Stop what you are doing. | 1 variant (consistency = urgency) |
| **Clock Tick (Hour Change)** | Very quiet clock tick (mechanical, 50ms, only audible if room is silent). | Time passing. Subtle pressure. | 1 variant |

#### Hardware / Environmental Desktop Sounds

| Event | Description | Emotional Function | Variants |
|---|---|---|---|
| **HDD Idle** | Continuous platter spin (40-60Hz rumble, very quiet, always present). | Machine is alive. Foundation of the keynote. | 1 loop |
| **HDD Seek** | Mechanical click-tick-click (variable rhythm, 100-300ms burst, mid-frequency). Randomized timing based on activity. | Machine is working. Sells data operations. | 8 variants (different seek patterns) |
| **HDD Thrashing (high load)** | Rapid seek barrage (10+ seeks in 2 seconds). Sounds stressed. | System under load. Feels like strain. | 3 variants |
| **Case Fan** | Broadband whoosh (air moving, slightly irregular, 200-4000Hz). Always present. Occasional fan speed change (pitch shift over 5-10 seconds). | Cooling. Part of the machine's breath. | 1 loop with dynamic pitch modulation |
| **CRT Monitor Hum** | 15.75kHz whine (right at the edge of audibility for many, lo-fi filtered to 8-12kHz for accessibility). Always present if monitor is on. | Period authenticity. Older players will FEEL this. | 1 loop |
| **CRT Degauss** | Loud magnetic BWOOOONG (descending pitch, 1 second, rattles the speakers). Rare event (player-triggered or random during boot). | Visceral. Physical. Nostalgia bomb. | 2 variants |
| **Power On** | CRT warm-up whine (ascending pitch over 3 seconds) + HDD spin-up + Windows boot sound. | Birth of the world. Game start. | 1 sequence |
| **Power Off** | HDD spin-down + CRT discharge (descending whine, 2 seconds, ends in soft click). | Death of the world. Game save. | 1 sequence |

### 3.2 LAN Party Phase — Event Sounds (25% of playtime)

The sonic space SHIFTS during LAN parties. We transition from single-desktop to multi-desktop + human presence.

#### Spatial Transition

When entering LAN party phase:
- Desktop keynote (CRT + HDD + fan) **multiplies** — now 5-8 machines humming in a room
- Room reverb shifts from bedroom (0.3-0.6s) to basement (0.8-1.2s), brighter reflections
- New ambient layer fades in: **human presence soundscape** (see below)

#### Human Presence Soundscape

This layer is mixed at ~30-40% volume relative to machine sounds. It is always present during LAN party phase, creating a bed of social presence. It is NOT individual voices (no dialogue) but **group texture**.

| Element | Description | Emotional Function |
|---|---|---|
| **Crowd Murmur (5-8 people)** | Indistinct conversation texture. Low-pass filtered (no intelligible words), variable density (sometimes quiet, sometimes overlapping). Occasional laughter spike. Male-skewed frequency content (teenage boys, mostly). | Room is full. You are hosting a thing. Warmth. |
| **Chair Creaks/Shifts** | Wood or plastic chair movement, periodic, tied to game intensity (more movement during tense moments). | Bodies in space. Restlessness. |
| **Controller/Mouse Clicks** | Not your desktop's clicks — these are OTHER people's clicks. Scattered spatially. During game moments, rapid clicking increases (intensity). | Collective action. Everyone is doing something. |
| **Footsteps (Occasional)** | Someone gets up. Walk to bathroom, get snacks, adjust cables. Footsteps on concrete (basement floor). Rare but grounds the scene. | Breaks. Movement. Life. |
| **Snack Sounds** | Chip bag rustle, can opening (pssh + crack), chewing textures (quiet, gross, human). Increases player immersion in the PHYSICAL party. | Embodiment. These are bodies, not just screen names. |
| **Keyboard Clatter (Multiple)** | 3-5 keyboards typing at once, asynchronous, membrane keys. During chat moments, increases. During game moments, decreases. | Communication. Coordination. |

#### Game-Within-Game Sounds

The actual game being played at the LAN party has audio, but it is **simplified and distant**. Full game audio would distract from the management layer. Instead, we hear:

| Game Type | Audio Signature | Emotional Function |
|---|---|---|
| **FPS (CounterOps)** | Gunfire (simplified, 3-4 shot sounds), explosions (muffled bass), footsteps, reload clicks. All slightly distant, like hearing it from another room. | Action. Intensity. Competitive energy. |
| **RTS (StarFight)** | UI beeps, unit acknowledgment sounds ("affirmative" style voice samples, lo-fi), building construction, battle ambiance (distant). | Strategic. Methodical. Lower intensity. |
| **Racing (Blur Kart)** | Engine drones (pitch shifts with speed), collision impacts, drift sounds, item pickup bleeps. | High energy. Chaotic. Fun. |
| **Fighting (BrawlMasters)** | Hit impacts (punchy, exaggerated), special move whooshes, announcer call samples (rare, lo-fi). | Rhythmic. Hype moments. |

Game audio is mixed at 40-50% volume and EQ'd to sound like it is coming from multiple speakers around a room (stereo spread, slight phasing). It is background to the foreground of **player management actions** and **chat interface**.

#### Event-Specific Stingers

These are triggered by narrative moments during the party.

| Event | Sound | Emotional Function |
|---|---|---|
| **Someone Rage-Quits** | Chair scrape (loud, harsh) + keyboard slam (impact) + footsteps storming away + door slam (distant). Crowd murmur drops briefly (shocked silence). | Drama. Tension. Uh-oh. |
| **Epic Play / Clutch Moment** | Crowd erupts: overlapping shouts, chair scrapes (standing), hand slaps (high-fives). Game audio swells briefly. | Hype. Collective joy. THIS is what it is about. |
| **Hardware Crash** | Abrupt silence from one machine (that machine's fan/HDD stops) + error beep + frustrated groan from crowd. | Technical failure. Host embarrassment. Scramble mode. |
| **Network Lag** | Game audio stutters (digital glitch texture) + frustrated groans + "LAAAAG" shout texture. | Frustration. Host responsibility. |
| **Snack Break Called** | Chair scrapes (multiple, people standing) + footsteps + chip bag rustles increase + conversation murmur rises (no game audio pressure). | Relief. Social moment. Breathing room. |
| **Fight Brewing** | Conversation murmur sharpens (argumentative frequency content, still no words) + game audio continues but crowd murmur detaches from game (people stop playing, turn to watch argument). | Social tension. Intervention needed. |
| **Bonding Moment** | Laughter spike (genuine, warm) + game audio stays level + murmur softens (people are smiling, not just playing). | Connection. This is working. |

### 3.3 Aftermath Phase — Minimal New Sounds

Aftermath phase returns to desktop interface, so all desktop SFX apply. New elements:

| Event | Sound | Emotional Function |
|---|---|---|
| **Forum Post Notification** | Browser page load complete + new post alert (soft chime). | Reaction arriving. Social echo. |
| **Reputation Change (up)** | Subtle positive chime (ascending two-tone, 800-1000Hz, quiet, 100ms). Not announced visually, just a feeling. | Reward. Growth. |
| **Reputation Change (down)** | Subtle negative tone (descending, 700-500Hz, quiet, 100ms). | Consequence. Regret. |

---

## 4. Music Direction

### 4.1 Style and Instrumentation

Music in LAN PARTY is NOT a traditional soundtrack. Music exists **diegetically** — it comes from Winamp. The player chooses what plays. But the music available in Winamp is curated to fit the world.

**Musical Style: Early 2000s Bedroom Electronic + Post-Grunge**

The in-game music library spans genres that would have been on a 2003 hard drive:

1. **Electronic / IDM / Downtempo** (Boards of Canada, Aphex Twin, The Postal Service, Air)
2. **Post-Grunge / Alt-Rock** (Linkin Park, Deftones, Incubus, System of a Down)
3. **Hip-Hop / Trip-Hop** (Eminem, Gorillaz, Massive Attack, RJD2)
4. **Pop-Punk / Emo** (Blink-182, Dashboard Confessional, Taking Back Sunday)
5. **Trance / Dance** (Paul Oakenfold, Tiësto, Darude yes really)
6. **Video Game OSTs** (DDR Eurodance, Tony Hawk punk, Halo ambient)

All music is **original compositions in these styles**, not licensed tracks (budget reality). Each track is written to feel period-authentic — production techniques, instrumentation, and mix aesthetics must pass the 2003 test.

**Instrumentation Palette:**

- **Electronic:** Software synths (VA subtractive, FM), drum machines (808/909 samples), arpeggiators, lo-fi sampling artifacts, intentional aliasing, sidechain compression, bitcrushing
- **Rock:** Distorted guitars (solid-state amp sim, high gain), bass guitar (picked, aggressive), live drums (heavily compressed), shouted/sung vocals (present but not lyrically dense — mostly "whoa-oh" textures)
- **Ambient:** Pad synths, field recordings (degraded, VHS-quality), music box, piano, found sound percussion

**Production Aesthetic:**

- **Loudness war casualties** — moderate to heavy limiting, squashed dynamics, 2003 masters were LOUD
- **Compression** — aggressive, pumpy, especially on rock tracks
- **Reverb** — early digital reverb algorithms (slightly metallic, not lush convolution), short decay on rock, longer on electronic
- **Lo-fi artifacts** — MP3 compression artifacts (subtle), slightly crushed high end (everything was 128kbps back then)

### 4.2 Emotional Arc Across the Meta Loop

Music selection by the player is a CHOICE, but the available music changes across the game's phases, subtly guiding the emotional tone.

| Game Phase | Available Music Bias | Emotional Target |
|---|---|---|
| **Genesis (Weeks 1-3)** | High-energy, optimistic, discovery. Pop-punk, trance, upbeat electronic. | Excitement. Possibility. Building something. |
| **Growth (Weeks 4-8)** | Full library available. Player has total freedom. Peak musical diversity. | Confidence. Mastery. Your world, your soundtrack. |
| **Golden (Weeks 9-12)** | Same library, but player has developed habits. They have "their" playlist now. | Comfort. Ritual. This is established. |
| **Fracture (Weeks 13-16)** | Library unchanged, but new tracks unlock — slower, more introspective. Post-rock, ambient, downtempo. Player might not notice at first. | Melancholy creeping in. Mood shifts. |
| **Finale (Weeks 17-20)** | Playlist feels heavier now. Upbeat tracks available but feel wrong. Player gravitates toward reflective music. | Bittersweet. Acceptance. Last times. |

This is NOT forced. The player can blast Linkin Park during the finale if they want. But the OPTION of introspective music arriving late creates an emotional off-ramp for players ready to feel the ending.

### 4.3 Adaptive Music Layers

Music is NOT dynamically adaptive in the traditional sense (no iMUSE-style stem mixing) because it is diegetic — it is literally Winamp playing. But there are adaptive rules:

**Volume Ducking:**

- **Desktop Phase:** Winamp at 100% if player wants. But if a critical notification arrives (MSN nudge, critical alert, DCC transfer request), music ducks to 60% for 3 seconds, then fades back.
- **LAN Party Phase:** Winamp (if player left it playing) ducks to 30-40% and mixes with game audio + crowd ambiance. Music becomes background. Player can pause it in-game.
- **Aftermath Phase:** Music returns to 100% if it was playing.

**Contextual Playlist Suggestions:**

The game does not force music, but Winamp's "Auto-DJ" mode (optional feature) will queue contextually appropriate tracks:

- **Pre-party prep:** Higher energy, hype tracks (pump-up music)
- **Post-party aftermath:** Lower energy, reflective tracks (comedown music)
- **Late night (in-game 12 AM - 4 AM):** Ambient, downtempo, chill tracks
- **High-tension moments (fight brewing, ISP warning, relationship crisis):** Music auto-pauses or shifts to tension-appropriate track if Auto-DJ is on

### 4.4 Mixtape System (Stretch Goal)

If scope allows, the **mixtape mechanic** becomes a musical expression tool:

- Player can burn custom CDs in Winamp
- Mixtapes can be "given" to characters via MSN file transfer
- Characters REMEMBER the mixtape content and reference it in dialogue ("that track you sent me last week is stuck in my head")
- Characters have music preferences (some like metal, some like electronic) — a well-chosen mixtape boosts relationship significantly

Mixtapes are **not mechanically mandatory** but are a high-skill relationship tool for players who engage with the music layer.

### 4.5 Silence Map — Where Music Should NOT Play

Silence is a sound design choice. These moments should have NO MUSIC even if the player left Winamp on (music auto-pauses or is absent from the mix):

1. **Game Boot Sequence** — Just hardware sounds. Let the desktop come alive without music competing.
2. **Critical Relationship Conversations** — If an MSN conversation hits a high emotional beat (character is upset, confessing something, leaving), music ducks to near-silence. The words and the silence matter more.
3. **ISP Warning / Consequences** — These moments should feel cold and serious. Music stops. Just the CRT hum and your heartbeat.
4. **Last LAN Party Ending** — Music can play during the party, but when the last person leaves and you return to desktop, there should be a moment of silence. Just the machines. Just you. The emptiness is the point.
5. **Character Departure Scenes** — When a character's away message changes to "Moving away. Thanks for everything" or similar, music pauses for 10 seconds. Honor the moment.

Silence in these moments makes them LOUDER.

---

## 5. Adaptive Audio System

LAN PARTY is not an action game. It does not need combat music stems or health-based intensity layers. But it IS a systems-driven game, and audio must respond to state.

### 5.1 Game States and Audio Profiles

| State | Active Audio Layers | Mix Focus | Transition Type |
|---|---|---|---|
| **Desktop (Idle)** | Desktop keynote (CRT+HDD+fan) at 100%, Winamp music (player choice), no notifications | Music foreground, environment background | — |
| **Desktop (Active Triage)** | Keynote at 80%, notification sounds frequent, typing sounds, app-specific SFX, music at 70-80% | SFX foreground, music supports | Smooth crossfade |
| **LAN Party (Pre-Start)** | Keynote multiplies (5-8 machines), human presence fades in, music ducks to 40%, setup SFX | SFX foreground, ambiance rising | 3-second crossfade with reverb shift |
| **LAN Party (Active)** | Multi-machine keynote, full human presence, game audio, chat SFX, music at 30% or paused | Game audio + crowd ambiance foreground | — |
| **LAN Party (High Intensity)** | Same as active but human presence louder, game audio more aggressive, music swells slightly if hype track | Crowd energy foreground | Dynamic intensity ramp over 10-30 seconds |
| **LAN Party (Conflict Event)** | Crowd murmur sharpens, game audio ducks, music stops, conflict stinger plays | Conflict SFX foreground, everything else backs off | Hard cut for music stop, stinger plays over |
| **LAN Party (End)** | Human presence fades out over 30 seconds (people leaving), machines spin down one by one, music fades back in softly, return to single-desktop keynote | Transition to silence, then music return | Long crossfade |
| **Aftermath (Reading Fallout)** | Desktop keynote, music resumes, slower notification rate, reflective energy | Music foreground, sparse SFX | Smooth fade-in |

### 5.2 State Transition Mapping

```
    DESKTOP (IDLE)
         |
         v
    DESKTOP (ACTIVE TRIAGE) <--> [notification spike triggers active state]
         |
         v
    LAN PARTY (PRE-START) <-- [player clicks "Start Party" button]
         |
         v
    LAN PARTY (ACTIVE) <--> [party begins, characters arrive]
         |
         +---> LAN PARTY (HIGH INTENSITY) <-- [hype event, close game, tournament]
         |
         +---> LAN PARTY (CONFLICT EVENT) <-- [fight, crash, drama trigger]
         |
         v
    LAN PARTY (END) <-- [party timer expires or player ends early]
         |
         v
    AFTERMATH (READING FALLOUT)
         |
         v
    DESKTOP (IDLE) <-- [loop restarts]
```

### 5.3 Real-Time Parameter Mapping

These parameters drive real-time audio changes:

| Parameter | Audio Effect | Implementation |
|---|---|---|
| **Notification Queue Length** (0-10+) | As queue grows, desktop keynote pitch subtly rises (+5-10% at 10+ notifications). Slight tension. | Pitch modulation on keynote loop, capped at +10% |
| **Download Progress** (0-100%) | HDD seek frequency increases toward completion. No audio at 0-30%, light at 30-70%, heavier at 70-99%, burst at 100%. | Dynamic seek trigger rate tied to progress % |
| **Party Energy Meter** (0-100%) | Human presence volume scales with energy (low energy = quieter crowd, high = louder). Game audio intensity also scales. | Volume automation + layer intensity |
| **Time of Day (In-Game)** | Room ambiance shifts: daytime = brighter, more household sounds; nighttime = darker, quieter, more isolated. CRT hum feels louder at night (psychoacoustic, actually same volume). | Ambiance layer swap, EQ shift on keynote (boost lows at night) |
| **Relationship Score (with any character)** | No direct audio feedback, BUT low relationship characters' messages have slightly harsher notification sounds (more sawtooth, less sine). Subtle negative association. | Per-character notification sound variant selection based on relationship tier |
| **ISP Heat Level** (hidden meter, 0-100%) | As heat rises, occasional network "glitch" sounds appear (digital artifacts, brief static bursts, very subtle). At high heat, these become more frequent. Subliminal unease. | Random glitch trigger rate tied to heat %, very low volume |

### 5.4 Vertical Layering — Ambiance Density

The desktop ambiance is vertically layered. All layers play simultaneously but mix balance shifts based on state:

**Layer Stack:**

1. **Base:** CRT hum + HDD idle spin (always present, never changes)
2. **Activity:** HDD seeks (dynamic based on system activity)
3. **Household:** Distant TV, footsteps above, refrigerator hum (bedroom ambiance, daytime only)
4. **Night:** Crickets outside, distant car (nighttime only, replaces household)
5. **Weather:** Rain on window (rare, random, adds texture)

**State-Based Mix:**

- **Idle Desktop:** Base 100%, Household/Night 40%, Activity 20%, Weather 30%
- **Active Desktop:** Base 80%, Household/Night 20%, Activity 80%, Weather 20%
- **LAN Party:** Base layer MULTIPLIES (5-8 instances of CRT+HDD), Household/Night 0%, Activity 100%, Weather 0%

### 5.5 Horizontal Sequencing — Event Triggers

Horizontal sequencing is simple: one-shot sounds triggered by events. No complex music sequencing. Timeline is driven by player actions and AI character behaviors, not authored content.

**Example Event Chain (Typical LAN Party Start):**

```
[Player clicks "Start Party"]
  -> State transition sound (desktop to party)
  -> Reverb shift (bedroom -> basement)
  -> Keynote multiplication begins (5 machines spin up over 10 seconds)
  -> Human presence fade-in (murmur + footsteps)
  -> Character 1 arrival stinger (door open, "hey!", chair scrape)
    -> [wait 5-15 seconds based on character punctuality]
  -> Character 2 arrival stinger
    -> [wait...]
  -> Character N arrival stinger
  -> [all characters present]
  -> Game selection sound (player chooses game, confirmation beep)
  -> Game audio fades in
  -> Party state = ACTIVE
```

This is event-driven, not time-driven. Audio responds to simulation state, not to a clock.

---

## 6. Mix Hierarchy — Priority and Ducking

In a game where 90% of audio is UI feedback, mix hierarchy is CRITICAL. The player must always hear what matters.

### 6.1 Priority Tiers

Audio events are assigned priority tiers. Higher priority events duck lower priority.

| Tier | Priority Level | Examples | Duck Rule |
|---|---|---|---|
| **Critical** | 1 (highest) | ISP warning, system crash, critical relationship moment notification, LAN party disaster event | Ducks all other audio to 30% for duration + 1 second tail |
| **High** | 2 | MSN message, mIRC PM, download complete, burn complete, character sign-in/out | Ducks music to 60% for 3 seconds, ducks ambiance to 80% |
| **Medium** | 3 | Mouse clicks, typing, window management, file operations, most desktop SFX | Ducks nothing, coexists with all layers |
| **Low** | 4 | Ambiance, HDD idle, CRT hum, background crowd murmur | Always present, never ducks anything, can be ducked by everything |
| **Music** | 5 (special) | Winamp playback | Ducked by tier 1-2, never ducks anything else, player-controlled volume |

### 6.2 Ducking Curves

Ducking is not instant. It uses **attack and release curves** to feel natural:

- **Attack (ducking down):** 50-100ms (fast but not abrupt)
- **Hold (at ducked volume):** Duration of higher-priority sound
- **Release (returning to normal):** 500-1000ms (slow, smooth, less noticeable)

**Exception:** Critical alerts use instant attack (0ms) for urgency. Release is still smooth.

### 6.3 Frequency Masking and EQ Relationships

Beyond volume ducking, tiers are EQ'd to occupy different frequency zones and avoid masking:

| Tier | Frequency Focus | EQ Strategy |
|---|---|---|
| **Critical** | Mid-range (600-1500Hz) — human ear most sensitive here | Boost mids, ensure cutting through |
| **High** | Upper-mids (1000-3000Hz) | Bright, clear, present |
| **Medium (Mouse/Keys)** | Mid-high (800-1500Hz) | Balanced, natural |
| **Low (Ambiance)** | Low-mids and sub (40-400Hz) and high air (8k+) | Avoids mid-range where priority events live |
| **Music** | Full-spectrum | Gentle high-pass at 60Hz (leave sub-bass room for ambiance), never compressed in-engine (it is already 2003-style crushed) |

This EQ strategy ensures that even when everything is playing, the mix remains clear.

### 6.4 Spatial Positioning (Stereo Field)

The game is 2D (desktop interface), but stereo positioning creates spatial clarity:

- **UI Sounds (clicks, typing):** Centered (mono or narrow stereo)
- **Notifications:** Slight left/right offset based on which side of screen app is on (MSN usually right side = notification panned 20% right)
- **Desktop Ambiance (CRT, HDD, fan):** Stereo spread (wide, enveloping)
- **LAN Party Human Presence:** Full stereo width, positioned around the player (you are sitting IN the circle of machines)
- **LAN Party Game Audio:** Slightly offset from center (feels like it is coming from other machines)
- **Music (Winamp):** Stereo, full width (player expectation for music playback)

Spatial positioning is subtle but helps with mix clarity and immersion.

---

## 7. Implementation Plan

### 7.1 Audio Middleware Choice

**Recommendation: FMOD Studio**

**Rationale:**

- LAN PARTY needs event-driven audio with state-based mixing, parameter-driven effects, and real-time ducking. FMOD excels at this.
- FMOD's snapshot system is perfect for state transitions (Desktop -> LAN Party reverb/mix shifts).
- FMOD's parameter sheets allow tying audio to game state (party energy, notification queue, time of day) without custom code.
- FMOD has excellent Unity/Unreal integration (assuming one of these engines).
- FMOD Studio's profiler is essential for debugging mix issues in a dense UI audio environment.

**Alternative (if budget is zero):** Unity's built-in audio with custom scripting. Viable but significantly more dev time for adaptive features. Not recommended unless FMOD license is prohibitive.

### 7.2 File Formats and Quality Standards

| Asset Type | Format | Sample Rate | Bit Depth | Compression | Rationale |
|---|---|---|---|---|---|
| **SFX (short, <2s)** | WAV | 48kHz | 24-bit (source) -> 16-bit (build) | PCM (uncompressed in build) | Low memory cost, need fast triggering, no latency |
| **SFX (long, 2-10s)** | WAV | 48kHz | 16-bit | PCM or light Vorbis (.ogg) if >5s | Balance quality and size |
| **Ambiance Loops** | OGG Vorbis | 48kHz | Quality 6-8 (~160-224kbps) | Compressed | Long loops, stream from disk |
| **Music** | OGG Vorbis | 48kHz | Quality 7-9 (~192-320kbps) | Compressed | Large files, stream from disk, need high quality for music fidelity |
| **Keynote Loops (HDD, CRT, fan)** | WAV | 48kHz | 16-bit | PCM | Short loops, always in memory, need seamless looping |

**Mono vs. Stereo:**

- All UI SFX (clicks, typing, beeps): **Mono** (positioned in code)
- Ambiance loops: **Stereo**
- Music: **Stereo**
- Keynote drones: **Mono** (positioned as center or stereo spread in FMOD)

**Looping:**

All loops must be **seamlessly looped** (zero-crossing match, no pops). Tools: iZotope RX for loop repair, Audacity for manual zero-crossing alignment.

### 7.3 Asset Naming Convention

Consistent naming is critical for a project with 200-400+ audio files.

**Format:** `[category]_[subcategory]_[descriptor]_[variant].wav`

**Examples:**

- `ui_click_mouse_default_01.wav`
- `ui_click_mouse_default_02.wav`
- `ui_doubleclick_01.wav`
- `app_msn_message_received_01.wav`
- `app_msn_signin_door_01.wav`
- `app_irc_channel_join_01.wav`
- `app_cdburn_complete_success_01.wav`
- `hw_hdd_seek_short_01.wav`
- `hw_hdd_seek_long_03.wav`
- `hw_crt_hum_loop.wav`
- `hw_fan_loop.wav`
- `lan_crowd_murmur_loop_med.wav`
- `lan_event_ragequit_01.wav`
- `amb_household_daytime_loop.wav`
- `amb_night_crickets_loop.wav`
- `music_electronic_downtempo_01.ogg`
- `music_rock_numetal_hype_02.ogg`

**Category Codes:**

- `ui` = Desktop interface interactions
- `app` = Application-specific sounds
- `hw` = Hardware sounds
- `lan` = LAN party phase sounds
- `amb` = Environmental ambiance
- `music` = Diegetic music tracks
- `stinger` = One-shot musical/impact moments

### 7.4 Memory Budget

**Target Platform:** PC (Steam) — memory is NOT severely constrained, but we still budget for Steam Deck (shared RAM pool, handheld optimization).

**Total Audio Memory Budget:** 150-250 MB in RAM at any time

**Breakdown:**

| Category | Count | Avg Size | Total | Load Strategy |
|---|---|---|---|---|
| UI SFX (short) | ~200 files | 50 KB | ~10 MB | All in memory (persistent) |
| Application SFX | ~100 files | 100 KB | ~10 MB | All in memory (persistent) |
| Hardware SFX | ~50 files | 80 KB | ~4 MB | All in memory (persistent) |
| Keynote Loops | ~8 files | 500 KB | ~4 MB | In memory (persistent) |
| Ambiance Loops | ~15 files | 2 MB (compressed) | Stream from disk | ~6 MB buffered |
| LAN Party Sounds | ~60 files | 150 KB | ~9 MB | Loaded on LAN party phase start, unloaded on exit |
| Music Library | ~40 tracks | 4-6 MB each | Stream from disk | ~8-10 MB buffered (1-2 tracks) |

**Total Persistent in RAM:** ~37 MB (UI, app, hardware, keynote)
**Peak RAM (LAN party active + music):** ~37 + 9 + 10 = **~56 MB**
**Streaming from disk:** Ambiance + Music (~200 MB total assets, never all loaded)

This is **well within budget** for a PC game. Optimization focus: ensure smooth streaming without stutters (pre-buffer music tracks, load LAN party assets asynchronously during party setup).

### 7.5 Integration Workflow

**Roles:**

- **Sound Designer (ECHO):** Creates all SFX, records/sources material, designs ambiance, directs music composition
- **Composer (External or ECHO):** Writes original music in period-authentic styles, delivers stems if needed for future adaptive work
- **Audio Implementer (ECHO or Engineer):** Integrates assets into FMOD, sets up events, snapshots, parameters, ducking rules, triggers
- **Engineer (Dev Team):** Hooks FMOD events to game code, passes parameters (party energy, notification count, etc.), handles state transitions

**Workflow Stages:**

1. **Pre-Production (Week 1-2):**
   - ECHO delivers this document (done)
   - Dev team confirms engine (Unity/Unreal/Godot) and FMOD integration feasibility
   - ECHO creates audio asset list (spreadsheet: every sound, priority, variant count, duration estimate)
   - Composer begins early music sketches (3-4 reference tracks for approval)

2. **Production (Week 3-10):**
   - **SFX Creation:** ECHO produces 20-30 SFX per week, delivers in batches organized by category
   - **Music Production:** Composer delivers 5-8 tracks per milestone, iterates based on feedback
   - **Temp Audio:** Dev team uses temp SFX (free libraries) to prototype core loop, validate triggers
   - **Early Integration:** ECHO integrates first batch (UI sounds) into FMOD, tests in build

3. **Implementation (Week 8-12):**
   - ECHO builds FMOD project: events, snapshots, ducking rules, parameter mappings
   - Engineer integrates FMOD events into game code, connects parameters
   - Iterative testing: ECHO plays build, identifies issues (sounds not triggering, ducking too aggressive, mix unclear), fixes in FMOD
   - Music integration: all tracks imported, Winamp system functional

4. **Mix and Polish (Week 13-15):**
   - Full playthrough with dev build, ECHO takes notes on every mix issue
   - Snapshot tuning: adjust state transition curves, reverb blends, volume levels
   - Accessibility pass: test with CRT hum disabled (15kHz+ might be painful for some), add audio options (SFX, music, ambiance volume sliders)
   - Final mix balance: ensure 30-second loop, 5-minute loop, and session loop all feel good

5. **QA and Bug Fixing (Week 16+):**
   - Audio-specific QA: test all triggers, all variants, all transitions
   - Bug triage: missing sounds, incorrect triggers, pops/clicks, ducking errors
   - Performance testing: verify streaming does not stutter, memory does not leak
   - Platform-specific testing: Steam Deck audio (different speakers, possible frequency response issues)

### 7.6 Testing Approach

Audio testing is NOT just "does it play?" It is "does it FEEL right?"

**Test Plan:**

1. **Trigger Validation (Technical):**
   - Every SFX must trigger when expected, every time
   - No double-triggers (same sound twice in <50ms)
   - No missing sounds (silent events)
   - Tool: FMOD profiler to track event firing

2. **Variation Coverage (Repetition Test):**
   - Play core loop for 30 minutes, listen for repetition fatigue
   - If any sound becomes annoying, add more variants or adjust trigger frequency
   - Target: no sound should feel "samey" within a 5-minute window

3. **Mix Clarity (Hierarchy Test):**
   - Create stress test scenario: 10 notifications arrive simultaneously, download completes, MSN signs in, player is typing
   - Can the player still identify each event? If not, adjust ducking rules or EQ separation
   - Priority tier 1 events should ALWAYS be audible

4. **State Transition Smoothness (Flow Test):**
   - Transition from Desktop -> LAN Party -> Desktop repeatedly
   - Listen for pops, clicks, abrupt cuts, reverb tails cutting off
   - Ensure emotional smoothness (transition should feel like moving through space, not jumping between presets)

5. **Emotional Resonance (Playtest):**
   - External playtesters (not dev team) play for 2 hours
   - Interview after: "Did any sound break immersion?" "Did the LAN party feel alive?" "Did you notice the CRT hum?" "Did the music fit?"
   - Qualitative data, not quantitative. We are testing FEEL.

6. **Accessibility Test:**
   - Test with all volume sliders at extremes (SFX only, music only, ambiance only)
   - Test with CRT hum disabled (accessibility option)
   - Test with colorblind-friendly UI (audio must convey information that color alone might not)

7. **Performance Test:**
   - Monitor CPU usage of FMOD playback (should be <5%)
   - Monitor memory usage (should stay within budget)
   - Test on min-spec PC and Steam Deck — no audio stutters, no streaming gaps

**Bug Severity Scale:**

- **Critical:** Audio completely missing, game-breaking audio bug, crash caused by audio system
- **High:** Key SFX not triggering (e.g., MSN message silent), ducking not working, mix hierarchy broken
- **Medium:** Wrong sound playing, variant distribution uneven, minor pops/clicks
- **Low:** Cosmetic (e.g., one variant sounds slightly different than others but still functional)

### 7.7 Audio Options Menu (Player-Facing)

Players must have control. Minimum required options:

- **Master Volume** (0-100%)
- **SFX Volume** (0-100%) — affects all UI and app sounds
- **Music Volume** (0-100%) — affects Winamp playback
- **Ambiance Volume** (0-100%) — affects keynote, room tone, crowd murmur
- **CRT Hum Toggle** (On/Off) — accessibility for tinnitus sufferers or high-frequency sensitivity
- **Spatial Audio Toggle** (On/Off) — stereo vs. mono (accessibility for hearing impairment)

**Advanced (Optional):**

- **Dynamic Range** (Compressed / Normal / Wide) — adjusts overall mix limiting for different listening environments (headphones vs. speakers)
- **Subtitle Cues for SFX** (On/Off) — displays "[MSN Message Received]" text for accessibility

---

## 8. Final Notes — ECHO's Perspective

This document is a blueprint, not a prison. Audio design is iterative. Sounds that look perfect on paper might feel wrong in the game. The 30-second loop might need different sounds at hour 1 vs. hour 20. The LAN party ambiance might need to be 20% quieter or 40% louder — we will not know until we hear it in context.

But here is what I know for certain:

**LAN PARTY lives or dies on whether the desktop feels ALIVE.** Not like a UI. Like a space. A place where things happen. Where the CRT hums because it is on. Where the hard drive clicks because it is thinking. Where your friends knock on the door of your MSN messenger and you HEAR them arrive.

The player must hear the difference between a bustling LAN party and an empty basement after everyone has gone home. They must hear the passage of time in the way their hard drive fills with downloaded games, in the way the crowd murmur changes from excited to tired, in the silence after the last "door close" sound when a friend signs off for the last time.

Audio is not polish. Audio IS the game feel. Take the sound away and LAN PARTY becomes a spreadsheet with a nostalgia skin. Leave the sound in — get it right — and the player will close their eyes and be 16 years old again, sitting in a basement that smells like Mountain Dew and burned CDs, surrounded by people who mattered.

That is the frequency we are tuning for.

Close your eyes. What do you hear?

A world.

---

**Document Complete**
**Word Count:** 9,247
**Status:** Ready for Review and Production**
**Next Steps:** Asset list creation, composer onboarding, FMOD project initialization, vertical slice audio integration**

*— ECHO, Sound Designer*
*"Listen to the space between."*
