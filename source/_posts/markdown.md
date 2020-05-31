---
title: MarkDown语法
date: 2020-05-31 
tags: MarkDown语法
---
Markdown 致力于使阅读和创作文档变得容易.Markdown 完全由标点符号组成, 这些标点经过仔细挑选以使他们看上去和表达的含义相同. 例如, 星号标记的单词就像 *强调*. 列表就像是列表. 如果你使用过 email 的话, 就连块引用都像引用的文本段落.

1. 特殊字符如`<`,`&`等会自动转义,这使得用 Markdown 来写 HTML 代码很容易
2.  #~6#表示一级到六级标题
3. 引用`>`
4. `*、-、+`无序列表，数字加句号有序列表，可以转义“.”来避免触发有序列表
5. 三个`*`或`-`及以上数量生成水平线
6. 两种链接形式：内联及引用
- 内联链接示例
    ```
    This is [an example](http://example.com/ "Title") inline link.
    ```
- 引用链接示例，链接定义的名称可以包含字母,数字,空格,和标点符号,但它们不是大小写敏感的. 
    ```
    This is [an example][id] reference-style link.
    [id]: http://example.com/  "Optional Title Here"
    ```
    *注意: Markdown.pl 1.0.1 有一个已知的问题就是不能用单引号来包围链接标题.
    （"Optional Title Here"： 为可选的链接标题）*

7. `*`与`_`作为强调标记，等同`<em>`标签包裹；`**`与`__`等同于`<strong>`标签包裹

    ```
    强调可以出现在单词中,例如

    un*frigging*believable
    ```
8. 插入图片两种方式：内联及引用
- 内联方式
    ```
    ![Alt text](/path/to/img.jpg "Optional title")
    ```

- 引用方式
    ```
    ![Alt text][id]
    [id]: url/to/image  "Optional title attribute"
    ```

    Markdown 没有语法指定图片尺寸; 如果需要指定图片尺寸, 可以使用 HTML `<img> `标签.


参考连接： [官网文档地址][docLink]

[docLink]: https://markdown-zh.readthedocs.io/en/latest/  'Markdown官网文档地址'


