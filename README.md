# Suunto App Web Demo

本项目是一个基于 Suunto 设计系统的本地 Web Demo，用于展示 Suunto App 的核心页面、交互流和 Light / Dark 主题切换效果。

## 预览目标

- 首页 Dashboard
- Calendar 月历
- Training 训练分析页
- Profile 个人中心
- Settings 设置页
- `Settings > Appearance` 全局主题切换

## 快速开始

直接用浏览器打开 `index.html` 即可。

```text
file:///Users/xiesimin/Desktop/suunto%20app%20demo/index.html
```

无需构建，无需后端。

## 交互说明

- 底部导航可切换主页面
- Calendar 可进入 Daily Page
- Profile 可进入 Settings
- Home 可进入 Pairing / Device
- Settings 中的 `Appearance` 可切换全局主题

主题规则：

- `Automatic` = Dark
- `Dark` = Dark
- `Light` = Light

## 目录结构

```text
index.html                  主入口
docs/color_variables.css    原始色彩语义参考
docs/suunto-semantic-colors.css  运行时语义色文件
fonts/                      Proxima Nova 字体资源
assets/                     设计切图与图标资源
PRD/                        产品文档与交付说明
```

## 文档

- [主 PRD](./PRD/suunto-web-demo-prd.md)
- [交接摘要](./PRD/suunto-web-demo-handoff-summary.md)
- [AI 交付说明](./PRD/codex-ai-dialogue-delivery.md)

## 资源说明

- 所有页面使用本地资源
- 图标优先使用可变色的 SVG / mask 方式
- 主题语义以 `docs/suunto-semantic-colors.css` 为运行时依据

## 注意事项

- 这是一个 Demo，不包含真实登录、后端同步或设备连接
- 页面内容以 mock 数据呈现
- 当前布局以手机画布为主，建议在浏览器中保持合适的预览宽度

## 许可证

仅用于内部展示与评审用途。
