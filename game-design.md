# LAN PARTY -- Game Design Document

**Designer:** REED
**Status:** First Pass -- Ready for Internal Review
**Pitch Reference:** `games/04-lan-party/pitch.md`
**Target Platform:** PC (Steam), Steam Deck secondary
**Genre:** Management Simulation / Social Simulation / Nostalgic Desktop Interface
**Target Session Length:** 30--60 minutes
**Audience:** Adults 28--42 (primary), 18--27 nostalgia-adjacent (secondary), management sim enthusiasts (tertiary)

---

## 1. Player Fantasy

### Fantasy Statement

**"I am the person everyone turns to. I have the basement, the bandwidth, and the burned CDs. I hold this community together with cable management and chat windows -- and the thing I'm building matters more than I realize."**

This is not a power fantasy about domination. It is a *belonging* fantasy about orchestration. The player wants to feel like the indispensable center of a social world that could not exist without them. They want to feel the specific cocktail of pride, stress, and warmth that comes from hosting -- from being the person whose house everyone comes to, whose desktop has the goods, whose MSN status is always Online.

What's the loop? The loop is caretaking disguised as logistics. Every file you download, every seating chart you arrange, every conversation you navigate -- it all serves one emotional function: making people show up and making them want to come back.

The secondary fantasy is *curator*. You choose which games get played. You build the playlist. You decide who sits next to whom. You are the DJ, the bouncer, and the bartender of a scene that only exists because you keep building it.

The tertiary fantasy is *nostalgia as gameplay*. The desktop is not a menu. The desktop is the toy. Clicking through WinXP, hearing the AIM door sound, watching a download bar crawl -- these are not loading screens. They are the game.

---

## 2. Core Loop Architecture

### 2.1 The 30-Second Loop: Click, Read, Decide

```
 +------------------+
 |  NOTIFICATION    |  <-- MSN message, IRC ping, download complete,
 |  (stimulus)      |      forum reply, system alert
 +--------+---------+
          |
          v
 +------------------+
 |  OPEN APP        |  <-- Player clicks to the relevant window
 |  (navigate)      |      (MSN, mIRC, browser, file manager)
 +--------+---------+
          |
          v
 +------------------+
 |  READ CONTEXT    |  <-- Scan the message, the download status,
 |  (assess)        |      the forum thread, the buddy list
 +--------+---------+
          |
          v
 +------------------+
 |  MAKE A CHOICE   |  <-- Reply (tone matters), ignore, redirect,
 |  (act)           |      download, delete, configure
 +--------+---------+
          |
          v
 +------------------+
 |  SEE FEEDBACK    |  <-- Relationship shift, rep change, file acquired,
 |  (reward/cost)   |      risk flag, mood shift in NPC
 +------------------+
          |
          +-------> loops back to NOTIFICATION
```

**Player verb:** TRIAGE. The desktop is a stream of competing demands. The player's moment-to-moment skill is prioritization. Which window do I answer first? What can wait? What's urgent? This is the *Papers, Please* muscle -- many small decisions, each with invisible downstream consequences.

**Feel target:** The feel is "busy but in control." Like running a good shift at a restaurant. The player should always have 2--3 open threads and feel clever when they resolve them efficiently.

### 2.2 The 5-Minute Loop: LAN Party Prep Cycle

```
 +-----------+     +-----------+     +-----------+     +-----------+
 |  ACQUIRE  |---->|  RECRUIT  |---->|  PREPARE  |---->|  RESOLVE  |
 |  (games)  |     |  (people) |     |  (setup)  |     |  (drama)  |
 +-----+-----+     +-----+-----+     +-----+-----+     +-----+-----+
       |                 |                 |                 |
       v                 v                 v                 v
   Download,         Message friends,  Assign hardware,  Mediate fights,
   verify rips,      manage RSVPs,     burn CDs, test    handle excuses,
   assess risk,      convince the      network config,   adjust plans
   store/organize    reluctant ones    pick game lineup  around no-shows
       |                 |                 |                 |
       +--------+--------+--------+--------+                |
                |                                            |
                v                                            |
         +------+------+                                     |
         |  LAN PARTY  |<-----------------------------------+
         |  (execute)  |
         +-------------+
```

Each prep phase is a mini-game of resource management conducted entirely through desktop applications:

- **ACQUIRE** uses mIRC channels, P2P clients, and scene contacts. The player verb is *sourcing*. Risk is the primary tension.
- **RECRUIT** uses MSN Messenger and forum posts. The player verb is *persuading*. Social dynamics are the primary tension.
- **PREPARE** uses the file manager, CD burner, and a hardware inventory notepad. The player verb is *organizing*. Logistics are the primary tension.
- **RESOLVE** uses all communication tools. The player verb is *mediating*. Drama is the primary tension -- someone always threatens to bail.

