---
layout: post
title:  "对这个博客的使用"
date:   2025-10-12 01:12:00 +0800
categories: jekyll
tags: jekyll markdown 
author: Haoyang Gao
mathjax: true
---

* content
{:toc}


## 模板



`filename: 2025-08-28-FileName.md`

```
---
layout: post
title:  "第一次写博客"
date:   2025-08-28 01:57:00 +0800
categories: Daily
tags: Daily 
author: PandHedge
mathjax: true
---
* content
{:toc}

## 计划

- [ ]  今日目标
- [ ]  今日目标


---

## 今日

-  <02:00> 
-  

---

## 三思与计划


---

```



## Write post 写帖子

##### 开头

You can write posts at folder `_posts`. At the beginning of the post, you should declare  layout、title、date、categories、tags、author(optional)  info、mathjax(optional，click [here](https://www.mathjax.org/) for more detail about `Mathjax`).
您可以在文件夹 `_posts` 写帖子。在帖子的开头，您应该声明布局、标题、日期、类别、标签、作者（可选）信息、mathjax（可选，单击[此处](https://www.mathjax.org/)了解有关 `Mathjax` 的更多详细信息）。

```
---
layout: post
title:  "对这个 jekyll 博客主题的改版和重构"
date:   2016-03-12 11:40:18 +0800
categories: jekyll
tags: jekyll 端口 markdown Foxit RubyGems HTML CSS
author: Haoyang Gao
mathjax: true
---
```

#####  摘要

These follow code is for making contents.
这些以下代码用于制作内容。

```
* content
{:toc}
```

​    

You can use 4 wraps as a excerpt separator. The words before separator as  excerpt show in the index page. When you enter the post page, you can  read full article.
您可以使用 4 个换行作为摘录分隔符。分隔符前的单词作为摘录显示在索引页面中。当您进入帖子页面时，您可以阅读全文。

The wraps config is in the file `_config.yml`, as follows:
wraps 配置位于文件 `_config.yml` 中，如下所示：

```
# excerpt
excerpt_separator: "\n\n\n\n"
```

##### 语法

You should use markdown syntax to write article, just like write readme in github.
你应该使用 markdown 语法来写文章，就像在 github 中写自述文件一样。

You can use 3 ``` to write code block.
您可以使用 3 ''' 来编写代码块。

更多可以查看 [jekyll官方教程](https://jekyllrb.com/docs/pages/)

##### 多页面与资源

如果您有很多页面，则可以将它们组织到子文件夹中。当您的站点构建时，用于对项目源中的页面进行分组的相同子文件夹将存在于该文件夹中。但是，当页面在前面设置*了不同的*永久链接时，子文件夹会相应更改。`_site``_site`

```
.
├── about.md          # => http://example.com/about.html
├── documentation     # folder containing pages
│   └── doc1.md       # => http://example.com/documentation/doc1.html
├── design            # folder containing pages
│   └── draft.md      # => http://example.com/design/draft.html
```

##### 更改输出 URL[永久链接](https://jekyllrb.com/docs/pages/#changing-the-output-url)

您可能希望源文件具有针对构建站点而更改的特定文件夹结构。使用[永久链接](https://jekyllrb.com/docs/permalinks/)，您可以完全控制输出 URL。

##### 引用图片

你可以按照以下方式操作：

1. **创建自定义图片目录**
   比如在仓库根目录新建 `images` 或 `pics` 等目录存放图片，例如：

   ```plaintext
   你的仓库/
   ├── _posts/
   ├── images/       # 自定义图片目录
   │   ├── pic1.jpg
   │   └── pic2.png
   └── index.md
   ```

2. **引用方式**
   在 Markdown 或 HTML 中通过相对路径引用：

   ```markdown
   <!-- 从 index.md 引用 images 目录下的图片 -->
   ![示例图片](images/pic1.jpg)
   
   <!-- 从 _posts/2023-01-01-post.md 引用 -->
   ![示例图片](../images/pic1.jpg)
   ```

3. **如果图片在其他分支**
   同样可以用 GitHub 原始文件 URL 引用，例如：

   ```markdown
   ![外部分支图片](https://raw.githubusercontent.com/你的用户名/仓库名/分支名/自定义目录/图片名.jpg)
   ```

核心原则是：路径要与你的实际目录结构对应，相对路径从当前文件位置出发，绝对路径从仓库根目录出发（以 `/` 开头）。

