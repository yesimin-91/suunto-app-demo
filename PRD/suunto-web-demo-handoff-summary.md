# Suunto App Web Demo Handoff Summary

## 1. Project Overview / 项目概览

| Item | 中文 | English |
|---|---|---|
| Project | Suunto App Web Demo | Suunto App Web Demo |
| Purpose | 用本地 Web Demo 展示 Suunto App 的核心页面与主题切换效果。 | Showcase the core Suunto app screens and theme switching in a local web demo. |
| Entry | `../index.html` | `../index.html` |
| Theme source | `../docs/suunto-semantic-colors.css` | `../docs/suunto-semantic-colors.css` |
| Design source | Figma `App Colors 2.0` | Figma `App Colors 2.0` |

## 2. Core Goal / 核心目标

- 中文：通过 `Settings > Appearance` 切换全局 Light / Dark mode，完整展示同一套 UI 的双主题效果。
- English: Use `Settings > Appearance` to switch the global Light / Dark theme and demonstrate the same UI in both modes.
- 中文：当前界面统一使用 16px 左右边距体系，主题切换只改颜色，不改布局。
- English: The current interface uses a unified 16px side-margin system, and theme switching only changes colors, not layout.

## 3. Scope / 范围

### In Scope / 已实现范围

- Home Dashboard
- Calendar
- Calendar Daily Page
- Training
- Profile
- Settings
- Pairing / Device
- Global bottom navigation
- Profile scroll collapse interaction
- Global theme switching

### Out of Scope / 不包含

- Real login / cloud sync / Bluetooth pairing
- Real backend data
- Native app behaviors
- Route-based deep linking
- A true system-linked automatic theme mode

## 4. Screen Summary / 页面摘要

| Screen | 中文说明 | English summary |
|---|---|---|
| Home Dashboard | 首页仪表盘，展示多个运动数据 Widgets。 | Home dashboard with multiple fitness widgets. |
| Calendar | 月历视图，展示月度活动与汇总。 | Monthly calendar with activity dots and summary cards. |
| Calendar Daily Page | 单日详情页，展示当天运动与健康数据。 | Daily detail page for activity and wellness data. |
| Training | 训练分析页，展示训练区间与周数据。 | Training analytics page with weekly breakdown. |
| Profile | 个人中心，展示头像、统计、运动分布、徽章与入口。 | Profile page with avatar, stats, sports breakdown, badges, and entry points. |
| Settings | 设置页，重点是 Appearance 主题切换。 | Settings page focused on Appearance theme switching. |
| Pairing / Device | 设备配对页，展示手表状态与设备功能入口。 | Device pairing page with watch status and device features. |

## 5. Navigation / 导航规则

| Trigger | Result |
|---|---|
| Bottom nav `Feed` | Open Home Dashboard |
| Bottom nav `Calendar` | Open Calendar |
| Bottom nav `Trends` | Open Training |
| Bottom nav `Profile` | Open Profile |
| Home device entry | Open Pairing / Device |
| Calendar July 10 | Open Calendar Daily Page |
| Profile settings action | Open Settings |
| Settings back | Return to Profile |
| Pairing back | Return to Home |

## 6. Theme Rules / 主题规则

- `Automatic` = Dark
- `Dark` = Dark
- `Light` = Light
- Theme switching must affect all major screens
- UI chrome, text, surface, border, and icon colors should follow semantic theme tokens
- Settings appearance switching must not change spacing or element positions

## 7. Data / Assets / Implementation

### Data / 数据

- Mock data only
- No CRUD
- Values should remain realistic and internally consistent

### Assets / 资源

- Local fonts
- Local icons and exported images
- Semantic color token file
- Avoid external runtime dependencies

### Implementation / 实现

- Single-file demo in `../index.html`
- No build step or external runtime dependency required for core rendering
- In-page state switching
- Theme persisted via `localStorage`
- Real DOM rendering, not screenshots

## 8. Acceptance Criteria / 验收要点

- `index.html` opens locally without a build step
- Bottom nav works
- Calendar to Daily Page works
- Profile to Settings works
- Home to Pairing works
- `Settings > Appearance` switches global theme
- Light mode and Dark mode both render correctly across the demo
- Selected theme persists after refresh

## 9. Risks / 风险

- Demo may change without PRD sync
- Some icons still depend on asset parity
- Single-file implementation is easy to review but harder to scale

## 10. Handoff Note / 交接备注

- 中文：研发以此页为快速交接入口，完整细节请回看 `PRD/suunto-web-demo-prd.md`。
- English: Use this page as the quick handoff entry; refer back to `PRD/suunto-web-demo-prd.md` for full details.