How does this feel at hour 20? At hour 20, the player is juggling multiple prep cycles with overlapping timelines. They have a party this weekend but are already seeding contacts for the one after. Two crew members are feuding. A download is corrupted and the backup source is on a private tracker they do not have ratio on yet. The 5-minute loop at hour 20 feels like spinning plates -- each plate a different app window.

### 2.3 The Session Loop: Host, Experience, Aftermath (30--60 Minutes)

```
 +------------------+       +------------------+       +------------------+
 |  DESKTOP PHASE   |------>|  LAN PARTY PHASE |------>|  AFTERMATH PHASE |
 |  (prep, 15-25m)  |       |  (event, 8-15m)  |       |  (fallout, 7-15m)|
 +------------------+       +------------------+       +------------------+
        ^                                                       |
        |                                                       |
        +-------------------------------------------------------+
                          (new week begins)
```

**DESKTOP PHASE (60% of playtime):** The player lives on their simulated desktop. Messages arrive. Downloads run. Forum threads evolve. The player preps for the next LAN party while managing the social ecosystem. Time passes in soft real-time with a clock in the system tray (speed controllable -- 1x, 2x, 4x, pause). Events are time-gated: IRC channels are busier at night, friends message after school, forum drama brews over days.

**LAN PARTY PHASE (25% of playtime):** The party happens. The perspective shifts -- the player's desktop now shows the game being played (a simplified, watchable mini-game), plus an MSN-style side chat where AI characters react in real time. The player can intervene: swap games if the energy is dying, address a fight, troubleshoot a crash. This phase is partially automated -- the AI characters play and interact -- but the player's prep determines the quality. Bad game rip? Crash. Wrong seating chart? Fight. No snacks? Morale death spiral.

**AFTERMATH PHASE (15% of playtime):** The party ends. Characters go home. The next morning, MSN statuses update. Forum posts appear -- recaps, inside jokes, complaints. The player reads the fallout and begins the next prep cycle. Relationships have shifted. Reputation has changed. New opportunities or crises have emerged from the party's events.

### 2.4 The Meta Loop: Season Arc

```
  MONTH 1          MONTH 2-3        MONTH 4-6         MONTH 7-9         MONTH 10-12
 +---------+     +-----------+     +-----------+     +-------------+     +----------+
 | GENESIS |---->|  GROWTH   |---->|  GOLDEN   |---->|  FRACTURE   |---->|  FINALE  |
 | 3 crew  |     |  8 crew   |     | 12+ crew  |     | Splits form |     | Last LAN |
 | 1st LAN |     |  Rep rises|     | Peak scene|     | People leave|     | Epilogue |
 +---------+     +-----------+     +-----------+     +-------------+     +----------+
```

A full playthrough spans roughly one in-game year (approximately 15--25 real-world hours depending on play speed). The meta loop tracks the lifecycle of a community -- formation, growth, peak, decline, and a final gathering. This arc is not scripted beat-by-beat but is driven by systemic pressures: characters have life events (moving away, getting jobs, losing interest) that probabilistically trigger based on timeline and relationship states. The player can delay decline through effort but cannot prevent it entirely.

The meta loop answers: how does this feel at hour 20? At hour 20, the player is deep in the Golden or Fracture phase. They have built something real. Losing a crew member stings because the AI has been generating 15 hours of personalized chat history. The question shifts from "how do I grow?" to "how do I hold on?"

---

## 3. Core Mechanics -- Detailed Breakdown

### 3.1 Desktop Simulation

**Player verb:** NAVIGATE, CLICK, ORGANIZE
**System description:** The entire game interface is a pixel-accurate simulation of a Windows XP-era desktop. There is no HUD, no traditional game menu, no health bar. Every game system is embedded inside a desktop application. The taskbar is the player's navigation. The system tray is their notification center. The desktop icons are their toolset.

**Applications as game systems:**

| Application | Game System | Primary Function |
|---|---|---|
| MSN Messenger | Relationship Manager | 1-on-1 conversations with AI characters, status tracking, group invites |
| mIRC | Acquisition Pipeline | Channel browsing, warez sourcing, scene reputation, DCC transfers |
| Forum Client (phpBB-style) | Reputation Tracker | Public posts, community sentiment, drama management, event announcements |
| File Manager (Explorer) | Inventory System | Downloaded files, CD images, hardware configs, storage management |
| CD Burner (Nero-style) | Crafting System | Burn ISOs to virtual CDs, compilation discs, mixtapes |
| Winamp | Mood/Atmosphere System | Playlist affects party mood, characters have music preferences, mixtape sharing |
| Notepad | Planning Tool | Free-form notes, to-do lists, seating charts, hardware inventory |
| P2P Client (Kazaa-style) | High-Risk Acquisition | Fast but dangerous downloads, malware risk, ISP flags |
| Web Browser (IE-style) | World Window | Gaming news sites, GeoCities pages, character homepages, hardware reviews |
| WinRAR | File Processing | Extract archives, verify integrity, handle split RARs (r01, r02...) |
| System Tray Clock | Time Management | Current time, day, speed controls, upcoming event reminders |

