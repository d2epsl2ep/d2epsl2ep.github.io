---
title: 开始
description: >-
  在此综合概述中开始了解 Chirpy 基础知识。您将学习如何安装、配置和使用您的第一个基于 Chirpy 的网站，以及将其部署到 Web 服务器。
author: cotes
date: 2019-08-09 20:55:00 +0800
categories: [Blogging, Tutorial]
tags: [getting started]
pin: true
media_subpath: '/posts/20180809'
---

## 创建站点存储库

创建站点存储库时，根据需要有两个选项：

### 选项 1.使用启动器（推荐）

这种方法简化了升级，隔离了不必要的文件，非常适合想要专注于以最少配置编写的用户。

1. 登录到 GitHub 并导航到 [**starter**][starter].
2. 单击按钮 <kbd>Use this template</kbd> 然后选择 <kbd>Create a new repository</kbd>.
3. 将新存储库命名为 `<username>.github.io`， 替换 `username` 为您的小写 GitHub 用户名。

### 选项 2.分叉主题

这种方法方便修改功能或 UI 设计，但在升级过程中会带来挑战。因此，除非您熟悉 Jekyll 并计划大量修改此主题，否则不要尝试此作。

1. 登录到 GitHub。
2. [分叉主题存储库](https://github.com/cotes2020/jekyll-theme-chirpy/fork).
3. 将新存储库命名为 `<username>.github.io`， 替换 `username` 为您的小写 GitHub 用户名。

## 设置环境

创建存储库后，就可以设置开发环境了。有两种主要方法：

### 使用开发容器（推荐用于 Windows）

Dev Containers 使用 Docker 提供隔离的环境，防止与系统发生冲突并确保所有依赖项都在容器内进行管理。

**Steps**:

1. 安装 Docker：
   - 在 Windows/macOS 上，安装 [Docker Desktop][docker-desktop].
   - 在 Linux 上，安装 [Docker Engine][docker-engine].
2. 安装 [VS Code][vscode] 和 [Dev Containers extension][dev-containers].
3. 克隆存储库：
   - 对于 Docker 桌面：启动 VS Code 并在 [clone your repo in a container volume][dc-clone-in-vol].
   - 对于 Docker 引擎：在本地克隆存储库， 然后在 [open it in a container][dc-open-in-container] 打开它。
4. 等待开发容器设置完成。

### Setting up Natively (Recommended for Unix-like OS)

For Unix-like systems, you can set up the environment natively for optimal performance, though you can also use Dev Containers as an alternative.

**Steps**:

1. Follow the [Jekyll installation guide](https://jekyllrb.com/docs/installation/) to install Jekyll and ensure [Git](https://git-scm.com/) is installed.
2. Clone your repository to your local machine.
3. If you forked the theme, install [Node.js][nodejs] and run `bash tools/init.sh` in the root directory to initialize the repository.
4. Run command `bundle` in the root of your repository to install the dependencies.

## Usage

### Start the Jekyll Server

To run the site locally, use the following command:

```terminal
$ bundle exec jekyll s
```

> If you are using Dev Containers, you must run that command in the **VS Code** Terminal.
{: .prompt-info }

After a few seconds, the local server will be available at <http://127.0.0.1:4000>.

### Configuration

Update the variables in `_config.yml`{: .filepath} as needed. Some typical options include:

- `url`
- `avatar`
- `timezone`
- `lang`

### Social Contact Options

Social contact options are displayed at the bottom of the sidebar. You can enable or disable specific contacts in the `_data/contact.yml`{: .filepath} file.

### Customizing the Stylesheet

To customize the stylesheet, copy the theme's `assets/css/jekyll-theme-chirpy.scss`{: .filepath} file to the same path in your Jekyll site, and add your custom styles at the end of the file.

Starting with version `6.2.0`, if you want to overwrite the SASS variables defined in `_sass/addon/variables.scss`{: .filepath}, copy the main SASS file `_sass/main.scss`{: .filepath} to the `_sass`{: .filepath} directory in your site's source, then create a new file `_sass/variables-hook.scss`{: .filepath} and assign your new values there.

### Customizing Static Assets

Static assets configuration was introduced in version `5.1.0`. The CDN of the static assets is defined in `_data/origin/cors.yml`{: .filepath }. You can replace some of them based on the network conditions in the region where your website is published.

If you prefer to self-host the static assets, refer to the [_chirpy-static-assets_](https://github.com/cotes2020/chirpy-static-assets#readme) repository.

## Deployment

Before deploying, check the `_config.yml`{: .filepath} file and ensure the `url` is configured correctly. If you prefer a [**project site**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) and don't use a custom domain, or if you want to visit your website with a base URL on a web server other than **GitHub Pages**, remember to set the `baseurl` to your project name, starting with a slash, e.g., `/project-name`.

Now you can choose _ONE_ of the following methods to deploy your Jekyll site.

### Deploy Using Github Actions

Prepare the following:

- If you're on the GitHub Free plan, keep your site repository public.
- If you have committed `Gemfile.lock`{: .filepath} to the repository, and your local machine is not running Linux, update the platform list of the lock file:

  ```console
  $ bundle lock --add-platform x86_64-linux
  ```

Next, configure the _Pages_ service:

1. Go to your repository on GitHub. Select the _Settings_ tab, then click _Pages_ in the left navigation bar. In the **Source** section (under _Build and deployment_), select [**GitHub Actions**][pages-workflow-src] from the dropdown menu.  
   ![Build source](https://chirpy-img.netlify.app/posts/20180809/pages-source-light.png){: .light .border .normal w='375' h='140' }
   ![Build source](https://chirpy-img.netlify.app/posts/20180809/pages-source-dark.png){: .dark .normal w='375' h='140' }

2. Push any commits to GitHub to trigger the _Actions_ workflow. In the _Actions_ tab of your repository, you should see the workflow _Build and Deploy_ running. Once the build is complete and successful, the site will be deployed automatically.

You can now visit the URL provided by GitHub to access your site.

### Manual Build and Deployment

For self-hosted servers, you will need to build the site on your local machine and then upload the site files to the server.

Navigate to the root of the source project, and build your site with the following command:

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

Unless you specified the output path, the generated site files will be placed in the `_site`{: .filepath} folder of the project's root directory. Upload these files to your target server.

[nodejs]: https://nodejs.org/
[starter]: https://github.com/cotes2020/chirpy-starter
[pages-workflow-src]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow
[docker-desktop]: https://www.docker.com/products/docker-desktop/
[docker-engine]: https://docs.docker.com/engine/install/
[vscode]: https://code.visualstudio.com/
[dev-containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[dc-clone-in-vol]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume
[dc-open-in-container]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container
