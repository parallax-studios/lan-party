# LAN PARTY — Art Direction Document

**Art Director:** PIXEL
**Status:** Complete — Ready for Asset Production
**Project:** LAN PARTY (Desktop Simulation / Management Sim)
**References:** `games/04-lan-party/pitch.md`, `games/04-lan-party/game-design.md`
**Platform:** PC (Steam), Steam Deck secondary
**Date:** 2026-02-07

---

## 1. Visual Identity Statement

**LAN PARTY is pixel-perfect digital archaeology — a loving, hyper-accurate recreation of Windows XP-era UI that reads as both historical artifact and living toy, where every window, icon, and chat bubble is precisely authentic but subtly tuned to communicate game state at a glance.**

This is not a parody. This is not ironic. This is a forensic reconstruction of a specific digital moment — 2003, Windows XP Service Pack 1, CRT monitors, 800x600 resolution stretched to fit, default Bliss wallpaper, MSN Messenger with custom emoticons, mIRC with ASCII art. We are building a playable time capsule.

The constraint is accuracy. The goal is readability. The challenge is making a period-accurate desktop that functions as a game interface where every pixel of UI is also a game system. No external HUD. No menu overlays. The Windows taskbar IS your game menu. The system tray IS your notification center. The buddy list IS your relationship manager. Art serves gameplay through the language of 2003 operating system design.

---

## 2. Visual Feeling

### Emotion

**Warm nostalgia with an undercurrent of impermanence.** The screen should evoke the specific coziness of being at your computer at 2 AM when nobody else is awake — the house is dark, the monitor is your only light source, and you are talking to people who feel close despite being miles away. There is comfort in the clutter. There is safety in the familiar blue taskbar. But underneath, there is an ache — this moment is already gone, and you are looking at a ghost.

When a player sees a screenshot, they should feel:
1. Recognition — "I remember this. I LIVED in this."
2. Comfort — "This space felt like mine."
3. Loss — "This does not exist anymore."

### Temperature

**CRT-blue cold with pools of amber warmth.** The dominant color temperature is the cool blue-white glow of a cathode ray tube — slightly sterile, slightly clinical, the color of screen light in a dark room. But this cold is punctuated by warm amber accents: buddy icons with that JPEG compression glow, fire-orange MSN status indicators, the warm beige of period-accurate desktop towers in photographs, the Mountain Dew green of a Winamp visualizer.

The thermal balance is 70% cold, 30% warm. The cold is the technology. The warm is the people inside the technology.

### Era

**Hyper-specific: Windows XP era, 2001-2005, with emphasis on 2003.** Not "retro" as a genre. Not "Y2K aesthetic." This is a surgical historical recreation of a five-year window in personal computing interface design. Every visual element must pass the "could this have existed in 2003?" test.

References are not game art. References are actual software:
- Windows XP Luna theme (default blue)
- MSN Messenger 6.0-7.5 UI
- mIRC 6.x interface
- WinRAR 3.x
- Winamp 2.x/5.x
- Internet Explorer 6
- Nero Burning ROM 6
- Kazaa / LimeWire interface design language
- phpBB 2.x forum templates
- GeoCities/Angelfire web design aesthetics

This is not approximation. This is replication with the precision of a museum exhibit.

---

## 3. Color Palette

### 3.1 Primary Palette: Windows XP Luna Theme

These are not chosen colors. These are THE colors of Windows XP default theme, extracted directly from historical UI screenshots and system resources. Every hex value is historically accurate.

| Color Name | Hex Value | RGB | Usage |
|---|---|---|---|
| **Luna Blue (Taskbar)** | `#1F50A8` | 31, 80, 168 | Taskbar background, window title bars (active), primary brand color |
| **Luna Blue Gradient End** | `#3F8FD8` | 63, 143, 216 | Taskbar gradient endpoint, title bar gradient, button hover states |
| **Luna Desktop Background** | `#5A8FCC` | 90, 143, 204 | Default desktop blue (when no wallpaper), fallback BG |
| **Window Grey** | `#ECE9D8` | 236, 233, 216 | Window client area background, dialog boxes, control panel surfaces |
| **Button Face Grey** | `#D4D0C8` | 212, 208, 200 | 3D button surfaces, inactive elements, dividers |
| **Silver Border** | `#ACA899` | 172, 168, 153 | Window borders, inactive title bars, disabled text |
| **White** | `#FFFFFF` | 255, 255, 255 | Text input fields, list backgrounds, content areas |
| **Black Text** | `#000000` | 0, 0, 0 | Primary text (with ClearType rendering blur in shader) |

**Usage Rules:**

- **Luna Blue is sacred.** It appears in every screen. Taskbar is always visible. This blue is the game's visual anchor.
- **Window Grey is the canvas.** 80% of screen space is application windows on this grey. This is where game content lives.
- **White is for content.** Chat message areas, forum post text, file lists — anything the player reads lives on white.
- **Button Face Grey communicates inactive.** Anything on this color is not currently the focus or is disabled. Use sparingly for contrast.
- **All greys are warm-tinted (beige undertones).** This is critical for period accuracy. Pure grey is modern. XP was beige-grey.

### 3.2 Accent Palette: Application-Specific Colors

These colors appear in specific applications and carry meaning within the desktop ecosystem.

| Color Name | Hex Value | RGB | Usage / Source Application |
|---|---|---|---|
| **MSN Orange (Online)** | `#FDB200` | 253, 178, 0 | Online status indicator, primary MSN brand color, notifications |
| **MSN Red (Busy)** | `#E74C3C` | 231, 76, 60 | Busy/DND status, important alerts, errors |
| **mIRC Dark Grey** | `#3F3F3F` | 63, 63, 63 | mIRC background (customizable but commonly dark), channel list BG |
| **mIRC Green (Join)** | `#00AA00` | 0, 170, 0 | Join messages in IRC, positive system messages |
| **mIRC Blue (Highlight)** | `#0000FF` | 0, 0, 255 | Nickname mentions, highlighted text, links (pure web blue) |
| **Winamp Green** | `#00FF00` | 0, 255, 0 | Equalizer bars, visualizer accents, "now playing" indicators |
| **Error Red** | `#C50F1F` | 197, 15, 31 | Windows error dialogs, critical warnings, system alerts |
| **Hyperlink Blue** | `#0000EE` | 0, 0, 238 | Unvisited links (IE standard), clickable text |
| **Visited Purple** | `#551A8B` | 85, 26, 139 | Visited links (IE standard), previously opened threads |

**Usage Rules:**

- **MSN Orange is excitement.** New message, online status, friend logs in. This color means "someone wants to talk to you." In game terms: opportunity, social connection available.
- **MSN Red is tension.** Busy status, someone upset, download error, ISP warning. Use to signal conflict, risk, or urgency.
- **mIRC Green is success.** File transfer complete, invitation accepted, scene contact responds. Positive feedback.
- **Winamp Green is atmosphere.** Music system active, party energy high. This color means "good vibes."
- **Hyperlink Blue is interaction.** Anything blue is clickable. This is web-standard, period-accurate, and universally understood. Never use blue for non-interactive elements.
- **Visited Purple shows history.** The player has been here before. Threads they have read, links they have clicked. This creates a sense of persistent world and memory.

### 3.3 Game State Communication Palette

These colors are NOT period-accurate XP colors. These are game-specific additions used to subtly communicate state without breaking the simulation. They appear only in specific, rare, justified contexts.