**Feedback:** Every app has period-authentic sound effects. MSN message *nudge*. mIRC join/part sounds. Download completion chime. CD burn progress bar. The desktop accumulates clutter over time -- more icons, more files, more open windows -- mirroring the player's growing empire.

**Depth:** Mastery of the desktop is spatial and procedural. Expert players have mental models of which app handles which problem. They alt-tab instinctively. They know where their files are. The desktop becomes an extension of their brain, just like a real power user's desktop in 2003.

### 3.2 Community Management (AI Character System)

**Player verb:** TALK, LISTEN, MEDIATE, INVITE, IGNORE
**System description:** Each AI character is a persistent agent with the following state model:

**Character State Model:**

- **Personality Traits** (fixed per playthrough): 5-axis model -- Sociability, Competitiveness, Loyalty, Patience, Boldness. Generated at character creation, determines behavioral tendencies.
- **Mood** (volatile, changes hourly): Float value -100 to +100, influenced by recent events, conversations, game outcomes, social status.
- **Relationships** (persistent, slow-changing): Pairwise relationship values between all characters, including the player. Range -100 to +100. Modified by direct interaction, gossip, shared experiences, and betrayal.
- **Desires** (rotate weekly): Each character has 1--3 active desires at any time: "wants to play CounterOps," "wants to be invited to the next LAN," "wants to resolve fight with xXDarkAngelXx," "wants recognition on the forum." Fulfilled desires boost mood and relationship. Ignored desires decay mood and can trigger drama.
- **Life Events** (probabilistic, timeline-gated): Job offer, family move, girlfriend/boyfriend, new hobby, academic pressure. These introduce external pressure that the player cannot control, only respond to.
- **Online Presence Pattern** (persistent): Each character has a schedule -- when they are Online, Away, or Offline on MSN. This pattern shifts based on life events and mood. A character going increasingly Offline is a warning sign.

**Feedback:** The player sees all of this through natural interfaces. Mood is expressed through chat tone, away messages, and forum posting frequency. Relationships are visible through who talks to whom, who sits together at LAN parties, who defends whom in forum arguments. Desires surface as direct requests ("hey can we play UnrealBattle next time?") or indirect hints ("man, nobody ever picks MY game...").

**Depth:** Where's the depth? The depth is in reading the room through text. An expert player notices that ShadowLurker's away message changed from a Slipknot lyric to "..." three days ago, cross-references that with the forum argument they had with N00bMaster last week, and proactively reaches out before the situation escalates. The game never tells you someone is upset -- you have to notice, like a real friend would.

### 3.3 Acquisition and Risk

**Player verb:** SEARCH, DOWNLOAD, VERIFY, DISTRIBUTE
**System description:** Games are the primary resource. You need them for LAN parties. Acquiring them is a multi-step process with escalating risk/reward:

**Acquisition Channels:**

| Channel | Access Requirement | Speed | Risk Level | Quality |
|---|---|---|---|---|
| P2P (Kazaa-style) | None | Fast | Very High | Low (malware, bad rips, fake files) |
| Public IRC Channels | Basic IRC knowledge | Medium | High | Medium |
| Private Trackers | Invitation + ratio maintenance | Medium | Medium | High |
| Scene Contacts | High reputation + trust | Slow | Low | Very High (pre-release, clean rips) |
| Legitimate Purchase | Money (scarce resource) | Instant | None | Perfect |

**Risk System:** Every illegitimate acquisition carries risk expressed through three threat vectors:

1. **Malware Risk** (per-file): Bad downloads can infect the simulated desktop. Effects range from annoying pop-ups to corrupted game files to losing save data. Scanning with a simulated antivirus mitigates this. Quality of source determines base malware probability.
2. **ISP Flag Risk** (cumulative): A hidden "heat" meter tracks overall piracy activity. Thresholds trigger escalating consequences: throttled download speeds, warning email from ISP, temporary internet outage, parental notification (social catastrophe). Heat decays slowly over time. Legitimate purchases and low-risk sources generate less heat.
3. **Social Risk** (contextual): Distributing bad rips damages reputation. Getting caught with pre-release content draws scene attention (good and bad). If a LAN party game crashes because of a bad rip, every attendee's opinion of you drops.

**File Verification Loop:** Downloaded files are not automatically usable. The player must: extract archives (WinRAR), verify file integrity (checksums in NFO files), mount or burn ISOs (CD burner), and test-run the game. Each step can reveal problems. A split RAR with a missing part. A keygen that is actually malware. An ISO that is 50MB too small (bad rip). This verification process is a mini-puzzle that rewards attention to detail.

**Feedback:** Download progress bars, file sizes, NFO file ASCII art (procedurally generated, a pure nostalgia hit), IRC channel reputation systems, ratio trackers on private sites.

