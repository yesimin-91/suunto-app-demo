# Suunto App Web Demo AI 生成过程记录

## 1. 文档说明

本文件用于交付阶段证明我使用 Codex 完成 Suunto App Web Demo 的过程，重点展示：

- 我如何通过提示词驱动 AI 生成 Demo
- 我如何逐步拆解页面、交互、主题和资源问题
- AI 如何根据指令完成实现、修正和验证

说明：

- 如果评审要求“完整聊天原文”，应补充你在其他线程中的实际原始对话。
- 当前版本采用“开发过程总结 + 提示词应用说明”的方式，更适合体现提示词能力。
- 本文内容基于当前仓库中的代码、PRD、资源、验证产物和 git 提交记录整理。

## 2. 项目目标

目标是生成一个本地可运行的 Suunto App Web Demo，用浏览器直接打开 `index.html` 即可查看，满足以下要求：

- 还原 Suunto App 关键页面
- 覆盖 Home、Calendar、Daily、Training、Profile、Settings、Pairing
- 使用单文件方式实现核心 Demo
- 支持 `Settings > Appearance` 全局 Light / Dark 主题切换
- 不依赖后端和构建流程

## 3. 为什么这份文档能证明 Codex 使用能力

评审要考察的通常不是“有没有使用 AI”，而是“能不能把 AI 当成执行工具”。

这个项目的过程可以清楚体现以下能力：

- 能把大任务拆成连续的小任务
- 能给出足够明确的页面和交互指令
- 能在实现后继续追问优化、修正和补齐
- 能围绕 Figma、主题系统、页面状态、资源资产做迭代
- 能让 AI 最终产出代码、文档和验证材料

## 4. 仓库中的过程证据

当前仓库可以直接作为 AI 执行过程的证据，主要包括：

- 主实现文件：`index.html`
- 主题语义色文件：`docs/suunto-semantic-colors.css`
- 需求文档：`PRD/suunto-web-demo-prd.md`
- 交接文档：`PRD/suunto-web-demo-handoff-summary.md`
- Figma 对齐与页面验证中间产物：`tmp/` 目录下大量截图、上下文、变量文件
- 资源整理结果：`assets/` 与 `assets/icons/figma/`

git 提交记录也能看出明显的两阶段过程：

1. `295c89f Add Suunto app web demo`
2. `d36bf67 Polish Suunto demo light mode and icon styling`

这说明开发过程至少经历了：

- 第一阶段：把 Demo 主体搭出来
- 第二阶段：继续做 light mode、图标、语义色和细节打磨

## 5. AI 生成 Demo 的过程总结

以下内容建议作为你交付时的主叙事。写法上采用“我给 AI 的指令类型 + AI 完成的结果”。

### 阶段 1：定义目标和交付形式

**我给 AI 的任务方向**

```text
帮我基于 Suunto App 设计做一个本地可运行的 Web Demo。
要求是手机视图、可直接打开、不依赖后端和构建流程。
```

**这类提示词的作用**

- 先锁定交付物类型，不让 AI 发散成原型说明或技术方案
- 明确“本地可运行”与“单文件可交付”要求
- 提前限制技术边界，减少后续返工

**AI 产出结果**

- 形成以 `index.html` 为核心的单文件 Demo 方案
- 使用本地资源、内嵌样式和脚本完成渲染
- 让项目能直接通过浏览器打开

**对应仓库证据**

- `index.html`
- `PRD/suunto-web-demo-prd.md` 中对单文件交付的描述

### 阶段 2：明确页面范围和信息架构

**我给 AI 的任务方向**

```text
把 Demo 页面范围定下来，至少包括首页、日历、训练、个人页、设置和设备页。
底部导航要能在主页面之间切换，详情页通过页面内状态切换打开。
```

**这类提示词的作用**

- 先定义“做哪些页面”，防止 AI 只做一两个页面示意
- 把导航方式也一起规定，避免 AI 默认做多页面路由站点
- 让 Demo 从一开始就具备“可浏览、可演示”的结构

**AI 产出结果**

- 构建了 Home、Calendar、Daily、Training、Profile、Settings、Pairing 这些页面状态
- 实现了底部导航切换与局部详情页跳转
- 页面切换采用单页内状态更新，而不是路由跳转

