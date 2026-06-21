# Suunto App Web Demo PRD

## 1. Background

This project converts the Figma design `App Colors 2.0` into a browser-based mobile web demo. The demo is intended for product/design review, interaction walkthroughs, and future implementation discussion. It is not a production app and does not require real backend data in the current phase.

The current implementation is a standalone HTML demo at `../index.html`. It uses local Proxima Nova fonts, local exported image assets, Suunto dark-mode color tokens, and simulated sports/activity data.

## 2. Goals

- Recreate the key Suunto App mobile screens from the Figma design in a browser.
- Keep the experience phone-first, using a 390px mobile canvas centered in the browser.
- Support the primary navigation flow across Home, Calendar, Training, Profile, Settings, and Pairing.
- Use real DOM text, cards, tabs, lists, charts, and controls instead of full-screen screenshots.
- Use simulated data where live Suunto account/device/activity data is unavailable.
- Keep the first version portable and offline-friendly with no external runtime dependencies.

## 3. Non-Goals

- No real login, cloud sync, device Bluetooth pairing, or account integration.
- No backend API, persistence, or user-generated data upload.
- No production-grade charting engine in the first version.
- No complete implementation of every secondary settings/device subpage.
- No light-mode or multilingual version unless requested in a later phase.

## 4. Target Users

- Product stakeholders reviewing the Suunto App information architecture.
- Designers validating layout, density, visual hierarchy, and dark-mode styling.
- Engineers estimating future implementation complexity.
- Demo viewers who need to click through the main app areas without installing a native app.

## 5. Source Design Scope

The source Figma node is `demo`, node ID `8813:52961`. The broad node is too large for stable full `get_design_context` extraction, so implementation should continue to use targeted child nodes and screenshots.

| Product Screen | Figma Node | Current Demo Coverage |
|---|---:|---|
| Home Dashboard | `8814:176621` | Implemented as Home Dashboard tab |
| Home Activities | `8869:168416` | Implemented as Home Activities tab |
| Calendar | `10041:172425` | Implemented as Calendar bottom-nav screen |
| Calendar Daily Page | `10041:172367` | Implemented as Daily detail screen |
| Training | `8814:174496` | Implemented as Training bottom-nav screen |
| Profile | `8813:171761` | Implemented as Profile bottom-nav screen |
| Settings | `8813:172628` | Implemented as Settings detail screen |
| Pairing / Device | `8813:55632` | Implemented as Pairing detail screen |

## 6. Product Structure

### 6.1 Home Dashboard

Purpose: Show the user's daily and weekly data overview.

Required content:

- Status bar and Home top bar.
- Device entry control in the top-left.
- Dashboard / Activities top tab switcher.
- Two-column widget grid.
- Widgets for steps, HRV, training load, duration, VO2max, recovery, sleep, heart rate, pace, speed, weekly activity, calendar date, calories, and map summary.

Primary interaction:

- Tap device entry to open Pairing / Device screen.
- Tap Activities tab to switch to Home Activities.

### 6.2 Home Activities

Purpose: Show a feed of recent sports activities.

Required content:

- Activity filter chips: All, Me, Flowing.
- Route activity cards with map image, route overlay, sport type, duration, distance, ascent, and social action indicators.
- Share photo carousel using local exported photo assets.

Primary interaction:

- Tap Dashboard tab to return to Dashboard.
- Bottom navigation remains available.

### 6.3 Calendar

Purpose: Show monthly activity distribution and monthly summary.

Required content:

- Calendar top bar.
- Diary / My Plan tabs.
- Time-range chips: Week, Month, Year, 30 days.
- July month grid with activity intensity dots.
- Monthly totals: duration, distance, ascent, calories.
- Sport summary cards for running, cycling, walking, and weight training.
- Map summary panel.

Primary interaction:

- Tap July 10 activity dot to open Calendar Daily Page.

### 6.4 Calendar Daily Page

Purpose: Show detailed daily activity and wellness data for a selected date.

Required content:

- Back navigation to Calendar.
- Daily summary metrics.
- Activity summary cards.
- Sleep chart.
- Heart rate chart.
- Resources chart.
- Steps chart.
- Calories chart.

Primary interaction:

- Tap back to return to Calendar.

### 6.5 Training

