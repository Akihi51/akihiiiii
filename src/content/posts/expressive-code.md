---
title: Expressive Code 示例
published: 2024-04-10
description: 展示 Markdown 中代码块的高亮效果。
tags: [Markdown, 博客, 示例]
category: 示例
draft: false
---

Fuwari 使用 [Expressive Code](https://expressive-code.com/) 渲染代码块。它支持语法高亮、文件标题、行号和高亮行。

## 基础高亮

```js
console.log("这段代码会被高亮显示");
```

## 带标题的代码块

```ts title="src/example.ts"
type Post = {
	title: string;
	published: Date;
	tags: string[];
};

const post: Post = {
	title: "中文博客示例",
	published: new Date("2024-04-10"),
	tags: ["Astro", "Markdown"],
};

console.log(post.title);
```

## 高亮指定行

```ts {2,5}
function greet(name: string) {
	const message = `你好，${name}`;

	return {
		message,
		createdAt: new Date(),
	};
}
```

## 终端示例

```powershell
pnpm install
pnpm dev
```
