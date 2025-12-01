# Chirpy 启动器

[![Gem 版本](https://img.shields.io/gem/v/jekyll-theme-chirpy)][gem]&nbsp;
[![GitHub 许可证](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

通过 [RubyGems.org][gem] 安装 [**Chirpy**][chirpy] 主题时，Jekyll 只能从主题的 gem 中读取以下文件夹中的文件：
`_data`、`_layouts`、`_includes`、`_sass` 和 `assets`，以及 `_config.yml` 文件中的一小部分选项。如果您曾经安装过这个主题 gem，可以使用命令
`bundle info --path jekyll-theme-chirpy` 来定位这些文件。

Jekyll 团队表示这是为了让用户掌握更多控制权，但这也导致用户在使用功能丰富的主题时无法享受开箱即用的体验。

要充分使用 **Chirpy** 的所有功能，您需要将主题 gem 中的其他关键文件复制到您的 Jekyll 站点。以下是目标文件列表：

```shell
.
├── _config.yml
├── _plugins
├── _tabs
└── index.html
```

为了节省您的时间，并防止在复制过程中丢失文件，我们将最新版本的 **Chirpy** 主题的这些文件/配置以及 [CD][CD] 工作流程提取到这里，以便您可以在几分钟内开始写作。

## 使用方法

请查看 [主题文档](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)。

## 贡献

此仓库会随着主题仓库的新版本自动更新。如果您遇到任何问题或想为其改进做出贡献，请访问 [主题仓库][chirpy] 提供反馈。

## 许可证

本作品以 [MIT][mit] 许可证发布。

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/
[CD]: https://en.wikipedia.org/wiki/Continuous_deployment
[mit]: https://github.com/cotes2020/chirpy-starter/blob/master/LICENSE
