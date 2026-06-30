# VEP 项目规范

## 技术栈

- **静态站点**：Jekyll（GitHub Pages 部署）
- **主题**：Just the Docs（2026-06-30 从 minima 迁移）
- **包管理**：Bundler（Gemfile），使用 `github-pages` gem
- **集合**：`veps`（目录 `_veps/`，输出 `/veps/`）

## 主题 — Just the Docs

**配置要点：**

- `_config.yml` 中用 `remote_theme: just-the-docs/just-the-docs` 而非 `theme:`
- `search_enabled: true` 开启搜索
- `heading_anchors: true` 开启标题锚点
- `color_scheme: light` 配色
- `ga_tracking` 可用于 Google Analytics
- 插件仅列必要的，目前仅 `jekyll-feed`
- 集合配置使用 `permalink: /:collection/:name`

**页面布局：**

- 普通页面使用 `layout: default`，添加 `nav_order` 控制侧边栏顺序
- 普通页面应显式添加 `permalink`（如 `/about/`）
- VEP 文档使用 `_layouts/vep.html`（继承 `default` 布局）
- 侧边栏子层级通过 `parent` 和 `grand_parent` front matter 实现

**集合处理：**

- `_veps/` 中的文档由 `_layouts/vep.html` 渲染
- VEP 文档添加 `nav_order` 后自动出现在侧边栏（不需要 `veps.md`）
- 索引页 `_veps/vep-0000.md` 通过 Liquid `{% raw %}{% for vep in site.veps %}{% endraw %}` 遍历展示列表

## VEP 文档规范

每篇 VEP 必须包含以下 front matter：

```yaml
---
vep: <编号>
title: <标题>
nav_title: VEP <编号>  # 可选，侧边栏显示名称，默认使用 title
status: 草稿 | 已接受 | 已实现 | 已拒绝 | 已撤回 | 终稿
type: 标准 | 流程 | 信息
nav_order: <数字>
created: YYYY-MM-DD
updated: YYYY-MM-DD  # 可选
author: <作者名>      # 可选
---
```

- `nav_order` 必填，决定侧边栏显示顺序（首页=1，VEP 索引=2，VEP 1=3...）

## 代码风格

- `_config.yml` 选项按功能分组，空行分隔
- Liquid 模板尽量简洁
- 自定义 CSS 放在 `_sass/custom/custom.scss`（just-the-docs 自动加载）
- 状态和类型字段使用中文（草稿/已接受/已实现/已拒绝/已撤回/终稿、标准/流程/信息）

## Git 提交规范

- 写完一个功能立即提交
- 提交信息格式：`<type>: <描述>`
- 类型：`feat` / `fix` / `style` / `refactor` / `docs`
