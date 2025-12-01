---
title: 撰写新文章
author: cotes
date: 2019-08-08 14:10:00 +0800
categories: [博客, 教程]
tags: [写作]
render_with_liquid: false
---

本教程将指导您如何在_Chirpy_模板中撰写文章，即使您之前使用过Jekyll也值得一读，因为许多功能需要设置特定变量。

## 命名和路径

创建一个名为`YYYY-MM-DD-TITLE.EXTENSION`{: .filepath}的新文件，并将其放在根目录的`_posts`{: .filepath}文件夹中。请注意，`EXTENSION`{: .filepath}必须是`md`{: .filepath}或`markdown`{: .filepath}之一。如果您想节省创建文件的时间，可以考虑使用[`Jekyll-Compose`](https://github.com/jekyll/jekyll-compose)插件来完成这项工作。

## 前置元数据

基本上，您需要在文章顶部填写如下所示的[前置元数据](https://jekyllrb.com/docs/front-matter/)（Front Matter）：

```yaml
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG]     # TAG names should always be lowercase
---
```

> 文章的_layout_已默认设置为`post`，因此无需在前置元数据块中添加_layout_变量。
{: .prompt-tip }

### 日期的时区

为了准确记录文章的发布日期，您不仅需要设置`_config.yml`{: .filepath}中的`timezone`，还需要在前置元数据块的`date`变量中提供文章的时区。格式：`+/-TTTT`，例如`+0800`。

### 分类和标签

每篇文章的`categories`最多可包含两个元素，而`tags`中的元素数量可以从零到无限。例如：

```yaml
---
categories: [Animal, Insect]
tags: [bee]
---
```

### 作者信息

文章的作者信息通常不需要在前置元数据中填写，默认情况下会从配置文件的`social.name`变量和`social.links`的第一个条目获取。但您也可以按如下方式覆盖它：

在`_data/authors.yml`中添加作者信息（如果您的网站没有这个文件，请放心创建一个）。

```yaml
<author_id>:
  name: <full name>
  twitter: <twitter_of_author>
  url: <homepage_of_author>
```
{: file="_data/authors.yml" }

然后使用`author`指定单个条目或使用`authors`指定多个条目：

```yaml
---
author: <author_id>                     # for single entry
# or
authors: [<author1_id>, <author2_id>]   # for multiple entries
---
```

需要说明的是，`author`键也可以标识多个条目。

> 从`_data/authors.yml`{: .filepath}文件读取作者信息的好处是页面将包含`twitter:creator`元标签，这丰富了[Twitter卡片](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started#card-and-content-attribution)并有利于SEO优化。
{: .prompt-info }

### 文章描述

默认情况下，文章的开头部分文字用于在首页的文章列表、_延伸阅读_部分以及RSS源的XML中显示。如果您不想显示自动生成的文章描述，可以使用前置元数据中的`description`字段进行自定义，如下所示：

```yaml
---
description: Short summary of the post.
---
```

此外，`description`文本也将显示在文章页面的标题下方。

## 目录

默认情况下，**目**录（Table of Contents，TOC）会显示在文章的右侧面板中。如果您想全局关闭它，请转到`_config.yml`{: .filepath}并将`toc`变量的值设置为`false`。如果您想关闭特定文章的目录，请在文章的[前置元数据](https://jekyllrb.com/docs/front-matter/)中添加以下内容：

```yaml
---
toc: false
---
```

## 评论

评论的全局开关由`_config.yml`{: .filepath}文件中的`comments.active`变量定义。为该变量选择评论系统后，所有文章都会启用评论功能。

如果您想关闭特定文章的评论，请在文章的**前置元数据**中添加以下内容：

```yaml
---
comments: false
---
```

## 媒体

在_Chirpy_中，我们将图像、音频和视频统称为媒体资源。

### URL前缀

有时我们需要为文章中的多个资源定义重复的URL前缀，这是一项枯燥的任务，您可以通过设置两个参数来避免。

- 如果您使用CDN托管媒体文件，可以在`_config.yml`{: .filepath}中指定`cdn`。网站头像和文章的媒体资源URL将以CDN域名作为前缀。

  ```yaml
  cdn: https://cdn.com
  ```
  {: file='_config.yml' .nolineno }

- 要指定当前文章/页面范围的资源路径前缀，请在文章的前置元数据中设置`media_subpath`：

  ```yaml
  ---
  media_subpath: /path/to/media/
  ---
  ```
  {: .nolineno }

选项`site.cdn`和`page.media_subpath`可以单独使用或组合使用，以灵活组合最终的资源URL：`[site.cdn/][page.media_subpath/]file.ext`

### 图片

#### 图片说明

在图片的下一行添加斜体文本，它将成为图片说明并显示在图片底部：

```markdown
![img-description](/path/to/image)
_Image Caption_
```
{: .nolineno}

#### 尺寸

为了防止图片加载时页面内容布局发生偏移，我们应该为每张图片设置宽度和高度。

```markdown
![Desktop View](/assets/img/sample/mockup.png){: width="700" height="400" }
```
{: .nolineno}

> 对于SVG，您至少需要指定其_width_，否则它将不会被渲染。
{: .prompt-info }

从_Chirpy v5.0.0_开始，`height`和`width`支持缩写（`height`→`h`，`width`→`w`）。以下示例与上面效果相同：

```markdown
![Desktop View](/assets/img/sample/mockup.png){: w="700" h="400" }
```
{: .nolineno}

#### 位置

默认情况下，图片是居中的，但您可以通过使用`normal`、`left`和`right`类之一来指定位置。

> 指定位置后，不应添加图片说明。
{: .prompt-warning }

- **Normal position**

  在以下示例中，图片将左对齐：

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .normal }
  ```
  {: .nolineno}

- **Float to the left**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .left }
  ```
  {: .nolineno}

- **Float to the right**

  ```markdown
  ![Desktop View](/assets/img/sample/mockup.png){: .right }
  ```
  {: .nolineno}

#### 暗黑/明亮模式

您可以让图片跟随暗黑/明亮模式的主题偏好。这需要您准备两张图片，一张用于暗黑模式，一张用于明亮模式，然后为它们分配特定的类（`dark`或`light`）：

```markdown
![Light mode only](/path/to/light-mode.png){: .light }
![Dark mode only](/path/to/dark-mode.png){: .dark }
```

#### 阴影

程序窗口的截图可以考虑显示阴影效果：

```markdown
![Desktop View](/assets/img/sample/mockup.png){: .shadow }
```
{: .nolineno}

#### 预览图片

如果您想在文章顶部添加图片，请提供一张分辨率为`1200 x 630`的图片。请注意，如果图片的宽高比不符合`1.91 : 1`，图片将被缩放和裁剪。

了解这些先决条件后，您可以开始设置图片的属性：

```yaml
---
image:
  path: /path/to/image
  alt: image alternative text
---
```

请注意，[`media_subpath`](#url前缀)也可以传递给预览图片，也就是说，当它已设置时，属性`path`只需要图片文件名。

对于简单使用，您也可以只使用`image`来定义路径。

```yml
---
image: /path/to/image
---
```

#### LQIP低质量图片占位符

对于预览图片：

```yaml
---
image:
  lqip: /path/to/lqip-file # or base64 URI
---
```

> 您可以在文章"[文本与排版](../text-and-typography/)"的预览图片中观察LQIP效果。

对于普通图片：

```markdown
![Image description](/path/to/image){: lqip="/path/to/lqip-file" }
```
{: .nolineno }

### 视频

#### 社交媒体平台

您可以使用以下语法嵌入来自社交媒体平台的视频：

```liquid
{% include embed/{Platform}.html id='{ID}' %}
```

其中`Platform`是平台名称的小写形式，`ID`是视频ID。

下表显示了如何从给定的视频URL中获取我们需要的两个参数，您还可以了解当前支持的视频平台。

| 视频URL                                                                                            | 平台       | ID             |
| -------------------------------------------------------------------------------------------------- | ---------- | :------------- |
| [https://www.**youtube**.com/watch?v=**H-B46URT4mg**](https://www.youtube.com/watch?v=H-B46URT4mg) | `youtube`  | `H-B46URT4mg`  |
| [https://www.**twitch**.tv/videos/**1634779211**](https://www.twitch.tv/videos/1634779211)         | `twitch`   | `1634779211`   |
| [https://www.**bilibili**.com/video/**BV1Q44y1B7Wf**](https://www.bilibili.com/video/BV1Q44y1B7Wf) | `bilibili` | `BV1Q44y1B7Wf` |

#### 视频文件

如果您想直接嵌入视频文件，请使用以下语法：

```liquid
{% include embed/video.html src='{URL}' %}
```

其中`URL`是视频文件的URL，例如`/path/to/sample/video.mp4`。

您还可以为嵌入的视频文件指定其他属性。以下是允许的属性完整列表。

- `poster='/path/to/poster.png'` — 视频加载时显示的海报图片
- `title='Text'` — 显示在视频下方的标题，样式与图片标题相同
- `autoplay=true` — 视频准备就绪后自动开始播放
- `loop=true` — 视频播放结束后自动重新开始播放
- `muted=true` — 初始状态下音频静音
- `types` — 指定用`|`分隔的其他视频格式扩展名。确保这些文件与您的主要视频文件位于同一目录中。

考虑使用上述所有属性的示例：

```liquid
{%
  include embed/video.html
  src='/path/to/video.mp4'
  types='ogg|mov'
  poster='poster.png'
  title='Demo video'
  autoplay=true
  loop=true
  muted=true
%}
```

### 音频

如果您想直接嵌入音频文件，请使用以下语法：

```liquid
{% include embed/audio.html src='{URL}' %}
```

其中`URL`是音频文件的URL，例如`/path/to/audio.mp3`。

您还可以为嵌入的音频文件指定其他属性。以下是允许的属性完整列表。

- `title='Text'` — 显示在音频下方的标题，样式与图片标题相同
- `types` — 指定用`|`分隔的其他音频格式扩展名。确保这些文件与您的主要音频文件位于同一目录中。

考虑使用上述所有属性的示例：

```liquid
{%
  include embed/audio.html
  src='/path/to/audio.mp3'
  types='ogg|wav|aac'
  title='Demo audio'
%}
```

## 置顶文章

您可以将一篇或多篇文章固定在首页顶部，固定的文章会根据发布日期按倒序排列。启用方式：

```yaml
---
pin: true
---
```

## 提示框

有几种类型的提示框：`tip`（提示）、`info`（信息）、`warning`（警告）和`danger`（危险）。它们可以通过向引用块添加`prompt-{type}`类来生成。例如，定义一个类型为`info`的提示框如下：

```md
> Example line for prompt.
{: .prompt-info }
```
{: .nolineno }

## 语法

### 行内代码

```md
`inline code part`
```
{: .nolineno }

### 文件路径高亮

```md
`/path/to/a/file.extend`{: .filepath}
```
{: .nolineno }

### 代码块

Markdown符号```` ``` ````可以轻松创建代码块，如下所示：

````md
```
This is a plaintext code snippet.
```
````

#### 指定语言

使用```` ```{language} ````可以获得带语法高亮的代码块：

````markdown
```yaml
key: value
```
````

> Jekyll标签`{% highlight %}`与本主题不兼容。
{: .prompt-danger }

#### 行号

默认情况下，除`plaintext`、`console`和`terminal`外的所有语言都会显示行号。当您想隐藏代码块的行号时，请向其添加类`nolineno`：

````markdown
```shell
echo 'No more line numbers!'
```
{: .nolineno }
````

#### 指定文件名

您可能已经注意到代码语言会显示在代码块的顶部。如果您想用文件名替换它，可以添加`file`属性来实现：

````markdown
```shell
# content
```
{: file="path/to/file" }
````

#### Liquid代码

如果您想显示**Liquid**代码片段，请用`{% raw %}`和`{% endraw %}`包围liquid代码：

````markdown
{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}
````

Or adding `render_with_liquid: false` (Requires Jekyll 4.0 or higher) to the post's YAML block.

## 数学公式

我们使用[**MathJax**][mathjax]来生成数学公式。出于网站性能考虑，数学功能默认不会加载，但可以通过以下方式启用：

[mathjax]: https://www.mathjax.org/

```yaml
---
math: true
---
```

启用数学功能后，您可以使用以下语法添加数学公式：

- **块级数学公式**应使用`$$ math $$`添加，`$$`前后**必须**有空行
  - **插入公式编号**应使用`$$\begin{equation} math \end{equation}$$`添加
  - **引用公式编号**应在公式块中使用`\label{eq:label_name}`并在行内文本中使用`\eqref{eq:label_name}`（见下面的示例）
- **行内数学公式**（在行中）应使用`$$ math $$`添加，`$$`前后无需空行
- **行内数学公式**（在列表中）应使用`\$$ math $$`添加

```markdown
<!-- Block math, keep all blank lines -->

$$
LaTeX_math_expression
$$

<!-- Equation numbering, keep all blank lines  -->

$$
\begin{equation}
  LaTeX_math_expression
  \label{eq:label_name}
\end{equation}
$$

Can be referenced as \eqref{eq:label_name}.

<!-- Inline math in lines, NO blank lines -->

"Lorem ipsum dolor sit amet, $$ LaTeX_math_expression $$ consectetur adipiscing elit."

<!-- Inline math in lists, escape the first `$` -->

1. \$$ LaTeX_math_expression $$
2. \$$ LaTeX_math_expression $$
3. \$$ LaTeX_math_expression $$
```

> 从`v7.0.0`版本开始，**MathJax**的配置选项已移至`assets/js/data/mathjax.js`{: .filepath}文件，您可以根据需要更改选项，例如添加[扩展][mathjax-exts]。  
> 如果您通过`chirpy-starter`构建网站，请将该文件从gem安装目录（使用命令`bundle info --path jekyll-theme-chirpy`检查）复制到您仓库中的相同目录。
{: .prompt-tip }

[mathjax-exts]: https://docs.mathjax.org/en/latest/input/tex/extensions/index.html

## Mermaid图表

[**Mermaid**](https://github.com/mermaid-js/mermaid)是一个优秀的图表生成工具。要在您的文章中启用它，请在YAML块中添加以下内容：

```yaml
---
mermaid: true
---
```

然后您可以像使用其他Markdown语言一样使用它：将图表代码用```` ```mermaid ````和```` ``` ````包围起来。

## 了解更多

有关Jekyll文章的更多知识，请访问[Jekyll文档：文章](https://jekyllrb.com/docs/posts/)。
