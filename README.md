# 我的博客

这是我的个人博客项目，用于记录技术、学习和生活内容。

## 来源说明

本项目基于开源博客主题 [Fuwari](https://github.com/saicaca/fuwari) 修改定制。原项目作者与模板版权归原项目维护者所有，本仓库主要包含个人化配置、样式调整和内容修改。

## 使用方式

1. 在 `src/config.ts` 中修改站点信息、导航和个人资料。
2. 在 `src/content/posts/` 中编写或修改博客文章。
3. 使用 `pnpm dev` 启动本地开发服务。
4. 使用 `pnpm run build` 构建静态站点。

## 常用命令

| 命令 | 说明 |
| --- | --- |
| `pnpm install` | 安装依赖 |
| `pnpm dev` | 启动本地开发服务 |
| `pnpm run check` | 检查 Astro / TypeScript 类型 |
| `pnpm run build` | 构建网站到 `dist/` |
| `pnpm preview` | 本地预览构建结果 |
| `pnpm new-post <filename>` | 创建新文章 |

## 部署

推荐部署到 Vercel：

- Framework Preset: `Astro`
- Install Command: `pnpm install`
- Build Command: `pnpm run build`
- Output Directory: `dist`
