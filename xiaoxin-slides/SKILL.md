---
name: xiaoxin-slides
description: 一键生成蜡笔小新漫画风格的演示文稿（PDF）。输入主题后，自动创建 NotebookLM 笔记本、搜索相关资料、生成蜡笔小新风格的演示文稿并下载到指定目录。适用于任何需要演示介绍的主题。
---

# 蜡笔小新风格演示文稿生成器

一键生成《蜡笔小新》漫画风格的演示文稿（PDF），自动完成从资料搜集到下载的完整工作流。

## 使用方法

用户只需提供一个主题，例如：
- "生成 Kimi 2.5 的演示文稿"
- "帮我做一个关于 Python 编程的演示文稿"
- "创建一个介绍人工智能的演示文稿"

## 完整工作流

当用户请求生成演示文稿时，执行以下步骤：

### 1. 创建 NotebookLM 笔记本
```bash
notebooklm create "主题演示文稿" --json
```
提取返回的 notebook_id

### 2. 搜索并添加相关资料
```bash
notebooklm source add-research "主题 核心能力 技术特点 应用场景" --mode fast --import-all
```

### 3. 设置语言为中文
```bash
notebooklm language set zh_Hans
```

### 4. 生成演示文稿
使用以下提示词生成演示文稿：
```
参考《蜡笔小新》的漫画风格，以漫画一贯套路，介绍 [主题] 的核心内容。中文内容，彩色画面，特别注意中文文字生成的正确性。不要生成图标、logo。
```

命令：
```bash
notebooklm generate slide-deck "提示词" --format detailed --length default --json
```

### 5. 等待生成完成并下载
使用 Task 工具在后台等待：
- 使用 `notebooklm artifact wait` 等待任务完成
- 使用 `notebooklm download slide-deck` 下载到 `/Users/wanglimeng/opencode/yanshiwengao/`
- 文件名格式：`[主题]_slides.pdf`

## 输出示例

**成功时返回：**
- 演示文稿文件路径
- 生成的核心内容摘要

**失败时处理：**
- 检查 artifact 状态
- 如果是 rate limit，建议等待后重试
- 提供手动下载的备选方案

## 注意事项

1. **生成时间：** 演示文稿生成通常需要 5-15 分钟
2. **Rate Limiting：** 演示文稿生成可能受 Google 速率限制，如遇失败请稍后重试
3. **语言设置：** 会自动设置为简体中文
4. **目录：** 默认下载到 `/Users/wanglimeng/opencode/yanshiwengao/`
5. **格式：** 输出为 PDF 格式

## 依赖

- notebooklm-py CLI 已安装并认证
- 用户已登录 NotebookLM (`notebooklm login`)
- 输出目录已存在或可创建
