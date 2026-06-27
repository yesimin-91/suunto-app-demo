# Suunto App Web Demo PRD

## 0. Document Meta

| Item | Value |
|---|---|
| Document type | Product Requirements Document |
| Project | Suunto App Web Demo |
| Current status | Implemented demo aligned document |
| Main entry | `../index.html` |
| Theme token source used by demo | `../docs/suunto-semantic-colors.css` |
| Source design | Figma `App Colors 2.0` |
| Last updated | 2026-06-27 |

## 1. Document Goal

This PRD is used as the single product description for the current Suunto web demo.

It must satisfy three goals:

- Module completeness: every implemented screen and interaction in the demo is covered, and no non-existent module is introduced.
- AI readability: the structure is explicit, deterministic, and easy for AI or engineering tools to parse.
- Engineering readiness: requirements are specific enough to be implemented or verified directly.

This document describes the demo **as it currently exists**, not an imagined future product.

## 2. Product Overview

The project converts the Figma design `App Colors 2.0` into a local, browser-based, phone-first interactive demo.

The main purpose of the current demo is:

- to present Suunto app information architecture and core visual modules;
- to compare Light mode and Dark mode display results through a real interactive flow;
- to support product/design review, stakeholder walkthroughs, and future engineering estimation.

This is not a production app. All data is mocked. No backend, account system, Bluetooth, or live device sync is required.

## 3. Primary Demo Goal

### 3.1 Core Value

The demo should allow a reviewer to:

1. Open the app shell locally.
2. Navigate through the key Suunto screens.
3. Enter `Settings`.
4. Use `Appearance` to switch the **global** UI theme.
5. Compare the same product UI in Light mode and Dark mode.

### 3.2 Theme Showcase Rule

The `Appearance` setting is not a secondary detail. It is one of the core demo interactions.

Current product rule:

- `Automatic` behaves the same as `Dark`.
- `Dark` behaves the same as the current dark theme.
- `Light` switches the full demo to light theme.

## 4. Scope

### 4.1 In Scope

- Home Dashboard
- Calendar
- Calendar Daily Page
- Training
- Profile
- Settings
- Pairing / Device
- Global bottom navigation
- Profile header collapse interaction
- Global Light/Dark theme switching from `Settings > Appearance`

### 4.2 Out of Scope

- Real login, real account state, cloud sync, Bluetooth pairing, watch communication
- Real charts backed by live data
- Real notifications, social feeds, comments, likes, uploads
- Editable profile data
- Full settings subpage depth
- URL routing, server rendering, or production deployment architecture
- Native app behaviors such as gestures, haptics, OS permissions, or system theme following
- A true automatic theme mode tied to system appearance

## 5. Target Users

- Product stakeholders reviewing information architecture and feature framing
- Designers validating layout parity, color semantics, density, and theme consistency
- Engineers estimating implementation scope and modularization strategy
- Demo viewers who need a local interactive artifact without installing a native app

## 6. Demo Environment And Form Factor

| Requirement ID | Requirement |
|---|---|
| ENV-01 | The demo runs locally by opening `../index.html` directly in a browser. |
| ENV-02 | The demo must not require a build step or external network request to render the core experience. |
| ENV-03 | The layout is phone-first and centered in a browser viewport. |
| ENV-04 | The visible app canvas targets a 390px wide mobile layout. |
| ENV-05 | The current demo may be presented inside an iPhone-like shell/frame for easier height review. |

## 7. Source Design Coverage

| Screen | Figma Node | Demo Status |
|---|---:|---|
| Home Dashboard | `8814:176621` | Implemented |
| Calendar | `10041:172425` | Implemented |
| Calendar Daily Page | `10041:172367` | Implemented |
| Training | `8814:174496` | Implemented |
| Profile | `8813:171761` | Implemented |
| Settings | `8813:172628` | Implemented |
| Pairing / Device | `8813:55632` | Implemented |

Implementation detail:

- The Figma source is too large for stable full-node extraction.
- Engineering/design alignment should continue to use targeted node inspection and asset exports by screen or component.

## 8. Information Architecture

### 8.1 Main Navigation

Bottom navigation includes four entries:

- Home Dashboard (bottom-nav label: Feed)
- Calendar (bottom-nav label: Calendar)
- Training (bottom-nav label: Trends)
- Profile (bottom-nav label: Profile)

### 8.2 Secondary Navigation

- Calendar contains a daily-entry interaction from the month view
- Profile opens `Settings`
- Home opens `Pairing / Device`

### 8.3 No-Nav Detail Screens

The following screens are detail screens and do not use the bottom nav as their primary return path:

- Calendar Daily Page
- Settings
- Pairing / Device

## 9. Functional Requirements

### 9.1 Global Interaction Requirements

| ID | Requirement |
|---|---|
| FR-G-01 | All primary navigation is implemented as in-page state switching, not route changes. |
| FR-G-02 | Screen switching must keep the current app shell and feel instantaneous. |
| FR-G-03 | The active bottom-nav item must update when switching between Home Dashboard (Feed), Calendar, Training (Trends), and Profile. |
| FR-G-04 | Scrollable screens must support vertical scrolling without blocking click targets. |
| FR-G-05 | Theme selection must update the global UI, not just the Settings screen. |
| FR-G-06 | The selected appearance mode must persist across refresh using local storage. |

