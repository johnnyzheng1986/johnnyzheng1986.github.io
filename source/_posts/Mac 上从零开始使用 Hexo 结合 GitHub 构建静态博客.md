以下是重新整理的步骤，指导你在 Mac 上安装 Homebrew，使用 Hexo 创建静态博客，并将其部署到 GitHub Pages：

### 第 1 步：在 Mac 上安装 Homebrew

打开 Mac 终端，并运行以下命令来安装 Homebrew：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 第 2 步：安装 Node.js 和 npm

使用 Homebrew 安装 Node.js，这会自动为你安装 npm：

```bash
brew install node
```

### 第 3 步：安装 Hexo

通过 npm 全局安装 Hexo 静态网站生成器：

```bash
npm install -g hexo-cli
```

### 第 4 步：创建新的 Hexo 博客

在你想要的目录中初始化一个新的 Hexo 博客：

```bash
hexo init my-blog
cd my-blog
npm install
```

这里的 `my-blog` 是你的博客目录名，可以根据你的喜好进行更改。

### 第 5 步：编写博客文章

在 `my-blog/source/_posts` 目录下创建 Markdown 文件来编写你的博客文章。例如：

```bash
touch my-blog/source/_posts/my-first-post.md
```

### 第 6 步：本地预览博客

在 Hexo 博客目录中生成静态文件并启动本地服务器来预览你的博客：

```bash
hexo generate
hexo server
```

现在，你可以在浏览器中访问 `http://localhost:4000` 来查看你的博客。

### 第 7 步：部署到 GitHub Pages

1. 在 GitHub 上创建一个新的仓库，名称必须为 `username.github.io`（其中 `username` 是你的 GitHub 用户名）。
2. 在 Hexo 博客的 `_config.yml` 配置文件中设置 GitHub Pages 相关选项，如果你使用 SSH 方式克隆和推送，配置如下：

   ```yaml
   deploy:
     type: git
     repository: git@github.com:username/username.github.io.git
     branch: [main]
   ```

   如果你使用个人访问令牌 (PAT) 作为 HTTPS 密码，配置如下：

   ```yaml
   deploy:
     type: git
     repository: https://github.com/username/username.github.io.git
     branch: [main]
   ```

3. 将本地的 Hexo 博客推送到 GitHub 仓库。如果你使用 SSH，命令如下：

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin git@github.com:username/username.github.io.git
   git push -u origin main
   ```

   如果你使用 HTTPS URL，确保你已经创建了一个个人访问令牌并保存好，然后在推送时输入你的 GitHub 用户名和个人访问令牌作为密码。

### 第8步：编译

内容推送到github上后，默认会使用Jekyll进行编译，但是经常会报错，可以改为下面方式。
1. 在你的仓库中，前往 Settings > Pages > Source，并将 Source 改为 GitHub Actions。

2. 在你的仓库中创建 .github/workflows/pages.yml 文件，并填入以下内容（将 16 替换为你的 Node.js 版本）：

```yaml
name: Pages

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js 16.x
        uses: actions/setup-node@v2
        with:
          node-version: '16'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
  ```
部署完成后，前往 https://username.github.io 查看网站。


### 第 8 步：自定义域名（可选）

如果你想使用自定义域名，你需要在 `_config.yml` 文件中设置 `url` 和 `root` 选项，并在域名提供商处配置 DNS 记录。

### 第 9 步：持续更新和发布

每当你添加新的文章或更新现有文章后，你需要运行 `hexo generate` 来生成新的静态文件，并通过 `git commit` 和 `git push` 将更改推送到 GitHub。GitHub Pages 将自动从你的 `main` 分支部署更新后的博客。

### 注意事项

- 确保你的 GitHub 账户已经登录，并且你有足够的权限来创建仓库和推送代码。
- 如果你使用 HTTPS URL，确保你已经创建了一个个人访问令牌并保存好。
- 如果你使用的是自定义域名，确保你的域名已经正确解析到 GitHub Pages 提供的服务。

按照这些步骤，你应该能够成功地使用 Hexo 和 GitHub Pages 搭建并部署你的博客。如果你需要更详细的指导或遇到问题，可以查看相关软件的官方文档或在社区论坛中寻求帮助。