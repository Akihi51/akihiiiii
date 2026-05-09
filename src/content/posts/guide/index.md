---
title: Fuwari 使用指南
published: 2024-04-01
description: "如何使用这个博客模板。"
image: "./cover.jpeg"
tags: ["Fuwari", "博客", "自定义"]
category: 指南
draft: false
---

> 封面图来源：[Source](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/208fc754-890d-4adb-9753-2c963332675d/width=2048/01651-1456859105-(colour_1.5),girl,_Blue,yellow,green,cyan,purple,red,pink,_best,8k,UHD,masterpiece,male%20focus,%201boy,gloves,%20ponytail,%20long%20hair,.jpeg)

这个博客模板基于 [Astro](https://astro.build/) 构建。没有在本文提到的内容，可以继续参考 [Astro 官方文档](https://docs.astro.build/)。

## 文章 Front Matter

```yaml
---
title: 我的第一篇博客
published: 2023-09-09
description: 这是一篇 Astro 博客文章示例。
image: ./cover.jpg
tags: [前端, 记录]
category: 技术
draft: false
---
```

| 字段 | 说明 |
| --- | --- |
| `title` | 文章标题。 |
| `published` | 发布时间。 |
| `description` | 文章摘要，会显示在首页文章卡片中。 |
| `image` | 封面图路径，支持网络图片、`public` 目录图片或相对 Markdown 文件的本地图片。 |
| `tags` | 文章标签。 |
| `category` | 文章分类。 |
| `draft` | 是否为草稿；草稿不会在站点中展示。 |

## 文章存放位置

文章文件应放在 `src/content/posts/` 目录下。你也可以创建子目录，把文章和它的图片资源放在一起。

```txt
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```
