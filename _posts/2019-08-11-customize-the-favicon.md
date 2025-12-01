---
title: 自定义网站图标
author: cotes
date: 2019-08-11 00:34:00 +0800
categories: [博客, 教程]
tags: [图标]
---

[**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/)的[网站图标(favicons)](https://www.favicon-generator.org/about/)存放在`assets/img/favicons/`{: .filepath}目录中。您可能希望用自己的图标替换它们。以下部分将指导您创建和替换默认的网站图标。

## 生成网站图标

准备一张尺寸为512x512或更大的方形图像（PNG、JPG或SVG格式），然后访问在线工具[**Real Favicon Generator**](https://realfavicongenerator.net/)并点击<kbd>Select your Favicon image</kbd>按钮上传您的图像文件。

下一步，网页将显示所有使用场景。您可以保留默认选项，滚动到页面底部，然后点击<kbd>Generate your Favicons and HTML code</kbd>按钮来生成网站图标。

## 下载并替换

下载生成的包，解压后从提取的文件中删除以下两个文件：

- `browserconfig.xml`{: .filepath}
- `site.webmanifest`{: .filepath}

然后将剩余的图像文件（`.PNG`{: .filepath}和`.ICO`{: .filepath}）复制到您Jekyll站点的`assets/img/favicons/`{: .filepath}目录中，覆盖原始文件。如果您的Jekyll站点还没有这个目录，只需创建一个即可。

以下表格将帮助您了解网站图标文件的变更：

| 文件                | 来自在线工具                      | 来自Chirpy  |
|---------------------|:---------------------------------:|:-----------:|
| `*.PNG`             | ✓                                 | ✗           |
| `*.ICO`             | ✓                                 | ✗           |

<!-- markdownlint-disable-next-line -->
>  ✓ 表示保留，✗ 表示删除。
{: .prompt-info }

下次构建站点时，网站图标将被替换为您自定义的版本。