**Depth:** At hour 20, the player has a network of sources, a curated library, and a reputation to protect. They know which IRC channels are reliable. They have cultivated a scene contact who sometimes shares pre-release material. The acquisition system has evolved from "find any copy of the game" to "maintain a supply chain of high-quality content while managing risk across multiple channels."

### 3.4 LAN Party Hosting

**Player verb:** PLAN, SETUP, MANAGE, TROUBLESHOOT
**System description:** The LAN party is the climactic event of each session cycle. It has four sub-phases:

**PLANNING (Desktop Phase):**
- Select games (from acquired library). Match games to crew preferences. Mix competitive and cooperative.
- Invite attendees (via MSN). Manage RSVPs. Navigate social dynamics -- inviting rival crew members creates tension; excluding someone creates resentment.
- Assign hardware (from inventory). Match system requirements to available rigs. Borrow equipment from crew members (social cost). Overclock for performance (hardware risk).
- Set atmosphere: Winamp playlist, snack planning (yes, snacks are a real system -- see section 3.5).

**SETUP (Transition Phase):**
- A brief sequence where the player configures the LAN environment. Network topology matters: daisy-chaining hubs vs. a proper switch. Cable routing. IP assignment (DHCP or manual -- manual is faster but error-prone).
- Hardware failures can occur based on equipment quality. A borrowed CRT might flicker. An overclocked CPU might crash under load.

