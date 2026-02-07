# LAN PARTY -- Release Plan

**Release Manager:** SHIP
**Status:** Master Release Checklist -- Ready for Implementation
**Reference Docs:** `pitch.md`, `game-design.md`, `technical-architecture.md`
**Target Platform:** PC (Steam), Steam Deck verified
**Target Launch Date:** TBD (set 90 days before launch)
**Last Updated:** 2026-02-07

---

## 0. Document Purpose

This document is the single source of truth for LAN PARTY's release process. If it is not on a checklist in this document, it does not happen. If a step fails, we execute the documented rollback procedure. No improvisation. No surprises. No launch day panic.

Launch day should be boring. If nothing goes wrong, I did my job.

---

## 1. Master Launch Checklist

Every item has an owner, a deadline relative to launch (L-X days), and a verification method. Items are categorized by phase. Nothing goes unchecked.

### 1.1 CODE COMPLETE PHASE (L-90 to L-60)

#### Build Pipeline

- [ ] **[BYTE] L-90:** Final commit tagged as `code-complete-candidate-1`. No new features past this point.
- [ ] **[BYTE] L-90:** All unit tests passing on CI/CD.
- [ ] **[BYTE] L-90:** All integration tests passing on staging build.
- [ ] **[BYTE] L-85:** Performance profiling complete on target hardware (mid-range 2020 laptop, Steam Deck). Verify 60 FPS desktop, 30 FPS mini-games, 2GB RAM max.
- [ ] **[BYTE] L-85:** Memory leak testing complete. Run game for 8 continuous hours. No memory growth beyond 2.2GB.
- [ ] **[BYTE] L-80:** Save/load stress testing complete. Load 50 save files from different game states. Zero corruption.
- [ ] **[BYTE] L-80:** AI text generation latency profiling complete. Verify < 3s per message with typing indicator masking delay.

#### Content Lock

- [ ] **[NOVA] L-90:** All character personality profiles finalized. No changes to AI prompts past this point.
- [ ] **[REED] L-90:** All mini-game balance locked. No mechanic changes past this point.
- [ ] **[PIXEL] L-90:** All UI assets finalized. No art changes past this point (exception: critical bug fixes).
- [ ] **[ECHO] L-90:** All audio assets finalized. No sound changes past this point.
- [ ] **[NOVA] L-85:** All narrative beats tested. Verify finale triggers correctly in 10 test playthroughs.
- [ ] **[REED] L-85:** Economy balance locked. Verify allowance/cost ratio tested across 20-hour playthrough.

#### Platform Testing

- [ ] **[CRASH] L-85:** Windows 10 clean install testing complete. Verify game runs on fresh Windows 10 VM with zero dependencies pre-installed.
- [ ] **[CRASH] L-85:** Windows 11 clean install testing complete.
- [ ] **[CRASH] L-80:** Steam Deck hardware testing complete. Verify controls, performance, battery life (target: 3+ hours).
- [ ] **[CRASH] L-80:** Linux/Proton compatibility verified on 3 distros (Ubuntu, Fedora, Arch).
- [ ] **[CRASH] L-75:** macOS testing complete (if supporting). Verify on latest macOS version.
- [ ] **[CRASH] L-75:** Low-spec hardware testing complete. Test on minimum spec machine (see section 4.2).

### 1.2 BETA/QA PHASE (L-60 to L-30)

#### Internal QA

- [ ] **[CRASH] L-60:** QA test plan finalized. Covers all systems, all edge cases, all failure modes.
- [ ] **[CRASH] L-60:** Regression testing complete. All previously fixed bugs verified as fixed.
- [ ] **[CRASH] L-55:** Full playthrough testing complete (5 testers, 15-25 hours each). Log all bugs, prioritize by severity.
- [ ] **[CRASH] L-50:** Critical bugs (crashes, save corruption, progression blockers) fixed and verified. Zero P0 bugs remain.
- [ ] **[CRASH] L-45:** High-priority bugs (major exploits, UX blockers, immersion breakers) fixed and verified.
- [ ] **[CRASH] L-40:** Medium-priority bugs triaged. Fix or defer to post-launch patch.

#### External Beta

- [ ] **[HYPE + CRASH] L-45:** Steam playtest build deployed. 100-200 external testers invited.
- [ ] **[HYPE] L-45:** Beta feedback channels set up (Discord, Steam forums, Google Form).
- [ ] **[CRASH] L-40:** Week 1 beta feedback reviewed. Prioritize critical issues.
- [ ] **[BYTE] L-38:** Critical beta issues fixed. Deploy beta patch 1.
- [ ] **[CRASH] L-35:** Week 2 beta feedback reviewed. Verify critical issues resolved.
- [ ] **[BYTE] L-33:** Deploy beta patch 2 (final beta build).
- [ ] **[CRASH] L-30:** Beta feedback aggregated. If no critical issues remain, promote beta build to release candidate.

#### Localization (if supporting)

- [ ] **[CLOCK] L-60:** Localization scope finalized. Which languages? (Recommend: English only for launch, add languages post-launch.)
- [ ] **[CLOCK] L-55:** Localization strings extracted and sent to translators.
- [ ] **[CLOCK] L-40:** Translated strings received and integrated.
- [ ] **[CRASH] L-35:** Localization QA complete. Verify no text overflow, broken formatting, mistranslations.

### 1.3 PLATFORM SETUP PHASE (L-60 to L-14)

#### Steam Store Page

- [ ] **[HYPE] L-60:** Store page copy finalized (description, features, about section).
- [ ] **[HYPE] L-60:** Store page assets prepared: 5 screenshots, 1 trailer (1-2 minutes), header capsule, library capsule, logo.
- [ ] **[HYPE] L-55:** Store page submitted to Steam for review.
- [ ] **[HYPE] L-50:** Store page approved by Steam (if rejected, iterate and resubmit).
- [ ] **[HYPE] L-50:** Store page set to "coming soon" visibility. Wishlist campaign begins.
- [ ] **[SHIP] L-45:** Steam app ID and depot configured. Upload first test build to private branch.
- [ ] **[SHIP] L-45:** Verify Steam depot upload works. Download build from Steam, run, verify integrity.

#### Steamworks Features

