---
title: test
published: 2026-05-09
description: '测试一下博客功能的使用'
image: ''
tags: [Playwright,博客,测试]
category: '测试'
draft: false 
lang: ''
---
# Playwirght 入门

## 安装Playwright

- 安装 Playwright 库

```python
pip install playwright
```

- 安装浏览器驱动（Chrome、Firefox、WebKit）：

```python
playwright install
```

## Playwright基础操作

- 从 Playwright 的同步 API 中导入 `sync_playwright`

```python
from playwright.sync import sync_playwright #同步写法（sync）
from playwright.async_api import async_playwright #异步写法（async）

```

- 简单代码示例

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()
    
    page.goto("https://playwright.dev")

    print("页面标题:", page.title())

    # 截图并保存
    page.screenshot(path="img/playwright.png")

    # Get started
    # 等待按钮出现
    page.get_by_role("link", name="Get started").wait_for()
    # 点击
    page.get_by_role("link", name="Get started").click()

    # 在文档页面搜索“agent”
    page.wait_for_load_state("networkidle") # 等待页面加载完成
    page.keyboard.press("Control+K")  # 打开搜索框
    page.get_by_placeholder("Search docs").fill("agent")
    page.wait_for_timeout(3000)
    page.keyboard.press("Enter")
    # 获取搜索结果的标题
    title = page.locator("h1").text_content()
    print(title)

    page.wait_for_timeout(5000)

    browser.close()
```

- 打开网页

```python
page.goto("https://playwright.dev")
```

- 等待页面加载

```python
page.wait_for_load_state("networkidle") #等所有网络请求结束
```

- 页面刷新

```

```

- 前进/后退

```

```