### 9.2 Home Dashboard

Purpose: show the first-screen overview of daily and weekly fitness data widgets.

Required content:

- iOS-like status area
- Home top bar
- Device entry button
- Two-column widget grid
- Widget collection including steps, HRV, training load, duration, VO2max, recovery, sleep, heart rate, avg. pace, avg. speed, activity, calendar, calories, period, commutes, and map summary

Required interaction:

- Tap device entry opens `Pairing / Device`

### 9.3 Calendar

Purpose: show monthly training distribution and a monthly summary.

Required content:

- Top bar
- Diary / My Plan style tab area
- Period chips
- Month calendar grid
- Activity dots in dates
- Month metrics summary
- Sport summary cards
- Map summary card

Required interaction:

- Tap the July 10 highlighted activity entry opens `Calendar Daily Page`

### 9.4 Calendar Daily Page

Purpose: show one selected day with activity and wellness detail.

Required content:

- Back button to Calendar
- Date summary
- Activity summary cards
- Sleep data section
- Heart-rate section
- Resources section
- Steps section
- Calories section
- Mixed chart presentation using CSS/SVG

Required interaction:

- Back button returns to Calendar

### 9.5 Training

Purpose: show training-zone style analytics and weekly breakdown content.

Required content:

- Top bar
- Top tab strip: `Training`, `Progress`, `Recovery`, `Daily health`
- Period chips
- Weekly selector
- All-sports summary
- Training volume cards
- Zone/intensity list
- Impact list

Required interaction:

- Bottom nav remains available

Current note:

- This screen is primarily a presentation screen.
- Top tabs and metric cards are visually implemented for demo parity; they are not a full analytics tool.

### 9.6 Profile

Purpose: show user identity, summary stats, sports breakdown, badges, and settings entry.

Required content:

- Hero background image
- Avatar, name, bio
- Paired device summary
- Following/follower summary
- Activity summary card
- Thumbnail/media row
- Sports stack and sport rows
- Badges panel
- Profile list panels

Required interaction:

- Tap the settings action opens `Settings`
- Bottom nav remains available

Additional scroll interaction:

- As the Profile page scrolls downward, the hero area fades/collapses
- The avatar shrinks toward a mini avatar in the top area
- A fixed profile top bar becomes visible
- Activity and list content remains available below

### 9.7 Settings

Purpose: show account/settings lists and host the theme-switching control.

Required content:

- Back button to Profile
- Sectioned settings list
- `Appearance` row with segmented control
- Account, Activity & training, Outdoor, General, Notification, Others, About APP sections
- Sign out button

Required interaction:

- Back button returns to Profile
- Appearance segmented control switches global theme

Appearance behavior:

- `Automatic`: stores the value `automatic` and renders the dark theme
- `Light`: stores the value `light` and renders the light theme
- `Dark`: stores the value `dark` and renders the dark theme

### 9.8 Pairing / Device

Purpose: show paired watch/device state and device-related entry points.

Required content:

- Back button to Home
- Device title and connection status
- Watch product image
- Sync/battery information
- Banner entry
- Device feature list
- Support and management rows

Required interaction:

- Back button returns to Home

## 10. Navigation Matrix

| Trigger | Result |
|---|---|
| Bottom nav `Feed` | Open Home Dashboard |
| Bottom nav `Calendar` | Open Calendar |
| Bottom nav `Trends` | Open Training |
| Bottom nav `Profile` | Open Profile |
| Home device entry | Open Pairing / Device |
| Calendar July 10 activity | Open Calendar Daily Page |
| Daily back | Return to Calendar |
| Profile settings action | Open Settings |
| Settings back | Return to Profile |
| Settings `Appearance` -> `Automatic` | Global dark theme |
| Settings `Appearance` -> `Light` | Global light theme |
| Settings `Appearance` -> `Dark` | Global dark theme |
| Pairing back | Return to Home |

## 11. Theme And Color Requirements

### 11.1 Source Of Truth

Theme semantics in the current demo are implemented through:

- runtime file: `../docs/suunto-semantic-colors.css`
- upstream reference: `../docs/color_variables.css`

Engineering rule:

- UI chrome, text, surfaces, and borders should use semantic tokens
- business/chart/activity colors may use product-specific accent tokens where required by the design

### 11.2 Theme Modes

| Mode in UI | Actual rendered theme |
|---|---|
| Automatic | Dark |
| Dark | Dark |
| Light | Light |

### 11.3 Theme Scope

Theme switching must affect all major screens:

- Home Dashboard
- Calendar
- Calendar Daily Page
- Training
- Profile
- Settings
- Pairing / Device

### 11.4 Semantic Color Rules