**对应仓库证据**

- `index.html` 中的 `data-screen="home" / "calendar" / "daily" / "training" / "profile" / "settings" / "pairing"`
- `PRD/suunto-web-demo-prd.md` 的页面范围与导航矩阵

### 阶段 3：先完成 Demo 主体页面

**我给 AI 的任务方向**

```text
先把主要页面内容搭出来，优先保证结构完整、视觉接近设计稿、数据丰富，先不用接真实数据。
```

**这类提示词的作用**

- 明确“先完成主干，再逐步精修”
- 把重点放在结构和内容密度，而不是业务逻辑
- 允许 AI 使用 mock data 快速把页面做完整

**AI 产出结果**

- 首页搭建了大量 widget
- Calendar 做了月历、汇总卡片和活动入口
- Daily Page 做了日详情、睡眠、心率、步数和图表模块
- Training、Profile、Settings、Pairing 各自具备完整内容块

**对应仓库证据**

- `index.html` 中完整的页面结构
- `PRD/suunto-web-demo-prd.md` 中对每页 required content 的描述

### 阶段 4：把交互从静态页面升级为可演示 Demo

**我给 AI 的任务方向**

```text
不要只做静态长图，要做成可交互的页面。
需要支持底部导航、从 Calendar 进入日详情、从 Profile 进入 Settings、从 Home 进入设备页。
```

**这类提示词的作用**

- 明确要求“真实 DOM + 交互状态”
- 避免 AI 只输出视觉稿式页面拼接
- 让 Demo 具备真实演示价值

**AI 产出结果**

- 主页面通过底部导航切换
- Calendar 可进入 Daily Page
- Profile 可进入 Settings
- Home 可进入 Pairing / Device

**对应仓库证据**

- `index.html` 内的导航按钮与状态切换脚本
- `PRD/suunto-web-demo-prd.md` 和 `PRD/suunto-web-demo-handoff-summary.md` 中的导航规则

### 阶段 5：把主题切换设为核心能力

**我给 AI 的任务方向**

```text
Settings 里要有 Appearance，并且切换的是全局主题，不是只切换设置页。
Automatic 和 Dark 都渲染 Dark，Light 渲染 Light，刷新后要保留状态。
```

**这类提示词的作用**

- 直接把评审重点变成实现重点
- 明确主题规则，避免 AI 自作主张接系统主题
- 明确持久化要求，让 Demo 更像完整产品

**AI 产出结果**

- 在 Settings 中加入 Appearance 分段控件
- 实现全局 `data-theme` 切换
- 用 `localStorage` 持久化 appearance mode
- 让所有关键页面跟随 Light / Dark 切换

**对应仓库证据**

- `index.html` 中 `data-appearance-option`
- `index.html` 中 `resolveThemeFromAppearance()`、`setAppearanceMode()`、`localStorage`
- `docs/suunto-semantic-colors.css`
- `PRD/suunto-web-demo-prd.md` 中的 Theme And Color Requirements

### 阶段 6：围绕 Figma 做视觉对齐

**我给 AI 的任务方向**

```text
继续按照 Figma 设计稿校对页面，把颜色、组件、图标、卡片、地图、训练模块和个人页细节往设计稿靠。
```

**这类提示词的作用**

- 把 AI 从“功能完成”推进到“视觉对齐”
- 提示 AI 不只是写代码，还要比对设计资源和局部截图
- 让后续迭代有明确标尺

**AI 产出结果**

- 补充和替换大量本地图标与资源
- 为 Calendar、Training、Profile、Settings、Map 等模块做针对性校正
- 输出了大量 Figma 相关中间验证文件

**对应仓库证据**

- `assets/icons/figma/`
- `assets/figma/`
- `tmp/calendar_figma/`
- `tmp/training_figma/`
- `tmp/profile_figma/`
- `tmp/settings_figma/`
- `tmp/map_figma/`

### 阶段 7：继续打磨 light mode 和图标体系

**我给 AI 的任务方向**

```text
继续修正 Light mode，检查所有页面在浅色主题下的背景、文字、卡片、图标和边框是否一致。
```