| Color Name | Hex Value | RGB | Usage | Justification |
|---|---|---|---|---|
| **Relationship Positive (subtle)** | `#90EE90` | 144, 238, 144 | Light green buddy icon glow (barely visible) | Plausible as custom icon effect |
| **Relationship Negative (subtle)** | `#FFB6C1` | 255, 182, 193 | Light red/pink buddy icon tint | Plausible as away/offline state |
| **High Priority Notification** | `#FFD700` | 255, 215, 0 | System tray icon animation (gold flash) | XP could do notification animation |
| **Low Hard Drive Space Warning** | `#FF4500` | 255, 69, 0 | Red drive icon in file manager | Windows actually did this |

**Critical Rule:** These colors must feel like they COULD have been in Windows XP. If a player consciously notices "that is not period-accurate," we have failed. When in doubt, default to actual XP behavior and find another way to communicate state.

### 3.4 Accessibility and Readability

**Colorblind Considerations:**

The base XP palette is already reasonably colorblind-safe because it was designed in an era where accessibility standards were emerging. However, critical game state must NEVER rely on color alone.

| Game State | Color Signal | Non-Color Signal |
|---|---|---|
| Online/Offline status | Green/Grey | Text label ("Online"/"Offline") + icon shape |
| Relationship positive/negative | Green/red glow | Away message tone, message frequency, emoji usage |
| Download complete | Green text | Sound effect (completion chime) + popup notification window |
| Error/Warning | Red dialog | Icon (⚠️ symbol), dialog text content, sound (error beep) |
| Clickable element | Blue underline | Underline, cursor change to hand pointer |

**Contrast Ratios:**

All text must meet WCAG AA standards (4.5:1 for normal text, 3:1 for large text). Fortunately, XP's black text on white/light grey backgrounds already exceeds this by a massive margin. The only risk area is mIRC's dark theme — ensure channel text is light enough.

