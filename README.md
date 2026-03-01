# Minghui Liwang Academic Homepage

基于 Jekyll 的个人学术主页项目，当前用于维护 `https://abbylliwang.github.io/`。

## 1. 项目简介

这是一个静态网站仓库，采用 [Minimal Light](https://github.com/yaoyao-liu/minimal-light) 主题进行定制。  
项目重点是内容可维护性：个人信息、科研成果、新闻、教学与服务内容均可通过 Markdown/YAML 直接更新。

主要特性：

- 纯静态站点，无后端依赖
- 支持深色模式自动切换
- 支持按年份自动整理论文列表
- 可直接部署到 GitHub Pages
- 页面内容以 Markdown/YAML 为主，便于持续更新

## 2. 技术栈与构建方式

- 静态站点框架：Jekyll `~> 3.8.5`
- 依赖管理：Bundler
- 样式：SCSS + CSS
- 页面模板：Liquid (`_layouts`, `_includes`)
- 发布方式：GitHub Pages（推荐）或本地构建静态文件

常用命令：

```bash
bundle install
bundle exec jekyll serve
bundle exec jekyll build
```

## 3. 目录结构（核心）

```text
.
├── _config.yml                  # 站点全局配置（姓名、单位、SEO、链接、主题开关）
├── index.md                     # 首页主内容（通过 include 组合各模块）
├── _layouts/
│   └── homepage.html            # 页面整体布局（头像、头部信息、社交链接、脚注）
├── _includes/
│   ├── experience.md            # 教育与经历
│   ├── news.md                  # 新闻动态
│   ├── publications.md          # 论文渲染模板（从 YAML 读取）
│   ├── projects.md              # 项目/基金/奖励
│   ├── services.md              # 学术服务
│   └── teaching.md              # 教学与指导
├── _data/
│   └── publications.yml         # 论文结构化数据（按 year 排序展示）
├── _sass/
│   ├── minimal-light.scss
│   └── minimal-light-no-dark-mode.scss
├── assets/
│   ├── css/                     # 字体与页面样式入口
│   ├── js/                      # favicon 与移动端缩放脚本
│   ├── img/                     # 头像、图标、示意图
│   └── files/                   # CV 等附件
├── _site/                       # Jekyll 构建产物（自动生成，通常不提交）
└── html_source_file/            # 历史静态快照目录（与当前 Jekyll 内容可能不同步）
```

## 4. 内容维护指南

### 4.1 修改个人基础信息

编辑 `_config.yml`：

- `title` / `position` / `affiliation` / `email`
- `keywords` / `description` / `canonical`（SEO）
- `google_scholar` / `cv_link`（头部图标链接）
- `avatar` / `favicon` / `favicon_dark`
- `auto_dark_mode` / `font` 等显示选项

### 4.2 修改首页结构与文本

编辑 `index.md`：

- 首页介绍（About）
- 研究方向（Research Interests）
- 各模块 include 的顺序与开关
- 联系方式（Contact）

### 4.3 维护新闻、教学、服务等模块

分别编辑 `_includes/*.md`：

- `_includes/news.md`
- `_includes/experience.md`
- `_includes/projects.md`
- `_includes/services.md`
- `_includes/teaching.md`

### 4.4 维护论文列表（推荐方式）

1. 在 `_data/publications.yml` 中新增条目。  
2. `publications.md` 会自动按 `year` 分组并倒序展示。

可用字段示例：

```yaml
- title: "Paper Title"
  authors: "A. Author, B. Author"
  conference_short: "IEEE TMC"
  conference: "IEEE Transactions on Mobile Computing, 2026."
  year: 2026
  notes: "Corresponding Author"
  pdf: "https://..."
  code: "https://..."
  page: "https://..."
  bibtex: "https://..."
  image: "./assets/img/teaser_example.png"
```

其中 `pdf/code/page/bibtex/image` 为可选字段。

## 5. 样式与主题定制

样式相关文件：

- `_sass/minimal-light.scss`：深色模式版本基础样式
- `_sass/minimal-light-no-dark-mode.scss`：关闭深色模式时使用
- `assets/css/style.scss`：SCSS 编译入口
- `assets/css/publications.css`：论文列表样式
- `assets/css/font.css` / `assets/css/font_sans_serif.css`：字体方案

常见定制点：

- 修改主色、链接样式、卡片阴影
- 调整头像大小、布局间距
- 切换 Serif / Sans Serif 字体
- 开启/关闭自动深色模式

## 6. 本地开发与预览

### 6.1 环境准备

- Ruby（建议 2.7+）
- Bundler

### 6.2 安装与运行

```bash
bundle install
bundle exec jekyll serve
```

浏览器访问：

- `http://127.0.0.1:4000`

### 6.3 生产构建

```bash
bundle exec jekyll build
```

构建结果输出到 `_site/`。

## 7. 部署建议

### 7.1 GitHub Pages（推荐）

1. 推送代码到默认分支。
2. 在仓库 Pages 设置中启用 GitHub Pages。
3. 确认 `_config.yml` 中 `canonical` 与实际域名一致。

### 7.2 自定义域名

- 如需启用，请在 `CNAME` 文件写入目标域名（当前文件为空）。
- 确保 DNS 记录配置正确后再启用。

## 8. 维护注意事项

- `_site/` 是生成目录，不作为源码编辑入口。
- `html_source_file/` 为历史静态版本，可能与当前页面不一致，避免误改后当作主版本发布。
- `assets/files/` 中可直接放置 CV、附录、代表作列表等可下载文件。
- 更新论文时建议统一字段，避免前端展示不齐。

## 9. 常见问题（FAQ）

### Q1: 我改了内容但页面没更新？

- 先确认编辑的是 `index.md`、`_includes/` 或 `_data/`，不是 `_site/`。
- 本地运行时重启 `jekyll serve`，或清理缓存后重试。

### Q2: 论文没有按预期显示？

- 检查 YAML 缩进是否为两个空格。
- 检查每个条目的 `year` 是否为数字。
- 检查链接字段是否写在对应条目下。

### Q3: 深色模式样式异常？

- 检查 `_config.yml` 的 `auto_dark_mode`。
- 检查 `assets/css/publications.css` 与 `_sass/minimal-light.scss` 的深色模式规则。

## 10. 许可证

本项目沿用上游主题许可证，详见 `LICENSE`。

## 11. 致谢

本项目基于以下开源项目定制：

- https://github.com/yaoyao-liu/minimal-light
- https://github.com/orderedlist/minimal
- https://github.com/pages-themes/minimal