**EXECUTION (LAN Party Phase):**
- AI characters arrive (or don't -- no-shows based on mood, weather, life events).
- Games are played. The player observes via a simplified top-down view of the game (stylized, not a full game-within-a-game) and the real-time chat sidebar.
- Events trigger: someone accuses another of screen-looking, someone rage-quits, two people who were feuding bond over a clutch play, hardware crashes, network lag.
- Player interventions: swap to a different game, mediate a dispute, troubleshoot a technical problem, call a snack break, adjust seating.
- Party energy is tracked as a visible meter. High energy = memorable party. Low energy = people leave early.

**AFTERMATH (Desktop Phase):**
- Characters go home. Relationship changes are applied based on party events.
- Forum posts appear: highlight reels, complaints, inside jokes.
- MSN conversations the next day process the emotional fallout.
- Reputation changes based on party quality.

**Party Quality Score** is determined by:

| Factor | Weight | Description |
|---|---|---|
| Game Selection Match | 25% | Did the games match crew preferences? |
| Hardware Stability | 20% | How many crashes/lag spikes occurred? |
| Social Harmony | 25% | Were conflicts managed? Did bonding moments happen? |
| Atmosphere | 15% | Playlist quality, snack availability, novelty factor |
| Surprise Factor | 15% | New game nobody expected, a new attendee, a tournament bracket |

### 3.5 The Snack System

This is not a joke. Snacks are a real, designed system. They represent the physical, embodied reality of hosting -- the thing that separates a LAN party from just playing online.

**Player verb:** STOCK, SERVE
**System description:** Before each LAN party, the player allocates a snack budget (from limited weekly allowance). Snack categories: Drinks (caffeine = energy boost, sugar crash later), Chips/Savory (baseline morale), Pizza (major morale spike, expensive, timing matters -- too early = cold by round 3), Candy (sugar rush = short energy spike), and Homemade (highest morale, requires prep time, specific characters react strongly).

Snacks affect the Party Energy meter. Running out of snacks mid-party triggers a morale dip. Specific characters have preferences ("FragMaster42 HATES Mountain Dew, only drinks Bawls"). Remembering these preferences is a relationship deepener that the game never explicitly tells you to track.

### 3.6 Reputation and Progression

**Player verb:** EARN, MAINTAIN, LEVERAGE
**System description:** The player has reputation scores in four overlapping communities:

| Community | Tracked Via | Reputation Currency | Unlocks |
|---|---|---|---|
| Friend Group | MSN + LAN parties | Trust | Deeper conversations, favors, hardware loans, loyalty during crises |
| Forum | Forum posts + events | Clout | Moderator status, ability to organize public events, influence over community opinion |
| IRC Channels | Channel activity + sharing | Cred | Access to better channels, invitations to private groups, faster DCC transfers |
| Warez Scene | Quality of contributions + discretion | Street Rep | Scene contact relationships, pre-release access, invitation to top-tier groups |

Reputation in each community operates on a 0--100 scale with decay. Inactivity in any community causes slow reputation loss. This creates the core tension of time management: the player cannot max all four simultaneously. Specializing in warez scene reputation gives access to the best content but requires time away from friend group maintenance, which can cause social decay.

---

## 4. Systems Interaction Map

```
                    +------------------+
                    |  DESKTOP SIM     |
                    |  (hub system)    |
                    +--------+---------+
                             |
            +----------------+----------------+
            |                |                |
            v                v                v
    +-------+------+  +-----+-------+  +-----+--------+
    |  COMMUNITY   |  | ACQUISITION |  |  REPUTATION  |
    |  MANAGEMENT  |  | & RISK      |  |  SYSTEM      |
    +-------+------+  +------+------+  +------+-------+
            |                |                |
            +-------+--------+--------+-------+
                    |                 |
                    v                 v
            +-------+------+  +------+--------+
            |  LAN PARTY   |  |  PROGRESSION  |
            |  HOSTING     |  |  (meta arc)   |
            +--------------+  +---------------+
```

### Positive Feedback Loops (Snowball Effects)

1. **Good parties attract more crew, more crew unlock better parties.** A successful LAN party boosts reputation, which attracts new potential crew members, which allows larger parties, which creates more social content, which boosts reputation further. This is the engine of the Growth phase.

2. **High warez rep unlocks better content, better content makes better parties.** Scene access provides clean, early rips. These impress the crew. Impressed crew talks you up on forums. Forum clout attracts scene attention. Cycle accelerates.

3. **Strong relationships yield favors, favors reduce friction.** A friend with high trust lends hardware. Borrowed hardware enables more attendees. More attendees build stronger relationships with more people. Network effect.

### Negative Feedback Loops (Balancing Forces)

1. **Crew size increases drama exponentially.** Every new member adds N-1 new relationship edges to the social graph. More people = more conflicts = more mediation time = less time for acquisition and prep. Growth has a natural ceiling imposed by social management cost.

2. **Piracy heat accumulates with success.** The better your library, the more you downloaded to build it. High heat means ISP consequences that threaten the entire operation. Success paints a target.

3. **Reputation decay forces active maintenance.** You cannot rest. Ignoring any community causes slow decay. This prevents the player from fully snowballing in one direction and forces constant re-engagement with all systems.

4. **Character life events inject uncontrollable entropy.** No amount of optimization prevents a core crew member from getting a girlfriend and going from "Online" to "Appear Offline" for two weeks. The game pushes back against total control.

### Emergent Possibilities

- A player discovers that two crew members with low mutual relationship but high competitiveness create the best LAN party energy when placed on opposing teams. They start engineering rivalries.
- A player realizes that burning mixtape CDs and distributing them via MSN file transfer is the most efficient relationship-building tool per time invested.
- A crew member who has been drifting (life event: new job) is pulled back by a perfectly chosen game selection that hits their specific nostalgia.
- An ISP scare causes the player to pivot to legitimate purchases, which changes their scene reputation but stabilizes their operation -- a genuine strategic pivot.

---

## 5. Progression Curves

### 5.1 Skill Progression (Player Knowledge)

The player learns in layers:

**Layer 1 (Hours 0--3): Interface Literacy.** Where things are. How apps work. Basic flow of message-respond-acquire-host. The desktop is novel and discovery-driven.

**Layer 2 (Hours 3--8): System Awareness.** Understanding that reputation has four axes. Noticing that character mood affects party outcomes. Starting to plan ahead instead of react. First experience of a party going wrong due to poor prep.

**Layer 3 (Hours 8--15): Strategic Optimization.** Actively managing risk/reward in acquisition. Engineering social dynamics. Reading character emotional states through indirect signals. Planning two parties ahead. Understanding trade-offs between community investment paths.

**Layer 4 (Hours 15--25): Mastery and Acceptance.** Knowing that total control is impossible. Accepting loss as part of the arc. Finding satisfaction in the quality of a single party rather than infinite growth. Reading the meta-arc and making peace with the finale.

### 5.2 Content Progression (Unlocked Systems and Complexity)

| In-Game Week | New System / Complexity Layer |
|---|---|
| Week 1 | Desktop basics, MSN, 3 initial contacts, first simple download |
| Week 2 | Forum access, first LAN party (3 people, 1 game), snack system |
| Week 3 | mIRC basics, public channels, more contacts appear organically |
| Week 4 | First drama event (two characters conflict), mediation mechanics |
| Week 5 | Private tracker invitation (ratio system), CD burner unlocked |
| Week 6-7 | Larger parties (6-8 people), hardware management, seating matters |
| Week 8 | Scene contact introduction, first high-value/high-risk acquisition |
| Week 10 | Community splits possible, moderator responsibilities on forum |
| Week 12+ | Tournament hosting, 10+ person events, full system mastery required |
| Week 16+ | Fracture phase begins, life events accelerate, focus shifts to retention |
| Week 20+ | Finale arc, last LAN party planning |

### 5.3 Difficulty Curve

The difficulty curve is **stepped with organic escalation**, not smooth. Each step corresponds to a new system introduction or a complexity spike from existing systems interacting in new ways.

```
Difficulty
    |
    |                                              ****
    |                                         ****
    |                                    *****
    |                              ******
    |                         *****
    |                   ******
    |              *****
    |         *****
    |    ****
    |****
    +-----------------------------------------> Time
    Wk1   Wk4    Wk8    Wk12   Wk16   Wk20

    Genesis | Growth  | Golden  | Fracture | Finale
```

Difficulty is not enemy scaling. It is complexity scaling. More characters, more simultaneous demands, more conflicting desires, more risk from accumulated heat, more emotional weight in decisions. The game gets harder because the player cares more and has more to lose, not because numbers get bigger.

---

## 6. Economy Design

### 6.1 Resource Currencies

| Currency | Source | Sink | Scarcity Driver |
|---|---|---|---|
| Time (in-game hours) | Passage of days | Every action | Hard cap per day; speed controls let you skip but not create time |
| Money (allowance/odd jobs) | Weekly allowance, odd jobs from forum | Legitimate game purchases, hardware, snacks, blank CDs | Low income, many competing demands |
| Storage (hard drive space) | Starting HDD, upgradable | Downloaded files, installed games, saved ISOs | Physical limit, must manage and delete |
| Bandwidth | ISP plan, upgradable | Downloads, uploads (ratio maintenance) | Shared with household (congestion at peak hours) |
| Blank CDs | Purchased with money | Burning games, mixtapes | Consumable, cannot be recovered once burned |
| Social Energy (implicit) | Regenerates daily | Every conversation, every mediation, every forum post | Represents the player's own patience; too many interactions per day reduces response quality options |

### 6.2 Economy Tension Design

The economy is designed around **three-way resource conflicts** that force meaningful choice:

**Money vs. Risk:** You can buy games legitimately (safe, expensive) or pirate them (free, risky). The economy ensures you cannot afford to buy everything, so piracy is not a moral choice -- it is a resource management choice. But every pirated game adds heat.

**Time vs. Breadth:** Maintaining four reputation tracks takes time. Maintaining relationships takes time. Downloading takes time. The player never has enough hours in a day. This scarcity is what makes the 30-second triage loop matter -- every minute spent in mIRC is a minute not spent on MSN.

**Storage vs. Library:** Hard drive space is physically limited (period-authentic: think 40GB). Games are 600MB--4GB each. The player must curate their library, deleting old games to make room for new ones. But old games have social value -- a crew member might request something from months ago. Storage management is collection management.

### 6.3 Inflationary Pressures and Sinks

The economy must avoid two failure states: **abundance** (player has everything, nothing matters) and **starvation** (player cannot do anything, game stalls).

**Anti-abundance mechanisms:**
- Hardware degrades over time (needs replacement/repair, costs money)
- Reputation decays in all four tracks
- Crew size increases demand for content variety
- Heat accumulation makes piracy increasingly costly
- Life events remove crew members regardless of player investment

**Anti-starvation mechanisms:**
- Fallback free games always available (low quality, everyone has played them, but functional)
- At least 2--3 crew members are always reliable regardless of drama state
- Odd jobs scale slightly with need (the game notices if you are broke for multiple weeks)
- Public IRC channels always accessible, even without reputation
- Small parties (3--4 people) are always viable with minimal resources

---

## 7. Difficulty and Balance Framework

### 7.1 Time Model: Soft Real-Time with Speed Controls

The game uses **soft real-time** with player-controlled time speed (1x, 2x, 4x, pause). This is the Rimworld model, not the Papers Please model. The reason: the emotional core requires characters to message you unprompted, for forum threads to evolve organically, and for time pressure to feel like time pressure. Action-triggered time (Papers, Please) would make the desktop feel like a task queue instead of a living world.

**Pause is always available.** The player can pause to read, think, and plan. Time speed affects only the passage of in-game hours, not the player's ability to process information. This is critical for accessibility and for the "cozy" feel target -- stress should come from prioritization, not from reflex speed.

### 7.2 Difficulty Settings: Vibe Selection

Rather than traditional Easy/Medium/Hard, difficulty is framed as **"What kind of experience do you want?"**

| Setting | Name | Mechanical Effect |
|---|---|---|
| Chill | "Summer Break" | Slower reputation decay, more forgiving risk system, characters are more patient, fewer simultaneous demands, extended meta timeline |
| Standard | "School Year" | Default tuning, full system complexity, intended experience |
| Intense | "Senior Year" | Faster decay, more aggressive character life events, tighter economy, higher social entropy, compressed timeline |

### 7.3 Balance Levers

These are the primary variables the design team tunes during playtesting:

1. **Message frequency per hour:** How many notifications arrive per in-game hour at each game phase? Too many = overwhelming. Too few = boring. Target: 3--5 at Genesis, 8--12 at Golden, 6--8 at Fracture (declining but higher stakes).

2. **Reputation decay rate per community:** How fast does inactivity cost you? This controls how many plates the player must spin. Tuned per difficulty setting.

3. **ISP heat thresholds:** At what cumulative risk level do consequences trigger? These thresholds determine how much piracy the player can sustain before pivoting strategies.

4. **Character mood volatility:** How quickly do characters shift mood? High volatility = more drama = more to manage. Low volatility = more predictable = less interesting. Target: moderate baseline with spikes around key events.

5. **Party quality factor weights:** The 5-factor party quality formula (section 3.4) can be reweighted to emphasize different player skills.

6. **Life event probability curve:** When and how often do characters experience life events that pull them away? This curve shapes the entire meta arc.

7. **Economy income vs. drain ratio:** Weekly allowance vs. cost of goods. This ratio determines whether the player feels resourceful or desperate.

### 7.4 Anti-Frustration Design

- **No permafail.** A terrible LAN party is a setback, not a game over. The community survives bad parties. The game is about recovery and adaptation.
- **Transparent-ish consequences.** The game does not tell the player "ShadowLurker's relationship dropped by 12 points." But it does show ShadowLurker's MSN status change to "whatever..." -- and a player paying attention learns to read these signals. Consequences are always *communicable* through the interface even if not numerically exposed.
- **Second chances for relationships.** Characters who drift can be pulled back with effort. No relationship is permanently destroyed by a single mistake (unless the mistake is egregious -- like sharing someone's private message publicly).
- **Graceful crew attrition.** When characters leave (life events), new potential crew members appear. The community changes but does not die. The player always has someone to host for.

---

## 8. Risk Assessment

### 8.1 Design Risks

| Risk | Severity | Likelihood | Mitigation |
|---|---|---|---|
| **Desktop sim feels tedious, not nostalgic** -- clicking through XP menus loses charm after hour 2 | Critical | Medium | Streamline interactions aggressively. Hotkeys for power users. Never require more than 3 clicks for a common action. The charm is in the *presence* of the desktop, not in the *friction* of it. Playtest for tedium at hour 5. |
| **AI characters feel robotic or repetitive** -- generated text breaks immersion | Critical | High | Invest heavily in per-character voice models. Use constrained generation (templates + fills) rather than fully open generation. Each character has a writing style guide. Playtest with focus on "did any message break immersion?" |
| **Players do not understand indirect feedback** -- relationship/mood changes go unnoticed | High | Medium | Subtle tutorial: early game, a character explicitly tells you "hey, I noticed you didn't reply to my message yesterday, what's up?" Teaching moment that this game tracks your behavior. Tooltip system on mouse-over of buddy list entries (shows mood hint in later game). |
| **LAN party phase is passive and boring** -- watching AI play is not engaging | High | Medium | Player must make 3--5 active decisions per party. Intervention points are clearly signaled. Party duration is short enough (8--15 real minutes) that it never overstays. If playtesting reveals passivity, add more player verbs (call plays, manage team composition mid-match). |
| **Piracy theme creates store/publisher friction** -- Steam/console platforms may object | Medium | Medium | Frame piracy as period-authentic, not endorsement. Consequences for piracy are real and escalating. The narrative frames the era as morally complex, not aspirational. Consult platform TOS early. Precedent: Hypnospace Outlaw handled piracy themes successfully. |
| **Session length exceeds target** -- players cannot find stopping points | Medium | High | Enforce natural stopping points at the end of each session loop (after aftermath phase). Auto-save at session boundaries. Desktop clock shows a clear "end of week" marker. Time speed controls allow compression of low-activity periods. |
| **Meta arc feels predetermined** -- player feels railroaded toward inevitable decline | Medium | Medium | Decline is systemic, not scripted. The player CAN delay it significantly through excellent play. Some playthroughs can end with a strong community intact, just smaller. The "last LAN party" is bittersweet, not tragic. Vary endings based on player choices throughout. |
| **Economy is too tight or too loose** -- player is either broke or swimming in resources | Medium | High | Extensive playtesting with telemetry on resource levels at each game phase. Dynamic safety valves: odd job availability scales with need. Tuning spreadsheet for all economic variables accessible to design team. |

### 8.2 Technical Risks

| Risk | Severity | Mitigation |
|---|---|---|
| AI text generation latency breaks real-time feel | High | Pre-generate message queues. Characters "type" for a realistic delay (the typing indicator IS the loading screen). Batch generation during time-speed transitions. |
| Desktop simulation performance on low-end hardware | Medium | The sim is 2D with minimal shader work. Optimize window rendering. Lazy-load application contents. The XP aesthetic is inherently low-fi -- leverage this. |
| Save state complexity (hundreds of relationship values, message histories, file states) | Medium | Serialize aggressively. Auto-save per in-game day. Keep message history capped at N messages per character with summarization for older history. |

---

## 9. Open Playtesting Questions

These are the questions I want answered with controllers in players' hands. No amount of theorycrafting substitutes for observation.

### Priority 1: Core Loop Validation

1. **Is the 30-second triage loop fun in isolation?** Build a vertical slice: 5 characters messaging simultaneously, one download running, one forum thread evolving. Can the player juggle? Do they want to? Does the prioritization feel like a skill or a chore?

2. **Does the desktop charm sustain past hour 3?** Track the exact moment players stop exploring the desktop and start treating it as pure utility. If that moment is before hour 3, the sim needs more discoverable details. If it is after hour 5, it is fine -- utility is the goal state.

3. **Is the LAN party phase engaging or a cutscene?** Measure player input frequency during LAN parties. If players are making fewer than 2 meaningful decisions per party, the phase is too passive. If more than 8, it is too frantic and undermines the "party autopilot" feel.

### Priority 2: Emotional and Social Systems

4. **Do players form genuine attachments to AI characters?** After 5 hours of play, can the player name their crew members' personality traits without looking? Do they have a favorite? Do they feel guilt when ignoring someone's message? If not, the character system needs more distinctiveness and the feedback needs to be more emotionally legible.

5. **Is social drama engaging or annoying?** When two characters fight, does the player lean in ("oh no, what happened?") or lean back ("ugh, not again")? The difference is variety and stakes. Track drama fatigue over time.

6. **Does the Fracture phase feel earned or imposed?** When characters start drifting, does it feel like a natural consequence of the world or like the designer flipping a switch? Life events must feel organic, not timed to a script.

### Priority 3: Economy and Progression

7. **Is the risk/reward of piracy calibrated correctly?** Players should pirate frequently in early game (low heat, high need), moderate in mid-game (rising heat, better alternatives), and face real consequences in late game (accumulated heat, high stakes). Track actual piracy frequency curves against this target.

8. **Does storage management feel strategic or tedious?** Deleting old games to make room should feel like a meaningful choice, not inventory Tetris. If players are spending more than 60 seconds managing storage per session, the system needs streamlining.

9. **Is the weekly allowance calibrated to create interesting choices?** The player should be able to afford approximately 30--40% of what they want, forcing prioritization. Track what players spend on and what they skip. If everyone is making the same spending choices, the economy is not presenting real trade-offs.

### Priority 4: Meta Arc and Pacing

10. **Is the total playthrough length correct at 15--25 hours?** Does the finale feel like it arrives too soon (player wanted more) or too late (player was ready to stop hours ago)? Both failure modes require different fixes -- pacing adjustment vs. content addition.

11. **Do players start a second playthrough?** The design assumes procedural generation creates replayability. Validate this. If the second playthrough feels too similar to the first within the first 2 hours, the character and event generation systems need more variance.

12. **Where do players save-quit most often?** This reveals natural session boundaries. If they are quitting mid-prep-cycle, the session loop is too long. If they are quitting after aftermath, the pacing is correct.

---

## 10. Appendix: Interaction Matrix

This matrix maps which systems directly affect which other systems. "D" = direct interaction. "I" = indirect interaction (through a shared resource or state).

|  | Desktop | Community | Acquisition | LAN Party | Reputation | Snacks |
|---|---|---|---|---|---|---|
| **Desktop** | -- | D | D | D | I | I |
| **Community** | D | -- | I | D | D | I |
| **Acquisition** | D | I | -- | D | D | -- |
| **LAN Party** | D | D | D | -- | D | D |
| **Reputation** | I | D | D | D | -- | -- |
| **Snacks** | I | I | -- | D | -- | -- |

Key coupling points:
- **Community <-> LAN Party** is the tightest coupling. Characters drive party quality; party outcomes reshape characters. This is the heartbeat of the game.
- **Acquisition <-> Reputation** is the most strategically interesting coupling. What you download and how you get it defines your standing in every community.
- **Desktop <-> Everything** is architectural, not strategic. The desktop is the lens through which all systems are accessed. It must never be a bottleneck.

---

## 11. Design Pillars -- Summary

If this document is too long and you need three sentences, here they are:

1. **The desktop is the game.** Not a menu. Not a wrapper. The simulation of a 2003 Windows XP desktop is the primary toy, and every game system is an application inside it.

2. **Characters are the content.** AI-driven persistent NPCs with memory, personality, and agenda are what make each playthrough unique. The game lives or dies on whether players care about their crew.

3. **The loop is caretaking.** Triage notifications, maintain relationships, manage risk, host events, process aftermath, repeat. The 30-second loop is answering a message. The session loop is hosting a party. The meta loop is building and losing a community. At every scale, the player is taking care of something that matters.

What's the loop? It is reading a message from someone who trusts you and deciding how to respond. It is burning a CD at 2 AM so tomorrow's party has one more game. It is noticing that your best friend's away message has been "..." for a week and choosing to ask why.

Where's the depth? It is in the invisible web of relationships, reputations, and risks that the player builds through thousands of small decisions -- none of which feel small.

How does this feel at hour 20? It feels like your desktop is a world. Like these screen names are people. Like the next LAN party actually matters. And somewhere in the back of your mind, you know this cannot last forever -- and that is exactly what makes it beautiful.

---

*Document by REED -- Game Designer*
*First pass complete. Zero placeholders. Zero TODOs. Ready for internal review and vertical slice planning.*
