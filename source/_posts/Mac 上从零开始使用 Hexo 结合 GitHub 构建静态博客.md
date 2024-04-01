以下是在 Mac 上从零开始使用 Hexo 结合 GitHub 构建静态博客的完整步骤，包括安装 Homebrew：

### 步骤 1: 安装 Homebrew

打开 Mac 终端，并运行以下命令来安装 Homebrew：


```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

安装过程中可能会提示你输入你的 Mac 用户密码。

### 步骤 2: 安装 Node.js 和 npm

使用 Homebrew 安装 Node.js（它会同时安装 npm）：

```bash
brew install node
```

### 步骤 3: 安装 Hexo

使用 npm 全局安装 Hexo：

```bash
npm install -g hexo-cli
```

### 步骤 4: 创建新的 Hexo 博客

在你想要的目录中创建一个新的 Hexo 博客：

```bash
hexo init my-blog
cd my-blog
npm install
```

这里 `my-blog` 是你的博客目录名，你可以根据自己的喜好更改。

### 步骤 5: 编写你的博客文章

在 `my-blog/source/_posts` 目录下创建 Markdown 文件来编写你的博客文章。例如：

```bash
touch my-blog/source/_posts/my-first-post.md
```

### 步骤 6: 本地预览博客

在 Hexo 博客目录中生成静态文件并启动本地服务器预览博客：

```bash
hexo generate
hexo server
```

现在，你可以在浏览器中访问 `http://localhost:4000` 来查看你的博客。

### 步骤 7: 部署到 GitHub Pages

1. 在 GitHub 上创建一个新的仓库，名称必须为 `username.github.io`（其中 `username` 是你的 GitHub 用户名）。
2. 在 Hexo 博客的 `_config.yml` 配置文件中设置 GitHub Pages 相关选项：

```yaml
# Deployment
deploy:
  type: git
  repository: https://github.com/username/username.github.io.git
  branch: [main]
```

确保将 `username` 替换为你的实际 GitHub 用户名。

3. 将本地的 Hexo 博客推送到 GitHub 仓库：

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/username/username.github.io.git
git push -u origin main
```

4. 在 GitHub 仓库的设置中，找到 "GitHub Pages" 部分，并选择 `main` 分支作为你的发布源。

### 步骤 8: 自定义域名（可选）

如果你想使用自定义域名，你需要在 `_config.yml` 文件中设置 `url` 和 `root` 选项，并在域名提供商处配置 DNS 记录。

### 步骤 9: 持续更新和发布

每当你添加新的文章或更新现有文章后，你需要运行 `hexo generate` 来生成新的静态文件，并通过 `git commit` 和 `git push` 将更改推送到 GitHub。GitHub Pages 将自动从你的 `main` 分支部署更新后的博客。

### 注意事项

- 确保你的 GitHub 账户已经登录，并且你有足够的权限来创建仓库和推送代码。
- 如果你在设置过程中遇到任何问题，可以查看 Hexo 的官方文档或在社区论坛中寻求帮助。
- 如果你使用的是自定义域名，确保你的域名已经正确解析到 GitHub Pages 提供的服务。

按照这些步骤，你应该能够成功地使用 Hexo 和 GitHub Pages 搭建并部署你的博客。