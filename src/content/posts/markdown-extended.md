---
title: Markdown 扩展示例
published: 2024-05-01
updated: 2024-11-29
description: '了解 Fuwari 支持的 Markdown 扩展能力'
image: ''
tags: [示例, Markdown, Fuwari]
category: 示例
draft: false
---

## GitHub 仓库卡片

你可以在文章中插入 GitHub 仓库卡片。页面加载时，仓库信息会从 GitHub API 获取。

::github{repo="Fabrizz/MMM-OnSpotify"}

写法如下：

```markdown
::github{repo="saicaca/fuwari"}
```

## 提示块

支持 `note`、`tip`、`important`、`warning`、`caution` 等类型。

:::note
这里适合放补充说明。
:::

:::tip
这里适合放使用技巧。
:::

:::important
这里适合放必须注意的信息。
:::

:::warning
这里适合放风险提醒。
:::

:::caution
这里适合放需要谨慎处理的内容。
:::

## 数学公式

行内公式：$E = mc^2$。

块级公式：

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
