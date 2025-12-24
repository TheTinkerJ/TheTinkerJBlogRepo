# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个基于 **Pelican** 的静态博客网站项目，用于生成个人博客并部署到 GitHub Pages。

- **静态网站生成器**: Pelican 4.11.0+（使用 Python）
- **包管理器**: uv
- **Python 版本**: 3.12+
- **默认语言**: 中文 (zh)
- **部署目标**: GitHub Pages (https://TheTinkerJ.github.io)

## 项目结构

```
TheTinkerJBlogRepo/
├── content/          # 博客内容源文件（Markdown 或 reStructuredText）
├── output/           # 生成的静态网站（不要手动编辑）
├── pelicanconf.py   # 开发环境配置
├── publishconf.py   # 生产环境配置
├── tasks.py         # Invoke 任务定义
├── Makefile         # Make 构建脚本
└── pyproject.toml   # Python 依赖配置
```

## 常用命令

### 使用 Invoke（推荐）

```bash
# 构建本地版本
invoke build

# 重建（删除旧文件后构建）
invoke rebuild

# 启动本地开发服务器（默认 localhost:8000）
invoke serve

# 构建后启动服务
invoke reserve

# 构建生产版本
invoke preview

# 自动重载服务器（文件修改时自动重建）
invoke livereload

# 发布到 GitHub Pages
invoke gh_pages
```

### 使用 Make

```bash
# 生成网站（开发模式）
make html

# 清理生成的文件
make clean

# 文件修改后自动重新生成
make regenerate

# 使用生产设置生成网站
make publish

# 本地服务（默认 8000 端口）
make serve

# 开发服务器（自动重载）
make devserver

# 部署到 GitHub Pages
make github
```

## 配置文件说明

### pelicanconf.py（开发配置）
- `SITENAME`: "Maoge's Space"
- `AUTHOR`: maoge
- `TIMEZONE`: Asia/Shanghai
- `DEFAULT_LANG`: zh（中文）
- `PATH`: content（内容目录）
- Feed 生成在开发模式下已禁用

### publishconf.py（生产配置）
- 继承 pelicanconf.py 的所有设置
- `SITEURL`: https://TheTinkerJ.github.io
- 启用 feed 生成
- `RELATIVE_URLS`: False（使用绝对 URL）

## 内容创建

博客文章应放在 `content/` 目录下，支持以下格式：

- **Markdown** (`.md`) - 推荐
- **reStructuredText** (`.rst`)

每篇文章需要包含元数据头部（Markdown 示例）：

```markdown
Title: 文章标题
Date: 2025-12-24
Category: 分类
Tags: 标签1, 标签2
Author: maoge

文章内容...
```

## 开发工作流

1. 在 `content/` 目录创建或编辑 Markdown 文件
2. 运行 `invoke livereload` 启动自动重载服务器
3. 在浏览器中访问 http://localhost:8000 预览
4. 确认无误后运行 `invoke gh_pages` 部署到 GitHub Pages

## GitHub Pages 部署

- 发布分支: `main`
- 部署命令会使用 `ghp-import` 将 `output/` 目录内容推送到指定分支
- 配置了 `--no-jekyll` 标志以禁用 Jekyll 处理

## 主题

项目使用 Pelican 默认主题（notmyidea 或 simple）。自定义主题可通过在 `pelicanconf.py` 中设置 `THEME` 变量来指定。
