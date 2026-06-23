# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

基于 [Hux Blog](https://github.com/Huxpro/huxpro.github.io) 主题的个人技术博客，使用 Jekyll 4 构建，托管在 GitHub Pages，自定义域名 `vincent.zone`。

## Commands

```bash
# 安装 Ruby 依赖
bundle install

# 本地启动 (http://localhost:4000)
bundle exec jekyll serve
# 或
npm start

# 同时开启 grunt watch 和 jekyll serve
npm run dev

# 创建新文章
rake post title="文章标题" subtitle="副标题"

# 编译前端资源 (Less → CSS, JS minify)
grunt
```

## Architecture

### 核心目录

| 目录 | 用途 |
|------|------|
| `_posts/` | Markdown 格式的博客文章，文件名格式 `YYYY-MM-DD-slug.md` |
| `_layouts/` | Liquid 模板：`post.html`（文章页）、`page.html`（单页）、`keynote.html`（演示）、`default.html`（基础布局） |
| `_includes/` | 可复用的 Liquid 组件：导航栏、侧边栏、页脚、友链、搜索等 |
| `_site/` | Jekyll 构建输出目录，已加入 `.gitignore` |
| `less/` | 主题样式源文件，通过 Grunt 编译为 `css/` 下的 CSS |

### 技术栈

- **后端/模板**: Jekyll 4 + Liquid 模板引擎 + kramdown (GFM) + Rouge 代码高亮
- **前端构建**: Grunt → Less 编译 + UglifyJS 压缩
- **JS/CSS**: 传统 jQuery 风格（非模块化），无 ES6+ 转译
- **前端文件**: `js/vincent-blog.js` → `js/vincent-blog.min.js`；`less/vincent-blog.less` → `css/vincent-blog.css`
- **评论**: Disqus
- **统计**: Google Analytics + 百度统计
- **分页**: jekyll-paginate 插件，每页 10 篇

### 文章 Front Matter

```yaml
---
layout: post
title: "标题"
subtitle: "副标题"
date: YYYY-MM-DD
author: "Vincent"
header-img: "img/post-bg-2015.jpg"
catalog: true          # 显示目录
tags: [Tag1, Tag2]
mathjax: true          # 可选，数学公式支持
---
```

### 修改主题样式

1. 编辑 `less/` 目录下的 `.less` 文件
2. 运行 `grunt` 重新编译为 CSS
3. 代码高亮主题在 `less/highlight.less`

### 部署

推送到 GitHub 后自动部署到 `vincent.zone`（GitHub Pages 绑定自定义域名，CNAME 文件控制）。

### 注意事项

- `.gitignore` 排除 `_site`、`node_modules`、`.jekyll-cache`、日志文件、`.idea`
- `Gemfile.lock` 已被 gitignore，如果构建有问题需重新 `bundle install`
- 主题基于 Apache 2.0 License，来自 Huxpro/huxpro.github.io