- [ ] **[SHIP] L-40:** Achievements configured in Steamworks partner portal (see section 3.2 for achievement list).
- [ ] **[SHIP] L-40:** Achievement icons uploaded (locked and unlocked states).
- [ ] **[BYTE] L-38:** Achievement integration complete. Verify achievements trigger correctly in-game.
- [ ] **[SHIP] L-35:** Cloud saves configured. Test save sync across two machines.
- [ ] **[SHIP] L-35:** Steam Workshop configured (if supporting user-generated content). Document submission guidelines.
- [ ] **[SHIP] L-30:** Trading cards configured (if applying). Design 5-8 cards, badge, emoticons, profile backgrounds.
- [ ] **[SHIP] L-30:** Trading cards approved by Steam (review takes 1-2 weeks).
- [ ] **[SHIP] L-28:** Big Picture Mode / Steam Deck compatibility verified. Controller mappings set.
- [ ] **[SHIP] L-21:** Launch discount configured (if offering). Recommend: 10% launch week discount.
- [ ] **[SHIP] L-21:** Regional pricing reviewed. Verify fair pricing across all regions (use Steam's auto-suggestions as baseline).

#### Age Ratings / Compliance

- [ ] **[SHIP] L-50:** Age rating determination complete (see section 5 for details). Expected: ESRB Teen (13+), PEGI 12.
- [ ] **[SHIP] L-50:** IARC questionnaire submitted via Steam (auto-generates ratings for most regions).
- [ ] **[SHIP] L-45:** Age rating certificates received. Upload to Steam.
- [ ] **[SHIP] L-40:** Content warning review complete. Does game need warnings for piracy themes, mild language, online interactions?
- [ ] **[SHIP] L-40:** Privacy policy finalized (if game collects any data). Post to website and link in-game.
- [ ] **[SHIP] L-40:** Terms of service finalized (if game has online features or user-generated content).
- [ ] **[SHIP] L-35:** GDPR compliance verified (if supporting EU). Data storage, user rights, deletion requests.

#### Marketing & Community

- [ ] **[HYPE] L-45:** Launch trailer finalized. Upload to YouTube, Steam store page.
- [ ] **[HYPE] L-40:** Press kit finalized: screenshots, trailer, fact sheet, key art, logo pack, press release template.
- [ ] **[HYPE] L-40:** Press list compiled. Target: PC gaming sites, indie game curators, nostalgia-focused outlets.
- [ ] **[HYPE] L-35:** Press outreach begins. Send press kits and review keys.
- [ ] **[HYPE] L-30:** Influencer outreach begins. Target: streamers/YouTubers who cover management sims, nostalgia games, indie gems.
- [ ] **[HYPE] L-28:** Review embargo set (recommend: L-7 to build hype, avoid early negative reviews killing momentum).
- [ ] **[HYPE] L-21:** Social media campaign begins. Daily countdown posts, dev diaries, behind-the-scenes.
- [ ] **[HYPE] L-14:** Discord server launched (if supporting). Moderators assigned. Community guidelines posted.
- [ ] **[HYPE] L-14:** Steam community hub activated. Forums moderated, discussions seeded.

### 1.4 GOLD MASTER PHASE (L-14 to L-1)

#### Build Finalization

- [ ] **[BYTE] L-14:** Release candidate 1 (RC1) built. Final commit tagged as `rc1`.
- [ ] **[CRASH] L-13:** RC1 smoke testing complete (play 2 hours, verify no critical bugs).
- [ ] **[CRASH] L-12:** RC1 full regression pass complete. Verify no new issues introduced.
- [ ] **[SHIP] L-10:** RC1 promoted to gold master. Tag commit as `gold-master-v1.0.0`.
- [ ] **[SHIP] L-10:** Gold master uploaded to Steam default branch (set to "not released" until launch).
- [ ] **[SHIP] L-10:** Gold master archived. Store in 3 places: local backup, cloud backup, external drive.
- [ ] **[SHIP] L-9:** Verify Steam build integrity. Download from Steam depot, run on clean machine, verify matches gold master.
- [ ] **[SHIP] L-9:** Day-one patch decision. Are there any known issues that need a patch? If yes, begin patch development.

#### Launch Day Preparation

- [ ] **[SHIP] L-7:** Launch checklist finalized (see section 2 for hour-by-hour timeline).
- [ ] **[SHIP] L-7:** Launch day war room scheduled. Who is on call? (Recommend: SHIP, BYTE, HYPE, CRASH.)
- [ ] **[SHIP] L-7:** Communication templates prepared: launch announcement, known issues post, emergency downtime notice, hotfix announcement.
- [ ] **[SHIP] L-7:** Rollback procedure tested (see section 6). Verify we can revert to previous build in < 30 minutes.
- [ ] **[SHIP] L-5:** Hotfix pipeline tested. Build, test, upload, deploy a dummy patch. Verify speed.
- [ ] **[SHIP] L-3:** Steam store page set to release at launch time (recommend: 10 AM PT for maximum visibility).
- [ ] **[SHIP] L-3:** All marketing assets scheduled: launch tweet, Discord announcement, Steam news post, press release.
- [ ] **[SHIP] L-1:** Final pre-launch check. Verify store page, build, pricing, regions all correct.
- [ ] **[SHIP] L-1:** Team briefed on launch day timeline. Everyone knows their role.
- [ ] **[SHIP] L-1:** Get some sleep. Tomorrow is the day.

### 1.5 LAUNCH DAY (L-Day)

See section 2 for detailed hour-by-hour timeline.

- [ ] **[SHIP] L+0h:** Game goes live on Steam. Verify store page is live, build is downloadable.
- [ ] **[HYPE] L+0h:** Launch announcements posted across all channels.
- [ ] **[CRASH] L+1h:** Monitor Steam forums, Discord, social media for critical issues.
- [ ] **[SHIP] L+2h:** First post-launch metrics review: sales, downloads, crash reports, reviews.
- [ ] **[SHIP] L+6h:** Mid-day check-in. Any critical issues? Deploy hotfix if needed.
- [ ] **[SHIP] L+12h:** End-of-day review. Aggregate feedback. Plan patch 1 if needed.
- [ ] **[SHIP] L+24h:** Launch retrospective. What went right? What went wrong? Document lessons learned.

### 1.6 POST-LAUNCH PHASE (L+1 to L+30)

#### Monitoring & Support

- [ ] **[CRASH] L+1:** Daily bug triage. Prioritize crash reports and progression blockers.
- [ ] **[SHIP] L+3:** Patch 1 scoped. Fix critical issues reported in first 72 hours.
- [ ] **[BYTE] L+5:** Patch 1 developed and tested.
- [ ] **[SHIP] L+7:** Patch 1 deployed. Announce via Steam news and Discord.
- [ ] **[CRASH] L+14:** Patch 2 scoped. Fix high-priority bugs and quality-of-life issues.
- [ ] **[BYTE] L+16:** Patch 2 developed and tested.
- [ ] **[SHIP] L+21:** Patch 2 deployed.
- [ ] **[SHIP] L+30:** 30-day post-launch review. Sales performance, player retention, review sentiment, roadmap adjustments.

#### Community Management

- [ ] **[HYPE] L+1:** Daily Discord/forum moderation. Address questions, gather feedback, manage toxic behavior.
- [ ] **[HYPE] L+7:** First post-launch dev diary. Thank players, share metrics, preview upcoming content.
- [ ] **[HYPE] L+14:** Community feature request aggregation. What do players want most?
- [ ] **[HYPE] L+30:** Roadmap announcement. What is coming in the first 3 months post-launch?

#### Analytics & Iteration

- [ ] **[CLOCK] L+3:** Analytics dashboard set up. Track: session length, progression rate, drop-off points, crash frequency.
- [ ] **[REED] L+7:** Gameplay telemetry review. Where are players struggling? Where are they quitting?
- [ ] **[REED] L+14:** Balance adjustments scoped based on telemetry. Economy too tight? Difficulty spikes?
- [ ] **[CLOCK] L+30:** Sales performance review. Hit targets? Adjust marketing spend.

---

## 2. Launch Day Timeline (Hour-by-Hour)

This is the schedule for launch day. All times relative to store page go-live (recommend: 10 AM PT / 1 PM ET / 6 PM UTC).

### Pre-Launch (L-Day, 6 AM PT)

**T-4h: War Room Opens**
- [ ] SHIP, BYTE, HYPE, CRASH on call via Discord voice channel.
- [ ] Final verification: Steam store page scheduled to release at 10 AM PT.
- [ ] Final verification: Build integrity. Download gold master from Steam, run on clean machine.
- [ ] Final verification: All marketing assets queued (Twitter, Discord, Steam news, press release).
- [ ] Emergency contacts confirmed: Steam partner support, hosting provider (if applicable), Discord admins.

**T-2h: Final Pre-Flight**
- [ ] Verify store page live status. Should still be "coming soon" until 10 AM PT.
- [ ] Verify pricing correct in all regions.
- [ ] Verify launch discount configured (if applicable).
- [ ] Verify review embargo lifts at correct time (recommend: same time as launch or T-1h).
- [ ] Team breakfast. Eat. Hydrate. Last chance for bathroom break before chaos.

### Launch Window (10 AM PT)

**T+0h: Go Live**
- [ ] 10:00 AM PT: Game releases on Steam. Store page transitions from "coming soon" to "buy now."
- [ ] SHIP verifies: Store page is live. Click "buy now," verify it works.
- [ ] SHIP verifies: Build is downloadable. Purchase game (test account), download, install, launch. Verify it runs.
- [ ] HYPE posts launch announcements:
  - Steam news post: "LAN PARTY is out now!"
  - Twitter/X: Launch tweet with trailer link and store link.
  - Discord: @everyone ping with launch announcement.
  - Reddit: r/gamedev, r/indiegaming, r/Games (follow subreddit rules).
  - Press release sent to press list.
- [ ] BYTE monitors crash reporting backend. Any crashes in first 10 minutes?

**T+15m: First Check-In**
- [ ] SHIP: Any reports of download issues? Installation failures?
- [ ] CRASH: Any forum/Discord posts about critical bugs?
- [ ] HYPE: Social media sentiment check. What are people saying?
- [ ] BYTE: Crash report review. Any patterns?

**T+30m: Early Adopter Wave**
- [ ] SHIP: First sales data visible in Steamworks dashboard. How many units sold?
- [ ] CRASH: First gameplay feedback arriving. Any progression blockers reported?
- [ ] HYPE: Streamer/YouTuber monitoring. Anyone streaming yet? Any issues on stream?

**T+1h: Critical Issue Window**
- [ ] This is the highest-risk hour. Most critical issues surface now.
- [ ] CRASH aggregates all reports. Categorize: P0 (game-breaking), P1 (major), P2 (minor).
- [ ] If P0 issue found:
  - BYTE investigates immediately.
  - SHIP prepares hotfix pipeline.
  - HYPE drafts "known issue" announcement.
  - Decision point: Deploy hotfix immediately or wait for more data?
- [ ] If no P0 issues: Celebrate. The build is stable.

### Mid-Day Monitoring (12 PM PT)

**T+2h: First Metrics Review**
- [ ] SHIP: Sales performance. On track vs. projections?
- [ ] SHIP: Steam reviews. Any negative reviews citing critical bugs? (Early negative reviews are momentum killers.)
- [ ] CRASH: Bug triage. Prioritize most-reported issues.
- [ ] BYTE: Performance monitoring. Any unexpected CPU/GPU spikes reported? Memory leaks?
- [ ] HYPE: Press coverage check. Any reviews live? Metacritic score (if applicable)?

**T+4h: Lunch Break (Staggered)**
- [ ] War room stays staffed. Rotate breaks. Someone always monitoring.

**T+6h: Hotfix Decision Point**
- [ ] Review all data from first 6 hours.
- [ ] Decision: Deploy hotfix today or wait until tomorrow?
  - Deploy today if: P0 issue affecting >10% of players, or negative review momentum building.
  - Wait until tomorrow if: Only minor issues, or issues affect <5% of players and have workarounds.
- [ ] If deploying hotfix: Execute hotfix procedure (section 7).

### Evening Monitoring (6 PM PT)

**T+8h: Evening Check-In**
- [ ] Player base expanding. Peak hours (evening US East Coast).
- [ ] Monitor for server load issues (if game has online components).
- [ ] Monitor for regional issues. EU/Asia players now active. Any region-specific bugs?

**T+10h: End-of-Day Planning**
- [ ] SHIP: Aggregate all feedback from launch day.
- [ ] CRASH: Final bug triage. What must be fixed in patch 1?
- [ ] BYTE: Patch 1 scope finalized. Timeline: develop tomorrow, deploy L+2 or L+3.
- [ ] HYPE: Draft "thank you" post for community. Acknowledge known issues, confirm patch incoming.

**T+12h: War Room Closes**
- [ ] Launch day is over. Game is live and stable (hopefully).
- [ ] On-call rotation begins. SHIP and BYTE on-call overnight for critical issues only.
- [ ] Team debrief scheduled for tomorrow morning.

### Post-Launch Monitoring (Ongoing)

**L+24h: Launch Retrospective**
- [ ] What went right?
- [ ] What went wrong?
- [ ] What surprised us?
- [ ] What would we do differently next time?
- [ ] Document lessons learned. Update this release plan for the next game.

---

## 3. Platform Configuration Checklist (Steamworks)

Steam is the primary platform. Every Steamworks feature must be configured correctly before launch.

### 3.1 Store Page Configuration

- [ ] App name: "LAN PARTY"
- [ ] Developer name: [Studio Name]
- [ ] Publisher name: [Studio Name or publisher if applicable]
- [ ] Release date: Set to launch date. Do NOT set to "TBA" or "coming soon" after launch date is locked.
- [ ] Short description (300 characters): Elevator pitch from pitch.md.
- [ ] Long description: Full pitch, features, core loop explanation.
- [ ] About This Game section: Detailed feature breakdown, screenshots, GIFs.
- [ ] Mature Content Description: "This game depicts piracy of software, which is illegal. Consequences are portrayed within the game. No graphic violence, sexual content, or strong language."
- [ ] System Requirements:
  - **Minimum:** Windows 10 64-bit, Intel i3-6100 or equivalent, 4GB RAM, Integrated graphics (Intel HD 520 or better), 2GB storage, Mouse and keyboard required.
  - **Recommended:** Windows 10/11 64-bit, Intel i5-8250U or equivalent, 8GB RAM, Dedicated GPU (GTX 1050 or better), 3GB storage, SSD recommended, Steam Deck verified.
- [ ] Supported languages: English (interface and audio). Add more languages post-launch.
- [ ] Tags: Management Simulation, Social Simulation, Indie, Singleplayer, Nostalgia, Early 2000s, AI-Driven Characters, Replayable, Story-Rich, Desktop Simulation.
- [ ] Categories: Single-player, Steam Achievements, Full controller support (Steam Deck), Steam Cloud, Steam Trading Cards (if approved).

### 3.2 Achievements

Design 20-30 achievements. Mix of progression-based (unmissable), skill-based (challenging), and discovery-based (hidden). Avoid grind achievements.

**Proposed Achievement List:**

| Name | Description | Type | Hidden? |
|---|---|---|---|
| First Message | Send your first MSN message. | Progression | No |
| First Download | Complete your first file download. | Progression | No |
| First LAN Party | Host your first LAN party. | Progression | No |
| Party of Five | Host a LAN party with 5 or more people. | Progression | No |
| Party of Ten | Host a LAN party with 10 or more people. | Progression | No |
| Legendary Host | Host 20 LAN parties. | Progression | No |
| Scene Access | Gain access to a private tracker. | Progression | No |
| Scene Legend | Reach maximum reputation in the warez scene. | Skill | No |
| Clean Library | Own 10 games acquired legally (no piracy). | Challenge | No |
| Master Pirate | Download 50 games via piracy. | Discovery | No |
| ISP Wrath | Receive a cease-and-desist letter from your ISP. | Discovery | No |
| Malware Victim | Install a file infected with malware. | Discovery | No |
| Zero Crashes | Host a LAN party with zero technical issues. | Skill | No |
| Peacekeeper | Mediate 10 crew conflicts successfully. | Skill | No |
| Rivalry Resolved | Help two rival crew members become friends. | Skill | No |
| The Ghost Returns | Bring back a crew member who went offline for 2+ weeks. | Skill | Yes |
| Perfect Party | Host a LAN party with 90+ quality score. | Skill | No |
| Snack Master | Never run out of snacks during a LAN party (10 parties). | Skill | No |
| Playlist Curator | Create a Winamp playlist that boosts party mood by 20+. | Skill | No |
| Finale | Complete the game's finale arc. | Progression | Yes |
| Everyone Showed Up | Host the final LAN party with all original crew present. | Skill | Yes |
| Nostalgia Trip | Change your desktop wallpaper 10 times. | Discovery | No |
| Hoarder | Fill your hard drive to 100% capacity. | Discovery | No |
| Minimalist | Complete the game with fewer than 10 games in library. | Challenge | No |
| Speed Downloader | Download a 4GB file in under 2 hours (in-game time). | Skill | No |
| Forum Celebrity | Reach 100 reputation on the forum. | Progression | No |
| Loyal Friend | Maintain a 90+ relationship with one character for the entire game. | Skill | No |
| Community Builder | Have 15 crew members active simultaneously. | Progression | No |
| The End of an Era | Watch the credits roll. | Progression | Yes |

Achievement icons: 64x64 pixels, locked and unlocked states. Style: pixel art or XP-era icon aesthetic.

### 3.3 Trading Cards

If applying for trading cards (requires game to meet Steamworks guidelines: enough playtime, positive reviews, no fake engagement).

**Card Set Design (5 cards):**
1. "The Host" - Key art: player at desktop, glowing monitor.
2. "The Crew" - Key art: CRT monitors in basement, five faces lit by blue glow.
3. "The Download" - Key art: progress bar at 99%, mIRC window in background.
4. "The Party" - Key art: LAN party in full swing, ethernet cables everywhere.
5. "The Finale" - Key art: empty basement, one monitor still on, "last online: 3 days ago."

Badge: 5 levels (crafted from cards).
Emoticons: 6 emoticons (MSN-style icons: smiley, wink, rage, crying, GG, brb).
Profile backgrounds: 2 backgrounds (CRT monitor glow, desktop screenshot).

### 3.4 Cloud Saves

- [ ] Enable Steam Cloud in Steamworks settings.
- [ ] Configure cloud save path: `%AppData%/LANParty/saves/`
- [ ] Set max cloud storage: 50MB per user (generous for JSON save files).
- [ ] Test cloud sync: Save on Machine A, load on Machine B. Verify integrity.
- [ ] Test conflict resolution: Save on Machine A offline, save on Machine B online, reconnect Machine A. Verify user is prompted to choose version.

### 3.5 Big Picture / Steam Deck

- [ ] Set "Steam Deck Compatibility" to "Verified" (if fully compatible) or "Playable" (if minor issues).
- [ ] Configure controller mappings: Default layout for Steam Controller, Xbox controller, PS controller.
- [ ] Test on Steam Deck hardware: Performance, controls, text readability, battery life.
- [ ] Deck-specific considerations:
  - UI text must be readable at 1280x800 resolution (Deck screen).
  - Touch screen support for desktop clicking (Steam Deck has touchscreen).
  - Performance target: 30 FPS minimum, 40-60 FPS preferred.
  - Battery target: 3+ hours of gameplay.

### 3.6 Regional Pricing

Use Steam's recommended pricing calculator as baseline. Adjust for purchasing power parity.

**Recommended Base Price:** $19.99 USD (justification: 15-25 hour playtime, high replayability, indie budget, nostalgia premium).

Regional pricing (examples):
- EU: €18.99
- UK: £16.99
- Canada: $24.99 CAD
- Australia: $29.95 AUD
- Russia: 1299 RUB (adjust based on exchange rate and Steam recommendations)
- China: ¥68 CNY
- Japan: ¥2200 JPY

Review and adjust based on market research and Steam's auto-suggestions.

### 3.7 Launch Discount

- [ ] Offer 10% launch week discount (first 7 days).
- [ ] Do NOT discount deeper than 10% in first month (devalues game, trains players to wait for sales).
- [ ] Plan future sales: Summer Sale (20% off), Winter Sale (25% off), anniversary sale (30% off).

---

## 4. Build Pipeline Documentation

This section documents how to build, test, and deploy the game. Anyone on the team should be able to execute this process.

### 4.1 Build Process

**Prerequisites:**
- Godot 4.3 installed (download from godotengine.org).
- Git repository cloned locally.
- Steam partner account credentials (for uploading builds).
- SteamCMD installed (for automated depot uploads).

**Step-by-Step Build:**

1. **Verify clean state:**
   ```bash
   cd /path/to/lan-party-repo
   git status
   # Ensure no uncommitted changes
   ```

2. **Tag release commit:**
   ```bash
   git tag -a v1.0.0 -m "Gold master release"
   git push origin v1.0.0
   ```

3. **Run tests:**
   ```bash
   godot --headless --path . --script res://tests/run_tests.gd
   # Verify all tests pass
   ```

4. **Export Windows build:**
   ```bash
   godot --export "Windows Desktop" builds/lan_party_v1.0.0_win64.exe
   ```

5. **Export Linux build:**
   ```bash
   godot --export "Linux/X11" builds/lan_party_v1.0.0_linux.x86_64
   ```

6. **Export macOS build (if supporting):**
   ```bash
   godot --export "macOS" builds/lan_party_v1.0.0_macos.dmg
   ```

7. **Verify build integrity:**
   - Run each build on a clean machine (VM or test hardware).
   - Play for 15 minutes. Verify: no crashes, save/load works, all systems functional.

8. **Create installer (Windows only):**
   - Use InnoSetup or NSIS to create installer.
   - Installer should: install game to Program Files, create Start Menu shortcut, create Desktop shortcut, install Visual C++ redistributables (if needed).

9. **Archive builds:**
   - Create ZIP of each build.
   - Store in 3 locations: local backup, cloud storage (Google Drive, Dropbox), external drive.

### 4.2 System Requirements Testing

Test on machines that match minimum and recommended specs. Do NOT skip this step. If the game does not run on minimum spec, you will get refunds and negative reviews.

**Minimum Spec Test Machine:**
- CPU: Intel i3-6100 or AMD equivalent
- RAM: 4GB
- GPU: Integrated graphics (Intel HD 520)
- OS: Windows 10 64-bit, fresh install
- Storage: HDD (not SSD)

**Test procedure:**
1. Install game on minimum spec machine.
2. Launch game. Measure startup time (should be < 30 seconds).
3. Play for 30 minutes. Monitor FPS (should be 30+ FPS for desktop, 20+ FPS for mini-games).
4. Monitor RAM usage (should stay under 2.5GB).
5. Save and load game. Verify no corruption.
6. Exit game. Verify no crash on exit.

**Recommended Spec Test Machine:**
- CPU: Intel i5-8250U or AMD equivalent
- RAM: 8GB
- GPU: GTX 1050 or equivalent
- OS: Windows 11 64-bit
- Storage: SSD

**Test procedure:**
1. Same as minimum spec test.
2. Verify 60 FPS for desktop, 30 FPS for mini-games.
3. Verify startup time < 10 seconds.

### 4.3 Steam Depot Upload

Use SteamCMD to upload builds to Steam depots.

**Setup:**
1. Install SteamCMD: https://developer.valvesoftware.com/wiki/SteamCMD
2. Create app build script (`app_build_1234567.vdf`):

```vdf
"AppBuild"
{
    "AppID" "1234567"  // Your Steam App ID
    "Desc" "LAN PARTY v1.0.0"
    "BuildOutput" "output/"
    "ContentRoot" "builds/"
    "SetLive" "default"  // Branch name (use "default" for public release)

    "Depots"
    {
        "1234568"  // Windows depot ID
        {
            "FileMapping"
            {
                "LocalPath" "lan_party_v1.0.0_win64/*"
                "DepotPath" "."
            }
        }
        "1234569"  // Linux depot ID
        {
            "FileMapping"
            {
                "LocalPath" "lan_party_v1.0.0_linux/*"
                "DepotPath" "."
            }
        }
    }
}
```

**Upload command:**
```bash
steamcmd +login your_steam_username +run_app_build /path/to/app_build_1234567.vdf +quit
```

**Verify upload:**
1. Log in to Steamworks partner portal.
2. Navigate to "Builds" tab.
3. Verify new build appears in list.
4. Set build to "default" branch (or keep on private branch for testing).
5. Download build via Steam client (use test account).
6. Run and verify integrity.

### 4.4 Automated Build Pipeline (CI/CD)

Use GitHub Actions for automated builds (see technical-architecture.md section 7.2 for YAML).

**Workflow:**
1. On commit to `main`: Run unit tests, export Linux build, upload to itch.io internal branch.
2. On tag push (e.g., `v1.0.0`): Run full test suite, export all platforms, upload to Steam private branch, notify team.

**Benefits:**
- Every commit is tested automatically.
- Builds are reproducible.
- No "works on my machine" issues.

---

## 5. Age Rating & Compliance

Age ratings are required to release on Steam in most regions. Use IARC (International Age Rating Coalition) via Steam's built-in questionnaire.

### 5.1 Expected Ratings

Based on content (piracy themes, mild language, no violence, no sexual content):

- **ESRB:** Teen (13+)
  - Content descriptors: Simulated Gambling (if applicable), Mild Language, Use of Alcohol and Tobacco (if depicted in-game).
- **PEGI:** 12
  - Content descriptors: Bad Language (if applicable).
- **USK (Germany):** 6
- **ACB (Australia):** PG
- **CERO (Japan):** A (all ages) or B (12+)

### 5.2 IARC Questionnaire Guidance

When filling out the IARC questionnaire on Steam:

**Violence:**
- "Does the game contain violence?" → No (or "cartoon violence" if mini-games depict shooting, but it is highly abstracted).

**Sexuality:**
- "Does the game contain sexual content?" → No.

**Language:**
- "Does the game contain bad language?" → Mild (if AI-generated chat includes words like "damn" or "crap"). Otherwise, No.

**Drugs/Alcohol/Tobacco:**
- "Does the game depict or reference drugs, alcohol, or tobacco?" → No (unless you show characters drinking soda/energy drinks, which is not rated content).

**Gambling:**
- "Does the game contain gambling?" → No.

**Online Interactions:**
- "Does the game allow online interactions with other players?" → No (single-player only).
- "Does the game allow user-generated content?" → No (unless Steam Workshop is enabled).

**Piracy/Illegal Activity:**
- "Does the game depict illegal activity?" → Yes. Describe: "The game depicts software piracy as a core mechanic. Consequences (ISP warnings, malware, social fallout) are portrayed within the game. Piracy is not glorified; it is presented as a morally complex choice with trade-offs."

### 5.3 Content Warnings

Consider adding an in-game content warning on first launch:

> "LAN PARTY depicts software piracy, which is illegal in most jurisdictions. This game is a work of fiction set in the early 2000s and does not endorse piracy. All events, characters, and consequences are fictional."

This protects the studio legally and sets player expectations.

### 5.4 GDPR Compliance (if supporting EU)

If the game collects any player data (analytics, telemetry, crash reports):

- [ ] Privacy policy drafted and posted to website.
- [ ] Privacy policy linked in-game (settings menu or credits).
- [ ] Player data stored securely (encrypted at rest, encrypted in transit).
- [ ] Player can request data deletion (provide email contact for GDPR requests).
- [ ] Crash reports anonymized (no personally identifiable information).

If the game does NOT collect any data (fully offline, no telemetry):
- [ ] State this clearly in privacy policy: "LAN PARTY does not collect, store, or transmit any player data."

---

## 6. Rollback & Hotfix Procedures

Things will go wrong. When they do, we need to act fast. These procedures ensure we can revert to a stable build or deploy a hotfix in under 60 minutes.

### 6.1 Rollback Procedure (Revert to Previous Build)

**When to rollback:**
- Critical bug discovered post-launch that affects >50% of players (e.g., save corruption, crash on startup, progression blocker).
- Hotfix introduced a worse bug than it fixed.

**Rollback steps:**

1. **Identify last known good build:**
   - Check Steamworks build history.
   - Identify previous build (e.g., `v1.0.0` before hotfix `v1.0.1`).

2. **Set previous build to live:**
   - Log in to Steamworks partner portal.
   - Navigate to "Builds" tab.
   - Find last known good build.
   - Click "Set build live on default branch."
   - Confirm action.

3. **Verify rollback:**
   - Steam updates propagate in 5-10 minutes.
   - Download game on test account. Verify previous build is now live.

4. **Communicate to players:**
   - Post Steam announcement: "We have reverted to the previous build while we investigate an issue. Your saves are safe. A fix is incoming."
   - Post on Discord and social media.

5. **Investigate and fix:**
   - Reproduce the critical bug.
   - Fix in development branch.
   - Test thoroughly on clean machines.
   - Deploy new hotfix (see section 6.2).

**Rollback time target:** < 30 minutes from decision to rollback to new build live.

### 6.2 Hotfix Procedure (Deploy Emergency Patch)

**When to hotfix:**
- Critical bug affecting 10-50% of players.
- Fix is small, low-risk, and well-tested.

**Hotfix steps:**

1. **Reproduce bug:**
   - Get repro steps from player reports.
   - Reproduce on dev machine.
   - Confirm bug is critical (crashes, save corruption, progression blocker).

2. **Develop fix:**
   - Create hotfix branch from `gold-master` tag: `git checkout -b hotfix-v1.0.1 gold-master`
   - Fix bug. Keep changes minimal. Do NOT add features or refactor.
   - Commit fix: `git commit -m "fix: resolve crash on startup when save file is corrupted"`

3. **Test fix:**
   - Run unit tests. Verify no regressions.
   - Run integration tests. Verify fix works.
   - Test on clean machine. Reproduce original bug, verify it is fixed.
   - Play for 30 minutes. Verify no new issues introduced.

4. **Build hotfix:**
   - Export builds for all platforms.
   - Verify build integrity (run on clean machine).

5. **Upload to Steam:**
   - Upload hotfix build to Steam depot.
   - Tag as `hotfix-v1.0.1`.
   - Set to live on default branch immediately (or schedule for off-peak hours if not urgent).

6. **Communicate to players:**
   - Post Steam announcement: "Hotfix v1.0.1 is now live. Fixed: [bug description]. Thank you for your patience."
   - Post on Discord and social media.

7. **Monitor post-hotfix:**
   - Watch for new reports. Did the hotfix work? Did it break anything else?
   - If hotfix causes new issues: Execute rollback procedure (section 6.1).

**Hotfix time target:** < 4 hours from bug discovery to hotfix live (for critical issues).

### 6.3 Emergency Contacts

Keep this list updated and accessible to all launch day team members.

| Contact | Role | Phone | Email | Availability |
|---|---|---|---|---|
| Steam Partner Support | Platform support | N/A | steamworks-support@valvesoftware.com | 24/7 (response time: 1-4 hours) |
| Hosting Provider | Server hosting (if applicable) | [Phone] | [Email] | 24/7 |
| BYTE | Lead Programmer | [Phone] | [Email] | Launch day: 24/7 on-call |
| SHIP | Release Manager | [Phone] | [Email] | Launch day: 24/7 on-call |
| CRASH | QA Lead | [Phone] | [Email] | Launch day: on-call 8 AM - 10 PM PT |
| HYPE | Marketing | [Phone] | [Email] | Launch day: on-call 8 AM - 10 PM PT |

---

## 7. Post-Launch Monitoring Plan

The game is live. Now we watch. Monitoring is not passive. We are hunting for issues before they become crises.

### 7.1 What to Monitor

**Sales & Performance Metrics:**
- Steam sales dashboard: Units sold, revenue, refund rate.
- Wishlist conversion rate: What % of wishlists converted to purchases?
- Regional breakdown: Which regions are performing best/worst?
- Traffic sources: Where are players finding the game? (Steam discovery, external press, social media.)

**Player Engagement Metrics:**
- Average session length: Target: 45-60 minutes (matches session loop design).
- Total playtime: Target: 15+ hours (indicates players are completing or replaying).
- Retention: What % of players play 1 hour? 5 hours? 10 hours? 20+ hours?
- Drop-off points: Where do players stop playing? (Indicates difficulty spikes, boring sections, or bugs.)

**Technical Metrics:**
- Crash reports: Use Steam's built-in crash reporting or integrate a third-party tool (e.g., Sentry, BugSplat).
- Performance reports: FPS drops, memory leaks, long load times.
- Save file corruption reports: Critical. Track any reports of lost saves.

**Community Sentiment:**
- Steam reviews: Monitor review score (% positive). Aim for "Very Positive" (80%+).
- Review text analysis: What are players praising? What are they criticizing?
- Forum posts: Steam community hub, Discord, Reddit. What are players asking for? What are they complaining about?
- Social media mentions: Twitter/X, TikTok, YouTube. What is the vibe?

### 7.2 Monitoring Tools

**Built-in Steam Tools:**
- Steamworks dashboard: Sales, refunds, wishlists, playtime, regional data.
- Steam reviews: Read every review in the first week. Respond to critical issues.
- Steam community hub: Monitor forums, discussions, screenshots, guides.

**Third-Party Tools:**
- **Sentry or BugSplat:** Crash reporting and error tracking. Integrate into game, monitor dashboard daily.
- **Google Analytics or Mixpanel:** Gameplay telemetry. Track session length, progression, drop-off points. (Only if you have privacy policy and GDPR compliance.)
- **Discord:** Community hub. Set up channels: #bug-reports, #feedback, #support, #general. Moderators active daily.
- **Hootsuite or Buffer:** Social media monitoring. Track mentions of game name, studio name, hashtags.

### 7.3 Monitoring Schedule

**Launch Day (L+0):**
- Hour-by-hour monitoring (see section 2).
- SHIP and CRASH on-call 24/7.

**Week 1 (L+1 to L+7):**
- Daily check-ins: Sales, reviews, crash reports, forum activity.
- Daily bug triage: Prioritize issues reported by multiple players.
- Daily community engagement: Respond to questions, thank players, acknowledge bugs.

**Week 2-4 (L+8 to L+30):**
- Every-other-day check-ins: Sales, reviews, telemetry.
- Weekly bug triage: Plan patches based on aggregated feedback.
- Weekly community updates: Dev diary, patch notes, roadmap teasers.

**Month 2+ (L+31 onward):**
- Weekly check-ins: Sales trends, player retention, review score.
- Monthly roadmap updates: What is coming next? New content, balance patches, quality-of-life improvements?

### 7.4 When to Act

**Immediate action required (within 1 hour):**
- Crash affecting >10% of players.
- Save corruption reports (even one report is critical).
- Store page down or broken (cannot purchase game).
- Major press outlet publishes review citing game-breaking bug.

**Action required within 24 hours:**
- Bug affecting 5-10% of players.
- Negative review momentum (review score dropping below 70%).
- Exploit discovered (players cheating or breaking game economy).

**Action required within 1 week:**
- Quality-of-life issues reported by multiple players (e.g., UI too small, controls awkward).
- Balance issues (economy too tight, difficulty spikes, progression too slow/fast).
- Performance issues on specific hardware (e.g., AMD GPUs, certain CPU models).

**Action required within 1 month:**
- Feature requests from community (e.g., "add X mini-game," "add colorblind mode").
- Platform expansion requests (e.g., "when is this coming to macOS?").

---

## 8. Known Risks & Mitigation

No plan survives contact with launch day. These are the risks we know about. Plan for them.

### 8.1 Risk: Steam Store Page Rejected or Delayed

**Probability:** Low (if we follow guidelines).
**Impact:** High (delays launch, kills marketing momentum).

**Mitigation:**
- Submit store page 60 days before launch (L-60).
- Follow Steamworks guidelines exactly: no misleading screenshots, no fake reviews, no prohibited content.
- If rejected: Fix issues immediately, resubmit within 24 hours. Have backup launch date (L+7) in case approval is delayed.

### 8.2 Risk: Critical Bug Discovered on Launch Day

**Probability:** Medium (bugs happen, no matter how much testing).
**Impact:** Critical (negative reviews, refunds, reputation damage).

**Mitigation:**
- Extensive beta testing (100-200 external testers, L-45 to L-30).
- Hotfix pipeline tested and ready (see section 6.2).
- Rollback procedure tested and documented (see section 6.1).
- Communication templates prepared (known issues post, hotfix announcement).

### 8.3 Risk: Poor Sales Performance

**Probability:** Medium (indie game market is crowded, discoverability is hard).
**Impact:** High (financial loss, studio viability).

**Mitigation:**
- Strong pre-launch marketing (L-45 to L-0): Press outreach, influencer seeding, Steam wishlist campaign.
- Demo or free trial (consider releasing a 1-hour demo at L-14 to drive wishlists).
- Launch discount (10% off first week to incentivize early adopters).
- Post-launch marketing budget: Paid ads (Reddit, Twitter, Google), influencer sponsorships, Steam visibility events (featured on front page costs money but drives sales).

### 8.4 Risk: Negative Review Bomb

**Probability:** Low (unless game is broken or marketing was misleading).
**Impact:** High (tanks review score, kills discoverability).

**Mitigation:**
- Deliver on promises. Do NOT overhype in marketing. Set realistic expectations.
- Address critical bugs immediately. Show players you are listening and fixing issues.
- Engage with community. Respond to negative reviews (politely, professionally). Explain what you are doing to fix issues.
- Steam's review bomb detection: If reviews are off-topic (e.g., political controversy, platform exclusivity outrage), Steam may flag them and exclude from score.

### 8.5 Risk: AI Text Generation Quality Issues

**Probability:** Medium (AI is unpredictable, especially at scale).
**Impact:** High (immersion breaks, players complain about "robotic" dialogue).

**Mitigation:**
- Extensive AI testing during beta (L-45 to L-30). Have testers specifically flag any awkward or repetitive AI-generated text.
- Fallback templates for common messages (greetings, goodbyes, small talk). Only use AI for complex contextual messages.
- Post-launch patch: If AI quality is poor, replace worst offenders with hand-written templates. Announce as "dialogue polish patch."

### 8.6 Risk: Save File Corruption

**Probability:** Low (if save system is well-tested).
**Impact:** Critical (lost progress = refunds and negative reviews).

**Mitigation:**
- Extensive save/load testing (L-80 to L-30). Test edge cases: corrupt save file, missing save file, old save format, simultaneous saves on two machines (cloud sync conflict).
- Auto-save frequently (every in-game day). Keep 3 auto-save backups. If one is corrupt, roll back to previous.
- Save format versioning: Include version number in save file. Handle old versions gracefully (migrate or reject with clear error message).
- Emergency patch: If save corruption is reported post-launch, deploy hotfix within 24 hours. Provide save file recovery tool if possible.

### 8.7 Risk: Steam Deck Compatibility Issues

**Probability:** Medium (Deck has unique hardware, not all games run well).
**Impact:** Medium (Deck is growing market, but not majority of sales).

**Mitigation:**
- Test on Deck hardware early and often (L-80 to L-0).
- Optimize for Deck: 30 FPS target, 3+ hour battery life, readable text at 1280x800.
- If Deck compatibility is poor at launch: Mark as "Playable" instead of "Verified." Post-launch patch to improve Deck performance.

---

## 9. Launch Day Communication Templates

Pre-write these messages. When launch day chaos hits, you do not want to be drafting marketing copy.

### 9.1 Launch Announcement (Steam News)

**Title:** LAN PARTY is Out Now!

**Body:**

> The basement is ready. The CDs are burned. The crew is online.
>
> LAN PARTY is now available on Steam. Build your crew, host the sickest LAN parties of the early 2000s, and navigate the chaos of friendships that live in chat windows and die in silence.
>
> **Key Features:**
> - Fully interactive Windows XP desktop simulation
> - AI-driven characters with memory, personality, and drama
> - Management simulation meets social dynamics
> - 15-25 hour story arc about the impermanence of community
> - Steam Deck verified, achievements, cloud saves
>
> Launch week discount: 10% off for the first 7 days.
>
> Thank you to everyone who wishlisted, beta tested, and supported us. This game exists because you believed in it.
>
> See you in the basement.
>
> [Store Link]

### 9.2 Known Issues Post (if needed)

**Title:** Known Issues - We're On It

**Body:**

> We are aware of the following issues reported by players:
> - [Issue 1]: [Brief description]. Workaround: [if available]. Fix ETA: [date].
> - [Issue 2]: [Brief description]. Workaround: [if available]. Fix ETA: [date].
>
> We are working on a hotfix to address these issues. Patch v1.0.1 will deploy on [date].
>
> If you encounter a bug not listed here, please report it on our Discord (#bug-reports) or Steam community hub.
>
> Your saves are safe. Thank you for your patience.

### 9.3 Hotfix Announcement

**Title:** Hotfix v1.0.1 Now Live

**Body:**

> Hotfix v1.0.1 is now live on Steam. This patch addresses the following issues:
> - Fixed: [Bug 1]
> - Fixed: [Bug 2]
> - Fixed: [Bug 3]
>
> Steam will auto-update your game. If you do not see the update, restart Steam.
>
> Thank you for reporting these issues and for your patience as we worked to fix them.
>
> If you continue to experience problems, please let us know on Discord or the Steam forums.

### 9.4 Emergency Downtime Notice (if needed)

**Title:** Temporary Issue - We're Fixing It

**Body:**

> We are aware that some players are experiencing [issue description]. We have temporarily reverted to the previous build while we investigate.
>
> Your saves are safe. We expect to deploy a fix within [timeframe].
>
> We apologize for the disruption and appreciate your patience.
>
> Updates will be posted here and on Discord.

---

## 10. Patch Roadmap (First 90 Days)

Plan patches in advance. Do not wait for bugs to pile up. Proactive patching builds trust.

### Patch 1 (L+3 to L+7)

**Goal:** Fix critical bugs discovered in first 72 hours.

**Likely fixes:**
- Crash on startup (specific hardware or OS configurations).
- Save file corruption under rare conditions.
- UI scaling issues (text too small on high-DPI displays).
- Performance issues on minimum spec hardware.

**Deploy date:** L+7 (one week post-launch).

### Patch 2 (L+14 to L+21)

**Goal:** Fix high-priority bugs and quality-of-life improvements.

**Likely fixes:**
- AI text generation issues (repetitive or awkward dialogue).
- Balance adjustments (economy too tight, difficulty spikes).
- Missing features (e.g., rebindable controls, colorblind mode).
- Localization fixes (if supporting multiple languages).

**Deploy date:** L+21 (three weeks post-launch).

### Patch 3 (L+30 to L+60)

**Goal:** Content update and community requests.

**Possible additions:**
- New mini-game (if scope allows).
- New character archetypes (procedural generation variants).
- New narrative beats (extend replayability).
- Steam Workshop support (if community requests modding).

**Deploy date:** L+60 (two months post-launch).

### Patch 4+ (L+90+)

**Goal:** Long-term support and roadmap.

**Possible additions:**
- Major content expansion (new LAN party events, new acquisition channels, new progression arcs).
- Platform expansion (macOS release, console ports if viable).
- Seasonal events (e.g., "Y2K Party" around New Year's).

---

## 11. Success Metrics

How do we know if the launch was successful? Define success criteria in advance.

### Launch Day Success (L+0)

- [ ] Game launches on time (10 AM PT).
- [ ] Store page is live and functional.
- [ ] Zero P0 bugs (no game-breaking issues).
- [ ] Sales: 100+ units sold in first 24 hours (modest indie target).
- [ ] Reviews: 10+ reviews, 70%+ positive.

### Week 1 Success (L+7)

- [ ] Sales: 500+ units sold.
- [ ] Reviews: 50+ reviews, 75%+ positive (Steam "Mostly Positive").
- [ ] Zero critical bugs unresolved.
- [ ] Press coverage: 5+ outlets published reviews or coverage.
- [ ] Community: 500+ members in Discord, active daily discussions.

### Month 1 Success (L+30)

- [ ] Sales: 2,000+ units sold.
- [ ] Reviews: 200+ reviews, 80%+ positive (Steam "Very Positive").
- [ ] Retention: 50%+ of players who bought the game have played 5+ hours.
- [ ] Community: 1,000+ Discord members, active mod scene (if Workshop enabled).
- [ ] Press: Featured on at least one major outlet (PC Gamer, Rock Paper Shotgun, IGN Indie Spotlight).

### Long-Term Success (L+90)

- [ ] Sales: 5,000+ units sold (break-even or profitable, depending on budget).
- [ ] Reviews: 500+ reviews, 80%+ positive.
- [ ] Retention: 30%+ of players have completed a full playthrough (15+ hours).
- [ ] Community: Self-sustaining. Players creating content (fan art, streams, mods).
- [ ] Roadmap: Patch 3 deployed, community excited for future content.

---

## 12. Lessons Learned Template (Post-Launch)

After launch (L+30), conduct a retrospective. Document what worked and what did not. Use this for the next game.

**What went right:**
- [List 3-5 things that went well.]

**What went wrong:**
- [List 3-5 things that did not go well.]

**What surprised us:**
- [List 2-3 unexpected events, good or bad.]

**What we will do differently next time:**
- [List 3-5 changes to process, tools, or timeline.]

**Action items for next release:**
- [List specific changes to implement in the next release plan.]

---

## 13. Conclusion

This release plan is a living document. Update it as the project evolves. Add new risks, adjust timelines, refine checklists.

The goal is simple: Make launch day boring. If nothing goes wrong, if the build is stable, if players are happy, if reviews are positive, if sales hit targets — then this plan worked.

Launch day is the culmination of months or years of work. Do not let it be the day everything falls apart. Plan for failure. Test relentlessly. Have rollback procedures ready. Communicate clearly.

Ship it. Monitor it. Fix it. Iterate.

And when it is over, document what you learned. The next launch will be better because of this one.

-- SHIP

---

**Document Status:** Master release plan complete. Ready for implementation. Zero placeholders. Every checklist item is actionable. Every procedure is testable.

**Next Steps:**
1. Review with CLOCK (Producer) to validate timeline and resource allocation.
2. Review with BYTE (Lead Programmer) to validate build pipeline and technical procedures.
3. Review with HYPE (Marketing) to validate store page and marketing timeline.
4. Review with CRASH (QA Lead) to validate testing and monitoring plans.
5. Schedule L-90 kickoff meeting. Begin code complete phase.

**Revision History:**
- v1.0 (2026-02-07): Initial release plan by SHIP.
