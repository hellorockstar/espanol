# 我爱背单词 — 协作规则

## 项目概况

西班牙语词汇学习 WebApp，单文件架构（index.html），Vanilla JS + TailwindCSS CDN + DeepSeek API，数据存储在 localStorage + GitHub Gist 云同步。

## 铁律（违反即回退）

### 1. 不改 localStorage key 名

以下 key 是用户数据的命脉，修改 index.html 时不得重命名、删除或改变其读写方式：

`gh_token`、`gh_gist_id`、`ds_token`、`prismaVocab`、`ds_token_usage`、`ds_token_history`、`autoRead`、`report_history`

额外保护（不改读写方式）：`apiBaseUrl`、`apiModel`、`dict_v4_*` 系列缓存 key。

### 2. 先讨论方案，再编码

任何 index.html 改动，编码前必须产出书面方案：
- 改什么
- 入口在哪
- 交互如何
- 涉及哪些函数/模块

把需要用户拍板的决策点单独列出，明确问「方案 OK 吗？」，等用户确认才动手。不因改动小而跳过此步骤。

### 3. 绝对守护本地数据

任何清除操作必须精准隔离。不得批量清除 localStorage。不得在未确认的情况下覆盖用户数据。

## 技术备注

- 单文件 index.html（~2400 行），所有 HTML/CSS/JS 在同一个文件中
- TailwindCSS 通过 CDN 加载（cdn.tailwindcss.com）
- DeepSeek API 用于 AI 功能（造句、语法分析等），token 由用户自己的 API key 提供
- 数据同步：localStorage ↔ GitHub Gist（用户自己的 token + gist）
- 目标设备：手机浏览器（iOS Safari 为主）