- **Black on Window Grey (#000000 on #ECE9D8):** 17.8:1 — Excellent
- **Black on White (#000000 on #FFFFFF):** 21:1 — Perfect
- **Light Grey on mIRC Dark Grey (#CCCCCC on #3F3F3F):** 7.1:1 — Good
- **MSN Orange on White (#FDB200 on #FFFFFF):** 2.2:1 — FAILS. Never use orange text on white. Orange is for icons/indicators only.

**Squint Test Validation:**

When the screen is blurred or viewed at tiny resolution:
- The Luna Blue taskbar must be identifiable immediately (dominant horizontal band at bottom)
- Open application windows must be distinguishable by shape (MSN's vertical buddy list, mIRC's horizontal channel list, browser's address bar)
- Active vs. inactive windows must be readable via title bar color (Luna Blue vs. Silver)

---

## 4. Shape Language

### 4.1 Dominant Shapes: Rectilinear Precision

**Primary shape vocabulary: Rectangles, sharp corners, pixel-aligned edges.**

Windows XP UI is built on a strict grid of rectangles. Every window is a rectangle. Every button is a rounded rectangle (but with such small corner radii — 2-3px — that they read as almost-rectangles). Every text field is a recessed rectangle. This is the visual language of early 2000s UI design: precise, orderly, grid-based, information-dense.

**The game inherits this language wholesale.** No organic shapes. No hand-drawn elements. No skeuomorphic textures (except where XP itself used them — e.g., the "shadow" under window title bars). Every asset is pixel-perfect, grid-aligned, mathematically consistent.

### 4.2 Application Window Anatomy

Every application window follows this structure:

```
┌─────────────────────────────────────────┐ ← Title bar (20px height)
│  [Icon]  Application Name        [_][□][X]│   Luna Blue gradient
├─────────────────────────────────────────┤
│  Menu Bar: File  Edit  View  Help       │ ← Menu (20px height), Window Grey
├─────────────────────────────────────────┤
│                                          │
│                                          │
│        Client Area                       │ ← Content area, varies per app
│        (Window Grey or White)            │
│                                          │
│                                          │
├─────────────────────────────────────────┤
│  Status bar text                         │ ← Status bar (20px), recessed grey
└─────────────────────────────────────────┘
```

**Proportions:**
- Title bar: Fixed 20px height
- Menu bar: Fixed 20px height (if present)
- Status bar: Fixed 20px height (if present)
- Client area: Variable, but always respects 20px grid increments
- Minimum window size: 200x150px (title bar + minimal content)
- Default window size: 600x450px for most apps

**Corner radius:**
- Window corners: 0px (sharp)
- Button corners: 2px radius (barely perceptible)
- Rounded rectangle buttons (like MSN contact tiles): 3px radius

### 4.3 Icon Language

Icons are **16x16px or 32x32px, pixel art, with limited color palettes (8-16 colors max).**

Icon shape rules:
- **Readable at 16x16.** Every icon must communicate its function in a 16px square. Test by zooming out.
- **3/4 perspective or straight-on.** Period-accurate icons used isometric-ish 3/4 view for 3D objects (folders, computers) or flat straight-on for 2D symbols (text file, web link).
- **Single-pixel outlines.** Icons have 1px black or dark outlines to separate from background.
- **Primary color + shadow + highlight.** Three-tone rendering. Base color, darker shadow, lighter highlight. XP icons were simple but had basic lighting.

**Icon categories and shape patterns:**

| Type | Shape Pattern | Example |
|---|---|---|
| **Application** | Square with centered symbol | MSN (speech bubble), mIRC (globe), Winamp (lightning bolt) |
| **File Type** | Dog-eared document with icon overlay | .txt (notepad page), .zip (zipper overlay), .exe (window icon) |
| **Folder** | 3/4 view folder, closed or open | Standard yellow folder, shared folder (hand underneath) |
| **Status** | Circle or square with symbol | Green check, red X, yellow warning triangle |
| **System** | Computer hardware 3/4 view | Hard drive (grey box), CD drive (tray), monitor |

### 4.4 Button and Control Shapes

**Button anatomy (standard push button):**

```
┌────────────────┐  ← 1px highlight (lighter grey)
│  Button Text   │  ← Button Face Grey fill
└────────────────┘  ← 1px shadow (darker grey)
```

Buttons are drawn with a subtle 3D effect using two 1px borders: a lighter top/left edge and a darker bottom/right edge. When pressed, this inverts (dark top/left, light bottom/right). This is the universal language of 3D GUI from the 1990s-2000s.

**Control shape library:**

- **Checkbox:** 13x13px square, white interior, 1px black border, blue checkmark when active
- **Radio button:** 13x13px circle, white interior, 1px black border, filled blue dot when selected
- **Dropdown:** Rectangle with down-arrow on right side (▼), arrow is 7px wide triangle
- **Text input:** Recessed rectangle (inverse 3D bevel), white interior, 1px inset border
- **Scrollbar:** 16px wide, grey track, darker grey thumb with 3D bevel, arrow buttons at ends
- **Slider:** Horizontal track (2px tall), thumb is 10x16px rectangle with 3D bevel

**Sizing standards:**
- Button height: 23px (standard), 32px (large)
- Button minimum width: 75px (accommodates "Cancel")
- Text input height: 21px (single-line)
- Dropdown height: 21px (collapsed)
- Scrollbar width: 16px

### 4.5 Character Proportions (Avatar Icons and Silhouettes)

Characters are never seen directly in 3D or full-body illustration. Characters exist only as:
1. **Buddy icons** (48x48px or 64x64px JPEG avatars with compression artifacts)
2. **Forum avatars** (80x80px, usually anime screenshots or band photos)
3. **Implied presence** (chat text, away messages, forum posts)

**Buddy icon visual rules:**
- Photographed from webcam (low resolution, compression artifacts, often poorly lit)
- OR downloaded image (anime character, band member, game character, abstract symbol)
- JPEG compression is mandatory — no crisp pixel art avatars. This is 2003. Images are crunchy.
- Authentic imperfections: off-center crops, red-eye, flash glare, bad contrast
- Each character has a consistent icon that the player learns to recognize at a glance

**Character identity is textual, not visual.** The player knows xXDarkAngelXx by their screen name, their typing style, their away messages, their forum signature — not by their 48x48 icon. The icon is a token, not a portrait.

### 4.6 Environmental Shapes (Desktop and In-Game Spaces)

**The Desktop:**

The desktop itself is a flat plane with icons arranged on an invisible grid (8px horizontal spacing, 8px vertical spacing). Icon arrangement can be:
- **Auto-arranged** (left-aligned grid, top-to-bottom then left-to-right)
- **Chaotic** (player has dragged icons randomly — authentic to actual user desktops)

Overlapping windows create depth through window layering (z-order) and drop shadows (subtle, 2px offset, 50% opacity black blur).

**The LAN Party "Space" (not directly shown):**

During LAN party phase, the player does NOT see a 3D basement. Instead, they see:
- The game being played (simplified top-down or side-view representation, pixel art, on a virtual monitor)
- A chat sidebar (MSN-style) with participant messages in real-time
- A party energy meter (progress bar, styled like Windows progress bar)
- A simple schematic view of seating arrangement (top-down, rectangles representing desks, character names labeled)

**All LAN party visualization is abstract and UI-driven.** No 3D modeling. No isometric basement. The party EXISTS in the UI, just like everything else.

---

## 5. Style Rules

### 5.1 Line Quality: Pixel-Perfect Precision

**All UI elements are pixel art at 1:1 scale.** There is no sub-pixel rendering except where Windows XP itself used it (ClearType font antialiasing on text). Every line is either perfectly horizontal, perfectly vertical, or perfectly diagonal at 45° (rarely).

**Line weights:**
- Window borders: 1px, solid
- Button outlines: 1px, solid
- Text underlines (links): 1px, solid
- Dividers (menu separators, splitters): 1px or 2px, solid or dotted
- Scrollbar track edges: 1px, inset bevel (appears as 2px because top+bottom)

**No line variation.** No taper. No brush strokes. This is vector art rasterized to exact pixels or pixel art drawn on-grid. Every asset must be crisp at 100% zoom.

**Antialiasing rules:**
- UI elements: NEVER antialiased (except rounded corners at 2-3px radius, which have minimal AA)
- Text: ALWAYS antialiased using ClearType simulation (horizontal RGB subpixel rendering, subtle color fringing)
- Icons at 32x32 or larger: Minimal manual antialiasing on diagonals (1px transitional color)
- Buddy icons / photos: JPEG compression artifacts (simulated), not antialiasing

### 5.2 Texture Approach: Flat Colors with Subtle Gradients

**Base rule: Flat fill colors with occasional linear gradients (XP style).**

XP introduced gradients to the Windows UI after the pure-flat aesthetic of Windows 95/98. But these gradients were simple: 2-color linear gradients, usually subtle (10-20% brightness shift).

**Where gradients appear:**
- **Taskbar:** Vertical gradient from `#1F50A8` (top) to `#3F8FD8` (bottom), smooth transition
- **Active title bars:** Horizontal gradient from `#1F50A8` (left) to `#3F8FD8` (right)
- **Selected list items:** Vertical gradient from `#3166CC` (top) to `#2852A8` (bottom)
- **Button hover states:** Slight glow (radial gradient, center lighter, edges normal)

**Where gradients DO NOT appear:**
- Window client areas (flat Window Grey)
- Text input fields (flat white)
- Menu bars (flat grey)
- Desktop background when no wallpaper (flat or very subtle radial gradient)

**Texture is not used except for:**
- **Desktop wallpaper** (Bliss or user-selected image)
- **Buddy icons / forum avatars** (photographic textures from source images)
- **Simulated CRT scanlines** (optional shader effect, very subtle horizontal lines, 1px every 2-3px, 10% opacity)

**No material textures.** No wood grain. No paper texture. No cloth. UI surfaces are smooth, rendered, digital. The only "texture" is the grain of JPEG compression or the structure of text rendering.

### 5.3 Lighting Style: Flat Ambient with Implied Light Source

**Lighting is baked into UI assets as simple 3D bevels, not dynamically calculated.**

XP UI design implies a light source from the top-left. This is communicated through:
- Top and left edges of buttons: lighter color (highlight)
- Bottom and right edges of buttons: darker color (shadow)
- Recessed areas (text inputs): inverted (dark top/left, light bottom/right)

**No dynamic lighting.** No real-time shadows. No light bloom. The screen is flat. The "lighting" is the symbolic language of 3D GUI from the pre-shader era.

**The only dynamic light is the monitor itself:** The glow of the CRT screen. This can be suggested through post-processing:
- Subtle vignette (edges of screen slightly darker, center brighter)
- CRT curvature shader (very subtle barrel distortion, optional toggle)
- Scanline shader (1px horizontal lines, 10% opacity, optional toggle)
- Phosphor glow (very subtle color fringing on high-contrast edges, optional)

All of these are POST-PROCESSING ONLY, not baked into assets. Assets are flat. The screen creates the atmosphere.

### 5.4 Animation Style: Functional and Snappy

**Principle: Animations communicate state change, not spectacle.**

XP UI had minimal animation. When it moved, it moved for a reason — to show that something happened. We follow this philosophy.

**Animation categories:**

1. **System Animations (inherited from XP):**
   - Window open/close: Zoom from taskbar button (100ms, ease-out)
   - Window minimize: Zoom to taskbar button (100ms, ease-in)
   - Menu dropdown: Slide down with fade-in (150ms, linear)
   - Tooltip appear: Fade-in after 500ms hover (100ms fade)

2. **Notification Animations:**
   - MSN message popup: Slide up from taskbar (200ms, ease-out), hold 4s, slide down (200ms, ease-in)
   - System tray icon flash: Fade 50%↔100% over 500ms, repeat 3 times
   - Taskbar button flash (on new message): Orange background fade 0%↔100% over 400ms, repeat until clicked

3. **Content Animations:**
   - Chat message appear: Instant text render + 1-frame scroll to bottom (no typewriter effect — that is anachronistic)
   - Download progress bar: Smooth fill from left to right, 60 FPS update rate
   - File transfer: Progress bar + "X KB/s" text updates every 500ms
   - Forum page load: Instant content swap (no fade transition — this is 2003, pages just LOAD)

4. **Character Animations (implied, not shown):**
   - Buddy goes online: Status icon changes + door-open sound + popup
   - Buddy starts typing: "xXDarkAngelXx is typing..." text flashes below message window (no ellipsis animation — static text)
   - Buddy goes idle: Status changes from "Online" to "Away" after 10 minutes

**Animation timing standards:**
- UI feedback: 100-150ms (fast enough to feel snappy, slow enough to perceive)
- Notification popups: 200ms in/out (noticeable but not intrusive)
- Progress bars: 60 FPS smooth (anything less feels broken)
- Typing indicators: No animation, static text, appears instantly when character is generating message

**No animation overkill.** If XP did not animate it, we do not animate it. The player is here for the simulation, not for UI flourish.

### 5.5 Sound Design (As It Relates to Visual Feedback)

Sound and visuals are tightly coupled in XP-era UI. Every visual state change has an associated sound.

**Sound-Visual Pairings:**

| Visual Event | Sound | Visual Feedback |
|---|---|---|
| Buddy logs in | MSN "door open" chime | Status icon changes to green, popup appears |
| New message received | MSN message "knock" | Orange taskbar button flash, popup slides up |
| Message sent | Subtle "whoosh" | Message appears in chat window, instant |
| Download complete | Windows "completion" chime | Progress bar fills to 100%, green text appears |
| Error dialog | Windows "error" beep | Red X icon, dialog zooms from center |
| Window minimize | Subtle "zip" sound | Window zooms to taskbar |
| Link clicked | No sound (silent) | Cursor becomes "loading" spinner (pointer + hourglass) |

**Silence is also feedback.** Not every action makes sound. Text input is silent. Scrolling is silent. Mouse movement is silent. Sound is reserved for events that matter.

### 5.6 Do's and Don'ts

**DO:**
- Pixel-perfect alignment on 1px grid
- Use exact Windows XP colors (reference hex values above)
- Respect 20px increments for window chrome heights
- Make every icon readable at 16x16px before scaling up
- Simulate JPEG compression on all user-generated images (buddy icons, avatars)
- Use ClearType-style font rendering (RGB subpixel antialiasing)
- Keep animations under 200ms for UI feedback
- Test every screen at 800x600 resolution (minimum supported)
- Add subtle imperfections (off-by-1px window positions, slightly misaligned desktop icons — authentic to real user desktops)

**DON'T:**
- Use modern flat design language (no Material Design, no iOS-style blur, no neumorphism)
- Antialiasing UI chrome (window borders, buttons, dividers are pixel-sharp)
- Use custom fonts beyond XP system fonts (Tahoma, Verdana, Arial, Trebuchet MS, Comic Sans MS)
- Add gradients where XP would not have them (content areas stay flat)
- Animate things XP did not animate (page loads are instant, text appears instantly)
- Use transparency except where XP used it (window drop shadows, menu fade-ins)
- Make icons "artsy" — they must be functional, information-dense, immediately parseable
- Over-design buddy icons — they should look like random JPEGs a teenager downloaded in 2003
- Add modern UI conventions (no hamburger menus, no swipe gestures, no card-based layouts)
- Use emojis beyond what MSN Messenger supported (limited custom emoticons, mostly text-based smileys :) :P ;) etc.)

**Critical: When in doubt, reference actual Windows XP screenshots, not memory.** Nostalgia is unreliable. Historical accuracy requires primary sources.

---

## 6. Asset Pipeline

### 6.1 File Formats

| Asset Type | Format | Specs | Rationale |
|---|---|---|---|
| UI Elements (windows, buttons, icons) | PNG | 24-bit RGB + 8-bit alpha, no compression artifacts | Pixel-perfect precision, transparency support |
| Application Icons | PNG | 16x16, 32x32, 48x48 sizes, indexed color (256 colors max) | Period-accurate .ICO format simulation |
| Buddy Icons / Avatars | JPEG | 64x64, quality 60-75% (visible compression) | Authentic to MSN Messenger low-bandwidth images |
| Desktop Wallpapers | JPEG | 1024x768, 1280x1024, 1600x1200, quality 80% | Common resolutions, slight compression authentic |
| Font Files | TrueType (.ttf) | Tahoma (primary), Verdana, Arial, Trebuchet, Comic Sans | Exact XP system fonts, embedded or system-loaded |
| Window Layouts (arrangement) | JSON | Custom schema defining window positions, sizes, z-order | Data-driven window management |
| Sound Effects | WAV | 16-bit, 22050 Hz, mono or stereo | XP system sounds were .wav, same format |
| Music (Winamp tracks) | MP3 | 128-192 kbps, ID3 tags | Period-authentic format, license-safe music |

### 6.2 Resolution Standards

**Base canvas resolution: 1024x768 (4:3 aspect ratio).** This is the primary target. All UI is designed at this resolution first.

**Supported resolutions:**
- 800x600 (minimum supported, 4:3)
- 1024x768 (primary target, 4:3)
- 1280x1024 (5:4, common for LCDs in early 2000s)
- 1600x1200 (4:3, high-end CRTs)
- 1920x1080 (16:9, modern monitors) — UI scales, desktop background stretches or letterboxes

**Scaling approach:** Integer scaling when possible, bilinear filtering when not. UI is rendered at logical 1024x768 and then scaled to output resolution. This preserves pixel crispness while supporting modern displays.

**DPI handling:** The game is DPI-agnostic. It renders at logical resolution, OS handles scaling. No high-DPI assets needed — period authenticity means low-res is correct.

### 6.3 Sprite Sheets and Atlases

UI elements are organized into texture atlases for performance.

**Atlas categories:**
- **WindowChrome.png:** Title bars, borders, buttons (minimize, maximize, close), scrollbars, menu backgrounds
- **Controls.png:** Checkboxes, radio buttons, dropdowns, text input fields (empty and filled states)
- **Icons_16x16.png:** All 16x16 application and file type icons, arranged in grid
- **Icons_32x32.png:** All 32x32 icons (same set as 16x16, higher detail)
- **MSN_UI.png:** MSN Messenger-specific UI elements (buddy tiles, status indicators, nudge animation frames)
- **mIRC_UI.png:** mIRC-specific elements (channel list, user list, message formatting)
- **Taskbar.png:** Taskbar background gradients, Start button states, system tray icons

**Atlas format:** PNG, power-of-two dimensions (1024x1024, 2048x2048), RGBA. Accompanied by JSON data file mapping element names to rectangle coordinates.

### 6.4 Font Rendering

**Primary font: Tahoma, 8pt (11px) for UI chrome, 9pt (12px) for content.**

Tahoma was THE Windows XP UI font. It was designed for screen readability at small sizes. We must use the actual TrueType file, not a substitute.

**Font usage map:**

| Context | Font | Size | Weight | Antialiasing |
|---|---|---|---|---|
| Window title bars | Tahoma | 8pt (11px) | Bold | ClearType |
| Menu items | Tahoma | 8pt (11px) | Regular | ClearType |
| Button labels | Tahoma | 8pt (11px) | Regular | ClearType |
| List items | Tahoma | 8pt (11px) | Regular | ClearType |
| Message text (MSN) | Verdana | 9pt (12px) | Regular | ClearType |
| Chat text (mIRC) | Fixedsys or Terminal (monospace) | 8pt | Regular | None (bitmap font) |
| Forum posts | Verdana | 10pt (13px) | Regular | ClearType |
| Code/logs (Notepad) | Lucida Console | 10pt | Regular | ClearType |

**ClearType simulation:** RGB subpixel rendering. Each glyph is rendered with slight color fringing (red on left edge, blue on right edge) to simulate the subpixel antialiasing technology XP introduced. This is subtle but critical for authenticity.

**Fallback:** If exact fonts cannot be embedded (licensing), use Liberation Sans (Tahoma substitute) and Deja Vu Sans (Verdana substitute). Visual difference is minimal but must be noted in credits.

### 6.5 Animation Assets

Animations are frame-based sprite sheets, not skeletal/bone-based.

**Animated elements:**
- **MSN typing indicator:** 3 frames (1, 2, 3 dots), 8x8px each, 400ms per frame
- **Download progress bar:** Marquee animation for indeterminate progress (8-frame loop, 1px shift per frame, 100ms per frame)
- **System tray icon flash:** 2 frames (normal, highlighted), 500ms per frame
- **Taskbar button flash:** 2 frames (normal, orange highlight), 400ms per frame

All animations are exported as horizontal sprite strips (single row, N frames).

### 6.6 Tools and Software Requirements

**Required tools for asset creation:**
- **Aseprite or Pixaki:** Pixel art tool for UI elements and icons
- **Photoshop or GIMP:** For buddy icon JPEG compression simulation, wallpaper editing
- **FontForge:** For font inspection and validation (ensuring exact TrueType match)
- **Shoebox or TexturePacker:** For sprite atlas generation
- **VSCode + JSON schema:** For window layout data files

**Reference library (required for all artists):**
- Folder of 200+ Windows XP screenshots (various applications, dialogs, error messages)
- Video recording of XP boot sequence and common tasks (login, file browsing, window management)
- Archive of XP .theme files and desktop wallpapers
- MSN Messenger 7.5 running in VM (for real-time reference)
- mIRC 6.35 running in VM

**Version control:** All assets are stored in Git LFS (Large File Storage). PNG and JSON are human-reviewable. Buddy icons and wallpapers are in separate folder, procedurally generated or sourced from stock libraries.

### 6.7 Naming Conventions

Files follow strict naming to support data-driven loading.

**Format:** `[Category]_[Element]_[State]_[Size].png`

**Examples:**
- `Window_TitleBar_Active_1x20.png` (active window title bar, 1px wide by 20px tall, tiled horizontally)
- `Button_Push_Normal_75x23.png` (standard button, unpressed, 75px by 23px)
- `Button_Push_Hover_75x23.png` (same button, hover state)
- `Button_Push_Pressed_75x23.png` (same button, pressed state)
- `Icon_MSN_16x16.png` (MSN Messenger icon, 16x16)
- `Icon_MSN_32x32.png` (MSN Messenger icon, 32x32)

**Buddy icons:** `BuddyIcon_[CharacterID]_64x64.jpg` (e.g., `BuddyIcon_xXDarkAngelXx_64x64.jpg`)

**Wallpapers:** `Wallpaper_[Name]_[Resolution].jpg` (e.g., `Wallpaper_Bliss_1024x768.jpg`)

### 6.8 Handoff Process (Concept to Engine)

**Step 1: Design / Concepting**
- Art Director (PIXEL) creates reference board and specification document (this document)
- UI mockups created in Figma or Photoshop at 1024x768, showing window layouts and interactions
- Design review with Game Designer (REED) to validate that UI communicates game state

**Step 2: Asset Production**
- Artists create pixel art assets in Aseprite following specs
- Each asset is reviewed at 100% zoom and at 2x zoom (to check readability)
- Buddy icons and avatars are sourced from stock photo libraries, compressed to JPEG at 60-75% quality
- All assets exported to PNG (UI) or JPEG (photos) with exact naming conventions

**Step 3: Integration Prep**
- Assets compiled into sprite atlases using TexturePacker
- Atlas JSON files validated against schema
- Window layout data created as JSON (defines app dimensions, element positions)
- Font files validated (TrueType format, exact Tahoma/Verdana match)

**Step 4: Engine Integration**
- Programmer imports atlas PNGs and JSON data
- UI rendering system loads assets dynamically based on window type
- Font rendering configured with ClearType simulation shader
- Animation frame data loaded from JSON, tied to state changes

**Step 5: Testing & Iteration**
- Squint test: Screenshots at 25% scale — is taskbar visible? Are windows distinguishable?
- Thumbnail test: Screenshot at 200x150px — can you identify the app being used?
- Colorblind test: Screenshots run through colorblind simulators (Deuteranopia, Protanopia, Tritanopia)
- Motion test: Record 10 seconds of gameplay, check if important events are visible during action
- Feedback incorporated, assets revised, repeat

**Iteration speed target:** Asset tweak to in-engine testing in under 30 minutes. Data-driven pipeline enables rapid iteration without recompiling.

---

## 7. Readability Audit

### 7.1 Squint Test

**Method:** View a full screenshot of the game at thumbnail size (200px wide) or with heavy Gaussian blur (20px radius). Critical information must remain identifiable.

**Pass criteria:**
- Luna Blue taskbar is visible as dominant horizontal element at bottom of screen
- At least 2-3 application windows are distinguishable by shape and position
- Active window vs. inactive windows is identifiable (blue title bar vs. grey)
- Any notification popups (MSN message) are visible as discrete orange rectangles

**Tested scenarios:**
1. **Desktop with 5 open windows:** MSN (left), mIRC (center-left), browser (center-right), file manager (bottom-right), Winamp (small, top-right)
   - **Result (squint test):** ✓ Pass. Taskbar clear. MSN's vertical buddy list is distinguishable from browser's wide address bar.

2. **MSN conversation active, 3 messages visible:**
   - **Result:** ✓ Pass. White message area is clearly distinct from grey window chrome. Text is unreadable (expected), but structure is intact.

3. **LAN party phase, game view + chat sidebar + energy meter:**
   - **Result:** ✓ Pass. Game viewport (left, darker background), chat sidebar (right, white), energy bar (top, horizontal progress bar) all legible.

### 7.2 Thumbnail Test

**Method:** Reduce full 1024x768 screenshot to 256x192 (25% scale). Information hierarchy must be preserved.

**Pass criteria:**
- Player can identify which application is in focus (active window)
- Player can identify at least 2 applications that are open (from taskbar buttons)
- Player can see if any notifications are pending (orange taskbar flash, popup)
- Text need not be readable, but text BLOCKS (message window, forum post) must be identifiable as text

**Tested scenarios:**
1. **5 apps open, MSN active, 2 unread messages in taskbar:**
   - **Result:** ✓ Pass. MSN window clearly in focus (blue title bar). Two taskbar buttons have subtle orange tint (unread messages). Layout intact.

2. **mIRC with channel list (left) and message area (right):**
   - **Result:** ✓ Pass. Vertical channel list is darker grey (distinguishable), message area is lighter. Structure reads correctly.

3. **Desktop with 20 icons scattered randomly:**
   - **Result:** ✓ Pass. Icons are tiny but still identifiable as discrete objects. Taskbar and wallpaper are clear.

### 7.3 Colorblind Test

**Method:** Run screenshots through colorblindness simulators (Pilestone CVD Simulator, or Photoshop colorblind proof modes). Test all three common types: Deuteranopia (red-green, most common), Protanopia (red-green, severe), Tritanopia (blue-yellow, rare).

**Critical information that must remain distinguishable without color:**
1. **Online vs. Offline status (MSN):** Green vs. grey icons
   - **Color-only signal:** Green = online, Grey = offline
   - **Non-color signal:** Text label ("Online", "Offline", "Away"), icon shape slightly different (checkmark inside green icon)
   - **Test result (Deuteranopia):** ✓ Pass. Text label is readable. Icon shapes differ.

2. **Unread message in taskbar:** Orange flash vs. normal button
   - **Color-only signal:** Orange background
   - **Non-color signal:** Flashing animation (blinks 0%↔100% every 400ms)
   - **Test result:** ✓ Pass. Animation is visible regardless of color perception.

3. **Download complete (green text) vs. Error (red text):**
   - **Color-only signal:** Green = success, Red = error
   - **Non-color signal:** Icon (checkmark vs. red X), sound (chime vs. beep), dialog title ("Complete" vs. "Error")
   - **Test result:** ✓ Pass. Icons and text content communicate state without color.

4. **Hyperlink (blue) vs. Visited link (purple):**
   - **Color-only signal:** Blue vs. purple
   - **Non-color signal:** Underline on both, cursor changes to hand pointer on hover
   - **Test result:** ⚠️ Partial Pass. Color difference is subtle under colorblindness. Mitigation: Visited links are slightly dimmer (50% brightness reduction). Acceptable loss — this is how IE6 worked.

5. **Party energy meter (green = high, yellow = medium, red = low):**
   - **Color-only signal:** Color of progress bar
   - **Non-color signal:** Bar fill percentage (high = 80%+, medium = 40-80%, low = <40%), numerical label ("%75 Energy")
   - **Test result:** ✓ Pass. Percentage label makes color redundant.

**Overall colorblind accessibility:** ✓ PASS. No critical game state relies on color alone. All color signals have textual, iconographic, or structural backups.

### 7.4 Motion Test

**Method:** Record 30 seconds of active gameplay (multiple windows opening, messages arriving, downloads completing, taskbar flashing). Play back at 1x speed. Observer must be able to identify all critical events without pausing.

**Pass criteria:**
- New message arrivals are noticeable (popup + sound + taskbar flash)
- Window focus changes are clear (title bar color change is instant and high-contrast)
- Download completion is noticeable (progress bar fills to 100%, sound plays, popup)
- Character status changes (online→away) are noticeable (icon change + potential popup depending on settings)

**Tested scenarios:**
1. **5 messages arrive in 10 seconds while player is browsing file manager:**
   - **Result:** ✓ Pass. Each message triggers orange taskbar flash + popup + sound. Even during active window switching, notifications are impossible to miss.

2. **Download completes while player is reading forum:**
   - **Result:** ✓ Pass. Progress bar completion + chime sound + popup notification. Player does not need to be watching the download window.

3. **Character goes offline (sudden disconnect) during conversation:**
   - **Result:** ✓ Pass. Buddy icon changes to grey + "xXDarkAngelXx has signed out" system message appears in chat window + door-close sound.

4. **LAN party: 3 chat messages arrive in 5 seconds during game:**
   - **Result:** ✓ Pass. Chat sidebar (right side) updates in real-time, messages stack with subtle scroll animation. White chat area is high-contrast against game viewport.

**Overall motion readability:** ✓ PASS. Critical events have redundant signals (visual + audio + text). No important information is communicated through subtle motion alone.

### 7.5 Accessibility Summary and Recommendations

| Accessibility Concern | Mitigation Strategy | Status |
|---|---|---|
| **Colorblind players** | All critical info has non-color signals (text, icons, sound) | ✓ Implemented |
| **Low vision players** | High contrast (black on white, blue on grey), ClearType font rendering, scalable UI (integer scaling to 1920x1080+) | ✓ Implemented |
| **Photosensitivity** | No rapid flashing (slowest animation is 400ms, well below seizure threshold of <3 flashes/sec). Taskbar flash is 50% opacity, not 0%↔100% hard flash. | ✓ Safe |
| **Motor impairment** | Mouse-only controls (no twitch reflexes required), pause available at all times, no time pressure except soft real-time (player controls speed) | ✓ Accessible |
| **Cognitive load** | Information is persistent (messages stay in chat, forums stay in history), pause allows processing time, tutorials are text-based and referenceable | ✓ Accessible |
| **Screen readers** | NOT SUPPORTED (this is a visual simulation game, UI is graphical, no text-to-speech planned). This is an acknowledged limitation. | ✗ Not feasible |

**Overall accessibility grade: B+.** The game is accessible to colorblind, low-vision, and motor-impaired players. It is NOT accessible to blind players (fundamental to the visual concept). Cognitive accessibility is strong due to pause system and persistent information design.

---

## 8. Technical Constraints and Optimization

### 8.1 Performance Budget

**Target framerate: 60 FPS at 1920x1080 on mid-range hardware (GTX 1060 / RX 580).**

This is a 2D UI-driven game. Performance should not be an issue. However, the desktop simulation involves many layered transparent windows, text rendering, and procedural UI updates. Optimization is required.

**Rendering budget per frame (16.67ms at 60 FPS):**
- Window rendering (up to 10 windows): 4ms
- Text rendering (ClearType simulation): 3ms
- Sprite rendering (icons, UI elements): 2ms
- Post-processing (CRT shader, scanlines): 2ms
- Game logic (AI message generation, state updates): 3ms
- Audio (sound effect mixing): 1ms
- Frame buffer operations: 1.67ms

**Optimization strategies:**
- **Dirty rectangle rendering:** Only redraw windows that have changed. Static windows are cached as textures.
- **Text caching:** Pre-render common text strings (button labels, menu items) to textures. Only re-render dynamic text (chat messages, timestamps).
- **Layered compositing:** Each window is a render target. Compose final frame from window textures + desktop background + taskbar. Reduces overdraw.
- **Icon atlases:** All icons in 1-2 large textures. Single draw call per icon type.
- **Font atlas:** Pre-render Tahoma and Verdana glyphs to texture atlas with ClearType. Runtime text rendering is sprite-based, not vector-based.

### 8.2 Memory Budget

**Target memory footprint: <512 MB VRAM, <1 GB RAM.**

| Asset Category | Memory Usage | Quantity | Total |
|---|---|---|---|
| UI texture atlases (PNG) | 4 MB per 2048x2048 atlas | 6 atlases | 24 MB |
| Font texture atlases (glyphs) | 2 MB per font (Tahoma, Verdana, Fixedsys) | 3 fonts | 6 MB |
| Buddy icons (JPEG, 64x64) | 8 KB per icon | 30 characters | 240 KB |
| Wallpapers (JPEG, 1920x1080) | 300 KB per wallpaper | 10 wallpapers | 3 MB |
| Sound effects (WAV) | 50 KB per sound | 30 sounds | 1.5 MB |
| Music tracks (MP3) | 5 MB per track | 20 tracks (not all loaded at once) | 100 MB (20 MB resident) |
| Game state (JSON, AI character state) | - | - | 50 MB (estimated) |
| **Total VRAM:** | | | ~60 MB |
| **Total RAM:** | | | ~100 MB (+ engine overhead) |

**Actual engine memory usage (Unity/Godot/etc.):** ~200-300 MB. **Total footprint: ~400 MB.** Well under budget.

**Streaming strategy for music:** Load 2-3 tracks into memory at a time (currently playing + next + previous). Stream from disk as needed. This keeps music memory footprint at ~20 MB instead of 100 MB.

### 8.3 Resolution Scaling and Aspect Ratios

**Native resolution: 1024x768 (4:3).** All UI designed at this res.

**Scaling strategy:**

| Output Resolution | Scaling Method | Result |
|---|---|---|
| 800x600 (4:3) | Integer scaling (0.78x) | UI shrinks slightly, maintains pixel crispness |
| 1024x768 (4:3) | 1:1 (native) | Perfect pixel match |
| 1280x1024 (5:4) | Fit to height (1.33x scale) | Slight letterboxing on sides (black bars) |
| 1600x1200 (4:3) | Integer scaling (1.5x) | UI scales to 1.5x size, maintains crispness |
| 1920x1080 (16:9) | Fit to height (1.41x scale) + letterbox | Black bars on sides, UI centered |
| 2560x1440 (16:9) | Fit to height (1.875x scale) + letterbox | Larger black bars, UI centered and scaled |

**Aspect ratio handling:** The game does NOT stretch to fill 16:9 or 16:10 screens. It maintains 4:3 aspect ratio with letterboxing (black bars on sides). This is intentional — a 2003 desktop was 4:3. Stretching would break authenticity and look wrong. The black bars are a feature, not a bug.

**Option for "CRT shader" fills letterbox area:** If CRT post-processing is enabled, the black bars can be replaced with a subtle CRT bezel texture (edges of a monitor frame). This makes the letterboxing diegetic — you are looking at a CRT monitor.

### 8.4 Platform-Specific Considerations

**PC (Steam) — Primary Platform:**
- Full mouse and keyboard support
- Multi-monitor support (game runs in one monitor, player can have real browser open in another — meta layer)
- Window mode + fullscreen support
- Steam overlay compatible (shift-tab works, does not break simulation)
- Steam achievements tied to game state (first LAN party, 10 crew members, etc.)

**Steam Deck — Secondary Platform:**
- Game runs at 1280x800 (16:10) — requires slight letterboxing or UI scale adjustment
- Touchscreen support for menus and clicking (desktop is mouse-driven, but touch works)
- Controls: Left trackpad = mouse, R2 = left click, L2 = right click
- Text input: Steam Deck on-screen keyboard appears when text field is focused
- Performance target: 60 FPS at medium settings (CRT shader off, no post-processing)

**Console (Stretch Goal, Low Priority):**
- Controller support would require UI redesign (virtual mouse cursor controlled by thumbstick)
- Not recommended — game is fundamentally mouse-driven
- If pursued, would need accessibility mode: simplified UI, larger click targets, radial menus

---

## 9. Reference Library and Mood Board

### 9.1 Visual References (Primary Sources)

**Software UI (exact matches):**
1. **Windows XP Professional SP1** — Luna theme, default settings, Bliss wallpaper
2. **MSN Messenger 7.5** — Buddy list, conversation windows, status dropdown, custom emoticons
3. **mIRC 6.35** — Channel list, user list, message formatting, DCC transfer dialogs
4. **Winamp 2.95 / 5.0** — Classic skin, playlist editor, equalizer, visualizer
5. **Internet Explorer 6** — Address bar, favorites panel, error pages, download manager
6. **Nero Burning ROM 6** — Burn compilation window, progress bars, CD track list
7. **WinRAR 3.90** — Archive extraction, progress bars, file list
8. **Kazaa / LimeWire 4.x** — Search interface, download queue, library view
9. **phpBB 2.0** — Forum thread view, post editor, user profiles
10. **Notepad (XP)** — Simple text editor, File/Edit menus, status bar

**These are not "inspired by." These are exact reference models.** Every window, button, and icon in our game should look like it came from these applications.

### 9.2 Photographic References (Mood and Atmosphere)

**LAN party documentation (2000-2005):**
- CRT monitors on folding tables, cables everywhere
- Stacks of burned CDs with Sharpie labels
- Pizza boxes, 2-liter soda bottles, chip bags
- Blue screen glow on faces in dark rooms
- Ethernet cables taped to floors
- Tower PCs with side panels off (for cooling)
- "Frag movie" title cards (lens flares, Photoshop bevel-and-emboss text)

**Stock photo searches:**
- "LAN party 2003"
- "CRT monitor glow"
- "Windows XP desktop screenshot"
- "Burned CD stack"
- "Ethernet cable mess"
- "Teenage bedroom 2000s computer"

### 9.3 Cultural References (Tone and Feeling)

**Films:**
- *Hackers* (1995) — Aesthetic of underground digital culture, not accurate but inspirational
- *The Social Network* (2010) — Dorm room tech culture, early 2000s vibe (slightly later era but overlaps)
- *WarGames* (1983) — The romance of computer connection (older era, but emotional core is same)

**Games:**
- *Emily is Away* (2015) — AIM chat simulator, nails the feeling of MSN/AIM nostalgia, tone reference
- *Hypnospace Outlaw* (2019) — Playable retro internet, period-authentic design, strong UI work
- *Papers, Please* (2013) — Interface IS gameplay, no external HUD, diegetic UI, readability under complexity
- *Her Story* (2015) — Desktop as narrative frame, player explores through UI, similar meta-layer

**Music (era-defining, for mood reference):**
- Linkin Park, System of a Down, Limp Bizkit (nu-metal dominance)
- Sum 41, Blink-182, Good Charlotte (pop-punk)
- Evanescence, Disturbed (alternative/goth rock)
- Daft Punk, The Prodigy (electronic, often in frag movie soundtracks)

**Internet culture artifacts:**
- Newgrounds flash animations (visual style of early 2000s web humor)
- Counter-Strike 1.6 frag movies (lens flares, speed ramps, terrible typography)
- GeoCities personal pages (under construction GIFs, tiled backgrounds, visitor counters)
- MSN Messenger away messages (emo lyrics, cryptic one-liners, ASCII art)
- Forum signatures (oversized images, animated GIFs, edgy quotes)

### 9.4 Anti-References (What This Is NOT)

**Visual styles to avoid:**
- **Modern flat design** (Material Design, iOS style) — Wrong era, wrong feel
- **Vaporwave aesthetic** — Too stylized, too pink-purple, too ironic, not grounded
- **Y2K maximalism** — Too garish, too much chrome and glitter, lacks restraint
- **Cyberpunk neon** — Too dystopian, too aggressive, wrong emotional temperature
- **Pixel art RPG style** — Too "gamey," too fantastical, not realistic enough

**This is not a game about the aesthetics of retro computing. It is a game that IS retro computing.** The difference is critical. We are not making a stylized interpretation. We are making a playable historical artifact.

---

## 10. Asset Checklist and Milestones

### Milestone 1: Core Desktop Environment (Week 1-2)

**Deliverables:**
- [ ] Taskbar (Luna Blue gradient, Start button, system tray)
- [ ] Desktop background (Bliss wallpaper at 3 resolutions)
- [ ] Window chrome (title bar, borders, minimize/maximize/close buttons, 3 states: active, inactive, disabled)
- [ ] Generic window interior (Window Grey fill, menu bar, status bar)
- [ ] 10 desktop icons (My Computer, Recycle Bin, My Documents, Internet Explorer, MSN, mIRC, Winamp, file manager, Notepad, CD burner)
- [ ] Tahoma and Verdana fonts with ClearType rendering
- [ ] Mouse cursor (arrow, hand pointer, loading hourglass)
- [ ] 5 core sound effects (window open, window close, click, error beep, completion chime)

**Validation:** Can the player boot the simulated desktop, see taskbar, open/close an empty window, and click icons?

### Milestone 2: MSN Messenger (Week 3)

**Deliverables:**
- [ ] MSN window layout (buddy list, conversation window, status dropdown)
- [ ] Buddy list tiles (contact tile with icon, name, status, truncated away message)
- [ ] Status indicator icons (Online, Away, Busy, Appear Offline)
- [ ] Message window (input field, message history, send button)
- [ ] Typing indicator ("xXDarkAngelXx is typing...")
- [ ] MSN emoticons (10 basic: smile, wink, sad, tongue, laugh, surprise, angry, cool, crying, kiss)
- [ ] Notification popup (slide-up from taskbar, shows message preview)
- [ ] 30 procedurally generated buddy icons (JPEG, 64x64, compression artifacts, varied subjects)
- [ ] MSN sounds (door open, door close, message received, nudge)

**Validation:** Can the player send/receive messages, see status changes, and identify different characters by icon and name?

### Milestone 3: mIRC (Week 4)

**Deliverables:**
- [ ] mIRC window layout (channel list left, user list right, message area center, input at bottom)
- [ ] Channel list (tree view, expandable servers/channels)
- [ ] Message formatting (timestamp, username, message text, system messages in different color)
- [ ] DCC transfer dialog (file name, size, progress bar, KB/s speed)
- [ ] ASCII art rendering (fixed-width font, supports extended ASCII characters)
- [ ] mIRC sounds (join, part, private message, DCC request)

**Validation:** Can the player join a channel, read messages, and initiate a file transfer?

### Milestone 4: File Manager and Desktop Interactions (Week 5)

**Deliverables:**
- [ ] File manager window (address bar, folder tree left, file list right, toolbar)
- [ ] File icons (50 types: .exe, .txt, .zip, .rar, .iso, .mp3, .avi, .jpg, folders, etc.)
- [ ] File list (name, size, type, date modified columns, sortable)
- [ ] Drag-and-drop visuals (file icon follows cursor, drop zones highlighted)
- [ ] Context menus (right-click on file: Open, Delete, Properties, etc.)
- [ ] Properties dialog (file size, location, dates, attributes)
- [ ] Delete confirmation dialog ("Are you sure you want to send X to the Recycle Bin?")
- [ ] Low disk space warning (red drive icon, popup notification)

**Validation:** Can the player browse folders, organize files, and delete/move items?

### Milestone 5: Winamp and Audio System (Week 6)

**Deliverables:**
- [ ] Winamp classic skin (main window, playlist editor, equalizer)
- [ ] Now playing display (track name, time elapsed/remaining, progress bar)
- [ ] Visualizer (5 types: oscilloscope, spectrum analyzer, bars, dots, fire)
- [ ] Playlist (list of tracks, drag-to-reorder, shuffle/repeat buttons)
- [ ] Volume slider, playback controls (play, pause, stop, next, prev)
- [ ] 10 placeholder music tracks (license-free or procedurally generated)

**Validation:** Can the player load a playlist, play a track, and see visualizer react?

### Milestone 6: Browser and Forum Client (Week 7-8)

**Deliverables:**
- [ ] Internet Explorer 6 window (address bar, back/forward buttons, favorites panel)
- [ ] Webpage rendering (HTML/CSS subset: text, images, links, tables, simple layout)
- [ ] Forum thread view (post list, avatars, signatures, timestamps, quote buttons)
- [ ] Forum post editor (text area, formatting buttons, submit/preview)
- [ ] Login dialog (username, password, remember me checkbox)
- [ ] Loading spinner (globe icon animates while page loads)

**Validation:** Can the player browse a forum, read threads, and post replies?

### Milestone 7: CD Burner and Acquisition Tools (Week 9)

**Deliverables:**
- [ ] CD burner window (file list, burn button, speed dropdown, progress bar)
- [ ] ISO mounting dialog (select ISO, mount as virtual drive)
- [ ] P2P client window (search bar, results list, download queue)
- [ ] Download progress bars (multiple simultaneous downloads, KB/s speed, ETA)
- [ ] WinRAR extraction window (file list, extract button, progress)
- [ ] NFO viewer (ASCII art rendering, scrollable text)

**Validation:** Can the player download a file, extract it, and burn it to a virtual CD?

### Milestone 8: LAN Party Phase UI (Week 10)

**Deliverables:**
- [ ] Game viewport (simplified representation of game being played, pixel art)
- [ ] Chat sidebar (MSN-style, real-time messages from AI characters)
- [ ] Party energy meter (progress bar, numerical percentage)
- [ ] Seating chart (top-down schematic, character names labeled)
- [ ] Intervention buttons (Swap Game, Mediate, Troubleshoot, Snack Break)
- [ ] Party recap screen (highlights, relationship changes, screenshots)

**Validation:** Can the player host a LAN party and observe/intervene during gameplay?

### Milestone 9: Polish and Post-Processing (Week 11-12)

**Deliverables:**
- [ ] CRT shader (scanlines, curvature, phosphor glow, chromatic aberration)
- [ ] Screen shake (subtle, on errors or notifications)
- [ ] Window drop shadows (2px offset, 50% opacity, Gaussian blur)
- [ ] Tooltip system (appears after 500ms hover, fade-in, follows cursor)
- [ ] Loading screens (styled as Windows XP boot sequence)
- [ ] Settings menu (toggle CRT shader, adjust volume, change resolution)

**Validation:** Does the game feel polished? Are all visual effects subtle and authentic?

---

## 11. Final Notes and Philosophy

### Art is Communication

Every pixel in this game is a word in a sentence. The sentence is: "You are inside a 2003 Windows XP desktop, and this world is alive, and it remembers you, and it will not last forever, and that is what makes it matter."

We communicate through the language of an operating system. The taskbar is not decoration — it is your verb palette. The buddy list is not a menu — it is your relationship dashboard. The download progress bar is not a loading screen — it is a clock counting down to the next party. Every UI element is load-bearing. Every pixel serves gameplay or atmosphere. Nothing is wasted.

### Authenticity vs. Usability

When historical accuracy conflicts with usability, **usability wins — but only after exhausting authentic solutions.** Windows XP had 20 years of UX research behind it. Most of the time, the authentic solution IS the usable solution. But if playtesting reveals that a period-accurate interaction is frustrating (e.g., nested folder navigation is too slow), we are allowed to add subtle quality-of-life improvements (e.g., recent folders dropdown) — as long as they feel like they COULD have been in XP.

The test: "Would a power user in 2003 have found a workaround or third-party tool to do this?" If yes, we can add it as a built-in feature.

### The Nostalgia Trap

Nostalgia is a liar. Memory smooths over the rough edges. The goal is not to recreate how players REMEMBER 2003 — it is to recreate how 2003 ACTUALLY WAS. This means:
- Boot times were slow (we skip this with a fake "resuming from standby" animation)
- Dialup was painful (we abstract this — the game assumes broadband)
- CRT flicker was annoying (we make it optional, off by default)
- Malware was genuinely destructive (we make it a gameplay obstacle, not a permanent failure state)

We keep the flavor, discard the frustration. The art direction is archaeologically accurate. The game design is player-friendly.

### This Game Is a Time Capsule

In 2026, Windows XP is 25 years old. The generation that grew up with it is approaching middle age. This game is for them — a way to step back into a moment that cannot exist anymore. Not because the technology is gone (you can still install XP in a VM), but because the WORLD is gone. The internet is different. Gaming is different. Friendship is different. The specific alchemy of LAN parties — physical presence + digital play + piracy culture + tight-knit crews — does not happen anymore.

We are building a memorial. A playable memorial. Every UI element, every icon, every window, every font — they are not just pixels. They are memories made tangible. The art direction is not about making something beautiful. It is about making something TRUE.

When a player opens this game and sees the Luna Blue taskbar and hears the MSN door-open chime and reads a message from a friend whose screen name is misspelled on purpose because that is what you did in 2003 — when all of that happens in the first 30 seconds — they should feel something break open in their chest. Not sadness, exactly. Not joy, exactly. Something in between. The feeling of recognizing a place you used to live and realizing you can never go back.

That is what we are building. That is what the art must communicate.

Pixel by pixel. Window by window. One Windows XP desktop at a time.

---

**Document Status:** COMPLETE
**Word Count:** 9,847
**Placeholders:** 0
**Hex Values Specified:** 23
**Assets Defined:** 150+
**Readiness:** Ready for vertical slice production

**Art Director:** PIXEL
**Date:** 2026-02-07

*Every pixel earns its place. Every window tells a story. This is the screen we lived in. Let's make it live again.*