Purpose: Show training-zone analytics and weekly performance breakdown.

Required content:

- Training Zone top bar.
- Training / Progress / Recovery / Daily health tabs.
- Time range chips.
- Weekly period selector.
- All sports summary.
- Training volume stacked bar chart.
- Intensity zones list.
- Impact list with progress bars.

Primary interaction:

- Bottom navigation to other main areas.

### 6.6 Profile

Purpose: Show user identity, activity history, achievements, and account entry points.

Required content:

- Profile background image.
- Avatar, name, profile summary, paired devices, following/follower counts.
- Activities summary card.
- Recent activity thumbnails.
- Sports distribution rows.
- Badges.
- Personal records and leaderboard entries.
- Find friends, Teams up, Partner services, Help center, Visit Suunto.com entries.

Primary interaction:

- Tap settings icon to open Settings.

### 6.7 Settings

Purpose: Show app settings and account configuration.

Required content:

- Back navigation to Profile.
- Account section.
- Activity & training section.
- Outdoor section.
- General section with appearance selector, unit system, start of week, screen backlight, and power management.
- Notification section.
- Social links section.
- About app section.
- Sign out button.

Primary interaction:

- Tap back to return to Profile.

### 6.8 Pairing / Device

Purpose: Show paired watch state and device-related feature entries.

Required content:

- Back navigation to Home.
- Device title.
- Watch image with connected checkmark.
- Battery and sync status.
- Sync Now action.
- SuuntoPlus Store banner.
- SuuntoPlus apps, guides, watch faces.
- Device feature list including interval workouts, sport mode customization, offline maps, music, widgets, wallet, notifications, WeChat sports, connection settings.
- Support and device management rows.

Primary interaction:

- Tap back to return to Home.

## 7. Navigation Requirements

| Trigger | Expected Result |
|---|---|
| Bottom nav Home | Show Home screen |
| Bottom nav Calendar | Show Calendar screen |
| Bottom nav Training | Show Training screen |
| Bottom nav Profile | Show Profile screen |
| Home Dashboard tab | Show Dashboard widgets |
| Home Activities tab | Show Activities feed |
| Home device entry | Show Pairing / Device screen |
| Calendar July 10 | Show Daily Page |
| Daily back button | Return to Calendar |
| Profile settings icon | Show Settings screen |
| Settings back button | Return to Profile |
| Pairing back button | Return to Home |

The first demo version uses in-page state switching rather than URL routing. Later versions can add hash routes or a framework router if shareable deep links are required.

## 8. Data Requirements

All data can be simulated in the current phase. Mock data should be realistic and internally consistent enough for product review.

Required mock datasets:

- User profile: name, bio, avatar, paired device names, follower counts.
- Device state: watch model, battery, sync timestamp, connected status.
- Dashboard widgets: current value, target value, unit, trend or progress state.
- Activity feed: sport type, date, location, duration, distance, ascent, map route.
- Calendar month: activity dates, intensity/type color, monthly totals.
- Daily detail: activity summaries, wellness values, chart samples.
- Training: weekly duration/load/distance, stacked sport distribution, intensity zones, impact scores.
- Settings: section labels, row labels, selected values.

## 9. Visual And Design Requirements

- Theme: Suunto dark mode.
- Base background: black.
- Primary surface: dark gray.
- Primary accent: Suunto cyan-blue.
- Activity colors: running yellow, cycling orange, walking green, heart-rate red, sleep purple, recovery lime.
- Typography: Proxima Nova for English UI.
- Layout: 390px phone-first canvas with iOS-like status bar, top bars, scrollable content, and bottom navigation.
- Card radius: moderate rounded corners, generally 12-14px.
- UI density: data-rich and compact, matching the source app style.
- Do not use generic marketing dashboard patterns.
- Do not use full-page screenshots as the main screen rendering.

## 10. Asset Requirements

Current local assets:

| Asset | Use |
|---|---|
| `../fonts/font/Proxima Nova Reg.otf` | Regular text |
| `../fonts/font/Proxima Nova Sbold.otf` | Semibold text |
| `../fonts/font/Proxima Nova Bold.otf` | Bold text |
| `../docs/color_variables.css` | Source color token reference |
| `../fonts/font_variables.css` | Source typography token reference |
| `../assets/map.png` | Activity and calendar map panels |
| `../assets/Watch.png` | Pairing / Device watch image |
| `../assets/Avatar.png` | Profile/avatar image |
| `../assets/profile bg.png` | Profile hero background |
| `../assets/SuuntoPlus store image.png` | Pairing banner |
| `../assets/.ShareCrouselItem 1-7.png` | Activity/profile photo thumbnails |
| `../assets/Achievement badge 1-5.png` | Profile badge row |
| `../assets/Frame 1000007317.png` | Large optional map/background source |

Future asset needs:

- More exact Figma-exported icons if icon parity becomes a priority.
- Separate route map exports for multiple activity cards if repeated maps are not acceptable.
- Additional watch/device product images for multi-device states.

## 11. Technical Approach

Current implementation:

- Single file: `../index.html`.
- Embedded CSS and JavaScript.
- Local fonts via `@font-face`.
- Local image assets only.
- No external JavaScript or CSS libraries.
- Real DOM screens using `data-screen` states.
- Home Dashboard / Activities handled as in-page tab state.
- Charts drawn with CSS bars and inline SVG.

Rationale:

- Fastest path to a reviewable, offline-friendly prototype.
- Avoids dependency installation and build setup.
- Easier to preserve visual control for Figma-like mobile UI.
- Reduces risk from chart-library styling constraints.

Potential later architecture:

- Split into `src/` modules using Vite if the demo grows.
- Move mock data into JSON or JS modules.
- Add a lightweight router for deep links.
- Replace hand-drawn charts with Apache ECharts only if chart interactivity or real data volume increases.

## 12. Chart And Widget Implementation Strategy

Recommended first version:

- Continue using CSS/SVG charts for visual parity.
- Use compact components for progress bars, stacked bars, line charts, and mini sparklines.
- Keep chart data mocked and deterministic.

Library evaluation summary:

- Apache ECharts: best option for future complex charts, heatmaps, calendars, and interactive analytics.
- Chart.js: good for simple line/bar charts, but less convenient for highly custom mobile card visuals.
- D3: most flexible, but higher implementation cost.
- FullCalendar: too heavy for the custom Suunto-style activity calendar.

Current recommendation:

- Do not introduce a chart library until data updates, hover/tap chart inspection, or complex calendar heatmaps become a real requirement.

## 13. Risks And Implementation Challenges

- Figma broad-node extraction can time out. Work should continue page-by-page and module-by-module.
- Some Figma layers are instances or symbols, so exact inner text and component details may require additional targeted MCP calls.
- Hand-drawn SVG/CSS charts are visually flexible but not ideal for production data complexity.
- Current iconography uses code-drawn or character-based approximations in places; exact icon exports may be required for stricter parity.
- Long screens require careful handling of fixed top/bottom bars and scroll padding.
- Hidden files such as `.ShareCrouselItem 1.png` work locally but may be awkward for packaging or hosting; consider renaming in a later cleanup.
- Browser validation in the current environment may block localhost access. Direct file loading is available, and static checks should remain part of validation.

## 14. Acceptance Criteria

Version 1 is acceptable when:

- `../index.html` opens locally without a build step.
- No external network dependency is required.
- All referenced fonts and images load from local project files.
- Home Dashboard and Home Activities switch correctly.
- Bottom navigation switches between Home, Calendar, Training, and Profile.
- Calendar July 10 opens Daily Page.
- Daily Page back returns to Calendar.
- Profile settings opens Settings.
- Settings back returns to Profile.
- Home device entry opens Pairing / Device.
- Pairing back returns to Home.
- All eight target pages have visible, data-rich content.
- The visual language follows Suunto dark-mode mobile UI.

## 15. Future Iteration Backlog

- Add exact icon assets from Figma for navigation, sports, settings, and device features.
- Rename hidden carousel assets to non-hidden filenames and update references.
- Add hash-based URLs for shareable screen states.
- Add active states for Calendar Diary / My Plan and Training sub-tabs.
- Add optional chart tap interactions for Daily and Training screens.
- Add multiple activity cards with unique map/route images.
- Add device sync state variants: syncing, synced, error, low battery.
- Add profile edit and achievement detail flows if needed.
- Run a visual compare pass for each screen against Figma screenshots and tune spacing, font sizes, and card heights.

