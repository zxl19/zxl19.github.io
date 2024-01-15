---
layout: post
title: Markdown学习笔记
date: 2020-05-13
author: zxl19
tags: [Markdown, Note]
comments: true
toc: true
pinned: false
---

我的Markdown学习笔记，部分语法在网页显示中无法正常识别，但是在编辑器中均显示无误。

<!-- more -->

## Markdown Hello World

1. Markdown是标记语言（markup language）的一种，标记语言是指一种文本编码系统（text-encoding system），它由插入文本文档中的一组符号组成，以控制其结构、格式或各部分之间的关系；
2. 常用的标记语言除了Markdown，还有AsciiDoc、reStructuredText、Typst等；

## 标题

### 使用`=`和`-`标记一级和二级标题

```markdown
一级标题
======

二级标题
------
```

### 使用`#`标记一级到六级标题

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

## 段落格式

### 段落

- 段内换行：两个以上空格加回车；
- 新建段落：一个空行；

### 字体

```markdown
*斜体*
_斜体_
**加粗**
__加粗__
***加粗斜体***
___加粗斜体___
```

### 分隔线

在一行中用三个以上的`*`或`-`或`_`来建立一个分隔线，之间可以插入空格。

### 删除线

```markdown
~~删除内容~~
```

### 下划线

```markdown
<u>下划线文本</u>
```

### 脚注

```markdown
正文内容[^1]。

[^1]: 脚注内容
```

## 列表

### 有序列表

```markdown
1. 第一点
2. 第二点
3. 第三点
```

### 无序列表

使用`*`、`+`、`-`作为列表标记：

```markdown
* 第一点
* 第二点
* 第三点
```

### 列表嵌套

```markdown
1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素
```

## 区块

使用`>`，可嵌套使用：

```markdown
> 最外层
> > 第一层嵌套
> > > 第二层嵌套
```

### 区块中使用列表

```markdown
> 1. 第一项
> 2. 第二项
> + 第一项
> + 第二项
> + 第三项
```

### 列表中使用区块

```markdown
* 第一项
    > 区块内容
    > 区块内容
* 第二项
```

## 代码

### 行内代码

使用反引号<kbd>`</kbd>（Tab键上方）。

### 代码区块

- 缩进四个空格<kbd>Tab</kbd>（Tab键）；
- 三个反引号<kbd>`</kbd>（可以指定代码语言从而高亮显示）；

### 语言支持

| 名称 | 关键字 |
| :--- | :--- |
| C/C++| c, cpp |
| LaTeX | latex |
| MATLAB | matlab |
| Mermaid | mermaid |
| Python | py, python |
| Shell | bash, shell |
| text | text, plain |

## 链接

### 普通链接

```markdown
[链接名称](链接地址)

<链接地址>
```

### 高级链接

```markdown
[链接名称][1]

[1]: 链接地址
```

## 图片

### 使用Markdown

```markdown
![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")
```

### 使用HTML

```html
<p align="对齐方式">
    <a href="超链接">
        <img src="图片地址" alt="属性文本" width="宽度" height="高度">
    </a>
</p>
```

1. 对齐方式：

    - `center`：居中；
    - `left`：左对齐；
    - `right`：右对齐；

2. 宽度和高度单位为像素或百分比；

## 表格

### 基础用法

1. 使用<kbd>|</kbd>来分隔不同的单元格；
2. 使用<kbd>-</kbd>来分隔表头和其他行；

示例：

```markdown
| 表头 | 表头 |
| ---- | ---- |
| 单元格 | 单元格 |
| 单元格 | 单元格 |
```

### 对齐方式

- `----:`：设置内容和标题栏居右对齐；
- `:----`：设置内容和标题栏居左对齐；
- `:---:`：设置内容和标题栏居中对齐；

## 高级技巧

### 任务列表

Markdown支持带有复选框（checkbox）的任务列表：

```markdown
- [ ] 不勾选，未完成的任务
- [x] 勾选，已完成的任务
```

### 折叠内容

Markdown支持通过点击交互的折叠内容：

```html
<details>
    <summary> 标题 </summary>
    被折叠的内容
</details>
```

### 支持HTML元素

1. 不在Markdown涵盖范围之内的标签，都可以直接在文档里面用HTML撰写；
2. 目前支持的HTML元素有：`<kbd>`、`<b>`、`<i>`、`<em>`、`<sup>`、`<sub>`、`<br>`等；

### 转义字符

Markdown支持在以下符号前加上反斜杠`\`来插入普通符号：

```markdown
\   反斜线
`   反引号
*   星号
_   下划线
{}  花括号
[]  方括号
()  小括号
#   井字号
+   加号
-   减号
.   英文句点
!   感叹号
```

### 公式

1. **行内公式**：使用两个美元符号`$$`括起来；
2. **行间公式**：使用一个美元符号`$`括起来；

### 绘图

```text
可以，但没必要。
```

Markdown支持使用Mermaid语法进行绘图，但是已有较多交互式绘图工具能够完成类似的绘图任务，本文不再赘述。

## 教程

1. [Markdown教程-菜鸟教程](https://www.runoob.com/markdown/md-tutorial.html)
2. [Markdown官方教程](https://markdown.com.cn)
3. [Markdown Guide](https://www.markdownguide.org)
4. [一份Markdown学习笔记](https://keatonlao.gitee.io/a-study-note-for-markdown/)
5. [Markdown基本语法](http://younghz.github.io/Markdown/)
6. [Markdown Reference](https://support.typora.io/Markdown-Reference/)
7. [CommonMark Spec](https://spec.commonmark.org)

## 参考

1. [Markup language-Wikipedia](https://en.wikipedia.org/wiki/Markup_language)
2. [Plain text documentation in version control-the 3 best markup languages](https://www.augmentedmind.de/2020/12/06/plain-text-documentation-in-vcs/)
3. [如何看待typst?-HexUp的回答-知乎](https://www.zhihu.com/question/591143170/answer/2949290734)
4. [younghz/Markdown](https://github.com/younghz/Markdown)
5. [commonmark/commonmark-spec](https://github.com/commonmark/commonmark-spec)
6. [AsciiDoc](https://asciidoc.org)
7. [reStructuredText-SourceForge](https://docutils.sourceforge.io/rst.html)
8. [Introduction to reStructuredText-Write the Docs](https://www.writethedocs.org/guide/writing/reStructuredText/)
9. [reStructuredText-Sphinx documentation](https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html)
10. [Typst](https://typst.app)
11. [代码块-简书](https://www.jianshu.com/p/c2b75ff24c33)
12. [待办事项-简书](https://www.jianshu.com/p/0b257de21eb5)
13. [Markdown进阶技能：用代码画流程图（编程零基础也适用）-黄浮云的文章-知乎](https://zhuanlan.zhihu.com/p/69495726)
14. [Mermaid从入门到入土——Markdown进阶语法-陈修竹的文章-知乎](https://zhuanlan.zhihu.com/p/355997933)
15. [程序员画图-mermaid(流程图)-leancode的文章-知乎](https://zhuanlan.zhihu.com/p/440934038)