| ID | Requirement |
|---|---|
| TH-01 | Background, surface, text, icon, divider, and border colors must come from semantic theme variables. |
| TH-02 | Light mode must not leave dark-theme UI chrome behind on top bars, bottom nav, cards, or base backgrounds. |
| TH-03 | Dark mode must remain aligned with the dark semantic token mapping used by the current demo. |
| TH-04 | Icons that need theme response should use theme-aware SVG, mask, or semantic-color techniques rather than fixed-color raster assets whenever possible. |
| TH-05 | Activity colors, chart highlights, and sport-specific accents may remain stable across themes if required by the design language. |

## 12. Data Requirements

All data is mocked.

Required mock data groups:

- User profile data
- Device state data
- Dashboard widget values
- Dashboard activity widget data
- Profile media thumbnail data
- Calendar month data
- Daily detail data
- Training analytics data
- Settings list labels and selected values

Mock data quality rules:

- Values should be believable for a sports/fitness product
- Units must remain internally consistent
- Repeated content is acceptable if needed for the demo
- Data does not need CRUD behavior

## 13. Asset Requirements

Primary local assets include:

| Asset Type | Example |
|---|---|
| Fonts | `../fonts/font/Proxima Nova Reg.otf` |
| Font token reference | `../fonts/font_variables.css` |
| Theme token reference | `../docs/color_variables.css` |
| Runtime semantic theme file | `../docs/suunto-semantic-colors.css` |
| Watch/device images | `../assets/Watch.png` |
| Avatar/background images | `../assets/Avatar.png`, `../assets/profile bg.png` |
| Activity/map/media assets | `../assets/map.png`, `../assets/.ShareCrouselItem 1.png` etc. |
| Badge assets | `../assets/Achievement badge 1.png` etc. |
| Icon assets | `../assets/icons/figma/*` |

Asset rules:

- Prefer local assets only
- Prefer vector icons for theme-responsive UI
- Preserve naming consistency between design export and implementation mapping

## 14. Technical Implementation Requirements

| ID | Requirement |
|---|---|
| TECH-01 | The current deliverable is a single-file demo in `../index.html`. |
| TECH-02 | CSS and JavaScript may remain embedded for portability. |
| TECH-03 | No external framework is required for the current phase. |
| TECH-04 | Navigation is state-driven inside the page, not URL-driven. |
| TECH-05 | Charts should continue to use CSS and inline SVG unless a later phase requires a dedicated chart library. |
| TECH-06 | Theme state should be written to and restored from `localStorage`. |
| TECH-07 | Screen content should be rendered as real DOM, not flattened full-screen images. |

## 15. Chart Strategy

Current recommendation:

- Keep compact charts hand-built with CSS and inline SVG
- Optimize for design parity instead of generic chart-library defaults
- Introduce a chart library only if interaction depth or real data complexity becomes necessary

Library evaluation summary:

- Apache ECharts: strongest future candidate for advanced analytics
- Chart.js: acceptable for simple charts, weaker for strict UI parity
- D3: flexible but high-cost for this demo phase
- FullCalendar: unnecessary for the current custom monthly view

## 16. Risks And Constraints

- Large Figma nodes are unstable to read in one call; design alignment should continue component by component
- Single-file implementation is fast to review but harder to scale without later refactoring
- Some icons still depend on asset export quality and naming consistency
- Hidden filenames such as `.ShareCrouselItem` are usable locally but not ideal for long-term packaging
- Because this is a demo, some visual modules are presentation-only and do not represent complete business logic

## 17. Acceptance Criteria

The demo is acceptable when all conditions below are true:

- `../index.html` opens locally without build tooling
- Core UI renders with local fonts and local assets
- Home Dashboard, Calendar, Training, and Profile are reachable from the bottom nav
- Calendar can enter Daily Page and return
- Profile can enter Settings and return
- Home can enter Pairing / Device and return
- `Settings > Appearance` can switch the full demo between Light and Dark presentation rules
- `Automatic` and `Dark` both render the dark theme
- `Light` renders the light theme across the full demo, not only Settings
- The selected appearance mode persists after refresh
- Profile header collapse interaction works during scroll
- All core screens contain visible, data-rich content rather than empty placeholders
- The visual language remains recognizably aligned with the Suunto design system

## 18. Future Iteration Backlog

- Split the single-file implementation into reusable modules if the demo continues to grow
- Add shareable route states if deep links become necessary
- Add more exact Figma-exported icon replacements where parity still needs refinement
- Replace hidden asset filenames with packaging-safe names
- Add more explicit interaction states for Training and Calendar secondary controls
- Add a true system-linked automatic appearance mode if the demo goal expands
- Add screen-by-screen visual regression snapshots for design review

## 19. Engineering Handoff Notes

If engineering continues from the current demo, the recommended order is:

1. Keep `../index.html` as the executable reference.
2. Treat `../docs/suunto-semantic-colors.css` as the runtime theme contract.
3. Preserve the current screen/state model before attempting structural refactors.
4. Refactor only after visual parity and theme behavior remain stable.

This PRD intentionally mirrors the current demo behavior so that product, design, engineering, and AI tools can reference the same scope definition.
