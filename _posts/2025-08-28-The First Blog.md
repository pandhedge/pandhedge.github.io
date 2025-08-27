---
layout: post
title:  "对这个 jekyll 的使用"
date:   2025-08-28 01:12:00 +0800
categories: jekyll
tags: jekyll markdown 
author: Haoyang Gao
mathjax: true
---

* content
{:toc}


## Write post 写帖子



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

​    

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

​    

You should use markdown syntax to write article, just like write readme in github.
你应该使用 markdown 语法来写文章，就像在 github 中写自述文件一样。

You can use 3 ``` to write code block.
您可以使用 3 ''' 来编写代码块。

更多可以查看 [jekyll官方教程](https://jekyllrb.com/docs/pages/)

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

## 目标

- 目标
- 目标


---

## 评论

```