**这类提示词的作用**

- 把“主题切换可用”升级为“主题切换稳定”
- 强迫 AI 从局部功能检查上升到全局一致性检查
- 让 Demo 更符合验收标准

**AI 产出结果**

- 补齐多处 light mode 样式
- 让 Home、Calendar、Daily、Training、Profile、Pairing 在浅色模式下保持统一
- 修正多类图标和界面色彩

**对应仓库证据**

- `d36bf67 Polish Suunto demo light mode and icon styling`
- `index.html` 中大量 `html[data-theme="light"]` 样式
- `docs/suunto-semantic-colors.css`

### 阶段 8：整理需求文档和交接材料

**我给 AI 的任务方向**

```text
基于当前已经实现的 Demo，整理一份完整 PRD 和一份交接摘要，要求内容和实际实现保持一致。
```

**这类提示词的作用**

- 让 AI 不只是生成代码，还要补齐交付文档
- 明确要求“以已实现内容为准”，避免文档写成未来规划
- 让产品、设计、研发都能用同一份材料对齐

**AI 产出结果**

- 输出完整 PRD
- 输出中英双语的 handoff summary
- 把实现范围、交互规则、主题规则、技术约束和验收标准文档化

**对应仓库证据**

- `PRD/suunto-web-demo-prd.md`
- `PRD/suunto-web-demo-handoff-summary.md`

## 6. 这份项目最能体现的提示词能力

如果要总结我在这个项目里的提示词应用能力，重点不在“某一句提示词多华丽”，而在以下几种能力：

### 6.1 先收边界，再让 AI 执行

我不是一开始就让 AI “随便生成一个 Demo”，而是限定了：

- 本地运行
- 单文件实现
- 手机视图
- 不接后端
- 重点页面范围
- 关键交互路径
- 全局主题切换

这会大幅提高 AI 第一次输出的可用性。

### 6.2 先做主干，再做精修

先让 AI 完成页面和交互主干，再继续要求：

- 视觉对齐 Figma
- 补图标
- 修 light mode
- 调整滚动和 header collapse

这种分阶段提示比一次性提出全部要求更容易得到稳定结果。

### 6.3 明确指出“全局”要求

比如主题切换时，我不是只说“做一个 Light / Dark 切换”，而是强调：

- 全局切换
- 所有关键页面都要受影响
- `Automatic = Dark`
- 刷新后保留状态

这类约束能直接减少 AI 误解。

### 6.4 用“校对”和“继续修正”驱动迭代

在 Demo 项目里，第一次结果通常只能达到“能看”，要到“能交付”还需要多轮修正。  
因此高质量提示词并不只是生成，还包括：

- 继续对齐设计稿
- 检查浅色模式是否遗漏
- 修正图标和边框表现
- 保持文档与实现一致

## 7. 交付时建议如何介绍这份文档

你可以这样说明：

> 本文档不是单纯的聊天摘录，而是我使用 Codex 生成 Suunto App Web Demo 的过程说明。  
> 我重点展示了如何通过提示词定义目标、拆解页面、推进交互实现、完成主题切换、进行 Figma 对齐，并最终整理交付文档。  
> 这样可以更直接体现我使用 AI 工具完成实际项目的能力。

## 8. 如果评审要求更强的“完整对话原文”

你可以在本文件后面继续追加一个附录：

### 附录 A：原始对话记录

按时间顺序粘贴你和 AI 的实际对话，建议每一轮都保留：

- 我的原始提示词
- AI 的主要回复
- 这一轮产出的代码或页面结果

### 附录 B：提示词优化示例

建议额外举 2 到 3 组例子：

- 模糊提问版本
- 优化后提问版本
- 为什么优化后更有效

这样会更容易让评审看出你不是“碰运气用 AI”，而是真的会驱动 AI 干活。

## 9. 当前版本的结论

这次项目最适合交付的 AI 协作材料，不应该只是“我和 AI 聊了什么”，而应该是：

- 我如何给出实现指令
- AI 如何一步步生成 Demo
- 我如何继续追问和修正
- 最终如何沉淀为代码、文档和验证材料

从这个角度看，本文件已经更接近一个能通过考核的版本。
