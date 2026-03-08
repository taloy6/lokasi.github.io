---
title: "My Leaning Journey"
date: 2026-03-08
draft: false
---

# 我的第一个 Hugo 博客：新手完全指南

你好！看到你用 `tree` 命令打印出的文件列表，可能会觉得有点眼花缭乱。别担心，我来帮你理清这些文件夹和文件都是干什么的，以及如何一步步把自己的博客变得有内容、有模样。

---

## 1. 整体认识：Hugo 和 GitHub Pages

简单来说，Hugo 是一个**静态网站生成器**。你用它写文章（用 Markdown 格式），它就能自动生成一堆 HTML、CSS、JS 文件，也就是一个完整的网站。然后你把生成的这些文件放到 GitHub Pages 上，别人就能访问你的博客了。

在你的项目里，**源代码**（你平时要编辑的东西）和**生成的文件**（Hugo 自动生成的，不用手动改）混在一起，这是手动部署的结果。我们后面会慢慢理清。

---

## 2. 目录结构详解（哪些是你需要关心的）

让我们从上到下，把每个重要文件夹和文件的作用说清楚。

### 📁 根目录下的重要文件

| 文件名 | 作用 |
|--------|------|
| `hugo.toml` | 这是 Hugo 的**配置文件**，相当于博客的“总开关”。你在这里设置网站标题、主题、菜单、作者信息等。 |
| `.gitignore` | 告诉 Git 哪些文件不需要跟踪（比如生成的 `public` 文件夹）。不用动它。 |
| `.gitmodules` | 记录了主题的 Git 子模块信息，方便更新主题。不用手动改。 |
| `.nojekyll` | 一个空文件，作用是告诉 GitHub Pages “不要用 Jekyll 处理我的网站”。没有它你的 CSS 可能加载不出来。已经加上了，放心。 |
| `index.html`、`css/`、`js/`、`fonts/` 等 | 这些都是 Hugo **生成出来的静态文件**，也就是最终网站的内容。**你不用手动编辑它们**，每次修改文章或配置后，Hugo 会重新生成并覆盖它们。 |

### 📂 核心源码目录（你需要编辑的地方）

#### `content/`
这是你的**文章和页面**的家。里面默认有一个 `posts/` 子目录，用来放博客文章。

- 你的第一篇文章 `my-first-post.md` 就放在 `content/posts/` 里。
- 如果你想创建一个“关于我”页面，可以在 `content/` 下新建 `about.md`。
- 每个 Markdown 文件的开头都有两行 `---` 包围的“Front Matter”，用来写标题、日期、标签等信息。

#### `themes/`
这里存放你安装的主题。你用的是 `newsroom` 主题，所有主题文件都在 `themes/newsroom/` 里。**原则上不要直接修改这里的文件**，否则更新主题时会丢失你的改动。如果你想自定义主题，可以用后面的方法覆盖。

#### `static/`
存放**不需要 Hugo 处理**的静态文件，比如你自己上传的图片、下载的字体、额外的 CSS/JS 文件。放入这个目录的文件，在生成网站时会原封不动地复制到根目录。例如：

- 你想在文章里放一张照片 `me.jpg`，可以放到 `static/images/me.jpg`，然后在文章里用 `![我](/images/me.jpg)` 引用。
- 如果你要添加自定义 CSS，可以新建 `static/css/custom.css`，然后在主题的配置里或者通过修改模板来引入它。

#### `layouts/`
如果你想**修改主题的外观**，这里是你的“战场”。你可以把主题中想要修改的模板文件（例如 `themes/newsroom/layouts/index.html`）复制到 `layouts/` 相同路径下，然后随意修改。Hugo 会优先使用 `layouts/` 下的文件。

#### `assets/`
与 `static/` 类似，但这里面的文件可以被 Hugo 的管道处理（比如 Sass 编译、JS 打包）。对于新手来说，暂时用不到。

#### `archetypes/`
存放**文章模板**。当你运行 `hugo new posts/xxx.md` 时，Hugo 会使用这里的模板生成新文件。你可以修改 `archetypes/default.md` 来给每篇文章自动添加一些常用 Front Matter（比如标签、分类）。

#### `data/`
存放网站的数据文件（如 JSON、YAML），可以在模板中读取。新手可以先忽略。

#### `i18n/`
多语言翻译文件。如果你不需要双语博客，可以不管。

#### `resources/`
Hugo 的缓存目录，存放生成的资源（比如处理过的图片）。**不要手动修改**，可以安全地忽略。

### 📁 生成的目录（你不用管）

#### `public/`
这是 Hugo 运行 `hugo` 命令后生成的**完整网站**，所有最终 HTML、CSS、JS 都在里面。你之前手动把它复制到了根目录。现在你应该明白了：根目录下的那些 `index.html`、`css/` 等，其实就是 `public/` 的内容。

#### `categories/`、`tags/`、`page/` 等
这些也是生成的归档页面，比如按分类、标签、分页组织的文章列表。

---

## 3. 如何改造博客内容（写文章、建页面）

### ✍️ 写一篇新文章

1. 在终端（确保在项目根目录）运行：
   ```bash
   hugo new posts/我的第二篇文章.md
   ```
2. 用 VSCode 打开 `content/posts/我的第二篇文章.md`，你会看到类似这样的内容：
   ```markdown
   ---
   title: "我的第二篇文章"
   date: 2026-03-08T18:30:00+08:00
   draft: true
   ---
   ```
