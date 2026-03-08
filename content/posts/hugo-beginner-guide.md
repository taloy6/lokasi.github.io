+++
title = '我的第一个 Hugo 博客：新手完全指南'
date = 2026-03-08T19:23:11+08:00
draft = false
+++

# 如何在我的博客上发布新文章：完整流程

你好！欢迎来到我的博客。今天我来手把手教大家如何在我们的 Hugo 博客上发布一篇新文章。无论你是第一次接触，还是已经写过几篇，相信这篇指南都能帮到你。

---

## 1. 生成新文章

在本地电脑上打开终端（PowerShell 或命令提示符），进入你的博客项目根目录（例如 `D:\code\lokasi.github.io`）。

运行以下命令来创建一篇新文章（请将 `my-new-post` 替换为你想要的文件名，建议使用英文小写和短横线）：

```bash
hugo new posts/my-new-post.md
```

执行后，Hugo 会在 `content/posts/` 目录下生成一个 Markdown 文件，例如 `my-new-post.md`。文件内容开头会自动添加一些元信息（称为 **Front Matter**），默认格式可能是这样的：

```toml
+++
date = '2026-03-08T20:00:00+08:00'
draft = true
title = 'My New Post'
+++
```

**注意**：这里用的是 TOML 格式（用 `+++` 包裹，键值之间用等号 `=`）。这是 Hugo 的默认设置，我们保持统一就好。如果你更喜欢 YAML 格式（用 `---` 包裹，冒号分隔），也可以修改 `archetypes/default.md` 模板，但建议先按默认来。

---

## 2. 编辑文章内容

用你喜欢的编辑器（比如 VSCode）打开刚才生成的文件，比如 `content/posts/my-new-post.md`。

### 2.1 修改 Front Matter

- **标题**：将 `title` 改为你文章的真实标题，例如 `title = '我的第一篇博客文章'`。
- **发布日期**：通常保持自动生成的日期即可，也可以手动调整。
- **草稿状态**：`draft = true` 表示文章还不会显示在网站上。当你准备好发布时，需要将它改为 `draft = false`。

### 2.2 编写正文

在 `+++` 下方开始写文章正文，使用 Markdown 语法。例如：

```markdown
+++
title = '我的第一篇博客文章'
date = 2026-03-08T20:00:00+08:00
draft = false
+++

# 欢迎！

这是我的第一篇博客，很高兴能在这里分享知识。

## 为什么写博客？

- 记录学习过程
- 分享经验
- 与大家交流

你也可以插入代码块：

```python
print("Hello, world!")
```
```

**小技巧**：
- 插入图片：将图片放入 `static/images/` 目录，然后在文中使用 `![图片描述](/images/图片名.jpg)`。
- 添加链接：`[链接文字](https://example.com)`。

---

## 3. 本地预览

在终端运行以下命令，启动 Hugo 内置服务器：

```bash
hugo server
```

如果一切正常，你会看到类似输出：
```
Web Server is available at http://localhost:1313/lokasi.github.io/
```

打开浏览器访问该地址，你就能在博客首页看到刚刚创建的文章（如果文章是草稿，需要加上 `-D` 参数预览：`hugo server -D`）。修改文件后，浏览器会自动刷新，非常方便。

**注意**：由于我们的博客部署在子路径 `/lokasi.github.io/` 下，所以预览地址要加上这个路径。

---

## 4. 生成静态文件

当你在本地预览满意后，需要将文章生成最终的静态文件。运行：

```bash
hugo
```

这个命令会在 `public/` 目录下生成完整的网站文件（HTML、CSS、JS 等）。生成的 `public` 目录就是我们将来要部署到服务器上的内容。

---

## 5. 部署到 GitHub Pages

目前我们采用**手动部署**的方式，将生成的静态文件复制到项目根目录并推送到 GitHub。

### 5.1 复制文件

```bash
# 删除根目录下旧的生成文件（避免残留）
Remove-Item -Recurse -Force css, js, fonts, categories, page, tags, index.html, index.xml, sitemap.xml -ErrorAction SilentlyContinue

# 将 public 下的所有内容复制到根目录
Copy-Item -Recurse -Force public\* .
```

### 5.2 提交并推送到 GitHub

```bash
git add .
git commit -m "发布新文章：我的第一篇博客"
git push origin main
```

推送成功后，等待 1-2 分钟，访问你的博客网址（例如 `https://taloy6.github.io/lokasi.github.io/`），就能看到新文章了。

---

## 6. 常见问题与注意事项

### Q1：文章为什么不显示？
- 检查 `draft` 是否为 `false`。
- 确认文件保存在 `content/posts/` 目录下，文件名没有特殊字符（建议只用字母、数字、短横线）。
- 运行 `hugo server` 看是否有报错信息。

### Q2：Front Matter 格式错误怎么办？
- 如果是 TOML 格式，必须用 `+++` 包裹，键值之间用等号，例如 `title = '我的标题'`。
- 如果是 YAML 格式，用 `---` 包裹，键值之间用冒号，例如 `title: "我的标题"`。
- **不要混用两种格式**，否则 Hugo 会报错。

### Q3：图片或 CSS 加载不出来？
- 图片放在 `static/images/` 目录，引用时路径以 `/images/` 开头。
- 确保 `.nojekyll` 文件存在，否则 GitHub Pages 可能会干扰静态文件。

### Q4：如何让新文章出现在首页？
只要 `draft: false`，Hugo 会自动将文章按时间倒序显示在首页的文章列表中。

---

## 7. 进阶建议

- **使用 GitHub Actions 自动部署**：可以配置工作流，每次推送到 `main` 分支时自动生成并部署，省去手动复制文件的麻烦。
- **学习 Markdown 高级语法**：如表格、脚注、数学公式等，让文章更丰富。
- **自定义主题**：通过修改 `layouts/` 或添加 `static/css/custom.css` 来个性化博客外观。

---

现在你已经完全掌握了发布博客文章的流程，快去写下你的第一篇精彩内容吧！如果在操作中遇到任何问题，欢迎随时交流。

Happy blogging!