3. 把 `draft: true` 改为 `false`（否则文章不会显示）。
4. 在 `---` 下方用 Markdown 写你的正文。例如：
   ```markdown
   ---
   title: "我的第二篇文章"
   date: 2026-03-08
   draft: false
   ---

   这是正文。**支持加粗**，也可以[加链接](https://example.com)。

   - 列表项1
   - 列表项2
   ```
5. 保存文件。

### 📄 创建一个“关于我”页面

1. 运行：
   ```bash
   hugo new about.md
   ```
2. 编辑 `content/about.md`，设置 `draft: false`，写下你的自我介绍。
3. 如果你想让“关于”链接出现在导航菜单中，需要在 `hugo.toml` 的 `[menu]` 部分添加一项（参考下面）。

### 🖼️ 在文章里插入图片

- 将图片（例如 `cat.jpg`）放到 `static/images/` 目录下。
- 在 Markdown 中引用：`![一只猫](/images/cat.jpg)`

---

## 4. 如何改造博客页面（修改外观）

### 🎨 修改主题配置（最简单）

打开 `hugo.toml`，这是调整主题外观的最快方式。参考 `themes/newsroom/exampleSite/config.toml`，你可以添加作者信息、社交链接、更改颜色等。

例如，在 `[params]` 下添加：
```toml
[params]
  author = "你的名字"
  description = "这是我的技术博客"
  github = "你的GitHub用户名"
  avatar = "/images/avatar.jpg"   # 需要自己放头像到 static/images/
```
保存后重新生成，效果会变化。

### 🖌️ 自定义 CSS

如果你想修改字体、颜色等样式，可以这样做：

1. 创建 `static/css/custom.css` 文件，写上你自己的 CSS 规则，例如：
   ```css
   body { background-color: #f0f0f0; }
   .nav { background: #333; }
   ```
2. 需要让主题引入这个文件。通常你可以在主题的配置中指定额外 CSS，或者修改模板。最简单的办法是复制主题的 `layouts/_partials/head.html` 到 `layouts/_partials/head.html`，然后在其中添加：
   ```html
   <link rel="stylesheet" href="/css/custom.css">
   ```
3. 重新生成后，自定义样式就会生效。

### 🧱 修改页面布局

如果你想大幅改变某个页面（比如首页、文章页）的 HTML 结构，可以通过覆盖主题模板实现：

1. 找到要修改的模板文件，例如首页模板在 `themes/newsroom/layouts/index.html`。
2. 将该文件复制到你的项目 `layouts/` 目录下相同路径（`layouts/index.html`）。
3. 编辑这个副本，加入你的 HTML 和 Hugo 模板语法（可以参考主题的文档或示例）。

**注意**：这需要一点 HTML 和 Hugo 模板知识，可以先从简单调整开始。

### 🔗 修改菜单

你已经在 `hugo.toml` 中配置了菜单项，如果想要添加新的链接（比如“关于”），可以这样：
```toml
[menu]
  [[menu.main]]
    identifier = "about"
    name = "关于"
    url = "/about/"
    weight = 3
```

---

## 5. 如何预览和部署更新

### 本地预览
在项目根目录运行：
```bash
hugo server
```
然后打开浏览器访问 `http://localhost:1313/lokasi.github.io/`（注意你的 baseURL 是子路径）。修改文件后，浏览器会自动刷新。

### 生成并部署
当你在本地满意后，需要把更新推送到 GitHub 才能让网站更新。

由于你目前是手动部署模式，需要执行以下步骤：

1. 生成最新静态文件：
   ```bash
   hugo --cleanDestinationDir
   ```
2. 删除根目录下旧的生成文件（避免残留）：
   ```bash
   Remove-Item -Recurse -Force css, js, fonts, categories, page, tags, index.html, index.xml, sitemap.xml -ErrorAction SilentlyContinue
   ```
3. 将新生成的 `public/` 内容复制到根目录：
   ```bash
   Copy-Item -Recurse -Force public\* .
   ```
4. 提交并推送到 GitHub：
   ```bash
   git add .
   git commit -m "更新博客"
   git push origin main
   ```

**强烈建议**：配置 GitHub Actions 自动部署，这样你只需要 `git push` 源码，网站就会自动更新。需要的话我可以提供配置步骤。

---

## 6. 常见问题

### Q: 文章为什么不显示？
- 检查文件头部的 `draft` 是否设置为 `false`。
- 确认文件保存在 `content/posts/` 下，且文件名格式为 `YYYY-MM-DD-标题.md`。

### Q: 修改了配置但没生效？
- 运行 `hugo server` 会热加载，但如果你修改了 `hugo.toml`，可能需要重启服务器。
- 确保没有语法错误，可以用 `hugo` 命令测试是否能正常生成。

### Q: 自定义 CSS 没加载？
- 确认文件放在 `static/css/custom.css`，并且在模板中正确引用了。
- 检查浏览器开发者工具（F12）的 Network 标签，看 CSS 文件是否请求成功。

### Q: 头像或图片显示 404？
- 确认图片在 `static/images/` 下，并且在 Markdown 或配置中引用的路径以 `/images/xxx.jpg` 开头。
- 注意大小写和文件名拼写。

---

## 7. 下一步建议

- **写几篇文章**，让博客充实起来。
- **调整主题配置**，让它更符合你的审美。
- **学习 Markdown 语法**，让文章排版更漂亮。
- **尝试 GitHub Actions**，简化部署流程。

记住，整个项目里你主要关心的是：
- `content/`（文章和页面）
- `static/`（自己上传的图片、CSS）
- `hugo.toml`（配置）
- `layouts/`（如果你想改模板）

其他文件夹大多是 Hugo 自己维护的，不用怕弄乱。

如果你在操作中遇到任何问题，随时可以提问。祝你写博客愉快！