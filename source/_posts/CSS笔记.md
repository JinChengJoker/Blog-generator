---
title: CSS 笔记
date: 2018-03-17 14:51:31
---

CSS(Cascading Style Sheets) 层叠样式表。

## CSS 主要版本

- CSS2
    1998年发布 CSS2，紧接着发布 CSS2.1，修复了 CSS2 中的一些错误，删除了一些不被支持的内容，增加了一些已有浏览器的拓展内容。

- CSS3
    2011年 CSS 被分为多个模块，并且每个模块单独升级，统称为 CSS3。例如： CSS 选择器 level3，CSS 媒体查询 level3，CSS color level3 等等。


## 常见引入 CSS 方式

- 内联 `style` 属性
    ```
    <div style="color: red;"></div>
    ```

- `style` 标签
    ```
    <style>
        div {
            color: red;
        }
    </style>
    ```

- 引入外部 `CSS` 文件
    ```
    <link rel="stylesheet" href="./css/style.css">
    ```

- 在 .css 文件中引入
    ```
    @import url('./style.css');
    ```


## 文档流

指文档内元素的流动方向。

- 内联元素
    默认从左往右流动，遇到阻碍（宽度不够）换行继续从左往右流动。
    不接受 width 和 height 这两个属性。

- 块级元素
    默认从上往下流动，每个元素各占一行。


## 一些技巧

- 解决元素 `float` 之后出现的问题
    在 float 元素的父元素添加 clearfix 类：
    ```
    .clearfix::after {
        content: "";
        display: block;
        clear: both;
    }
    ```

- 鼠标移入显示边框
    可以默认透明边框，写鼠标移入效果时再填充颜色。


## 注意细节

- 尽量不要使用 `width` 和 `height` 属性，否则不注意就会造成一些奇怪的问题（例如简历 demo 中导航和个人资料 `<hr>` 的问题）。

- 在编辑器中，两个 `span` 标签换行，在浏览器中渲染会有空格（因为两个标签之间会有换行符，不论有多少空格和换行符都只会渲染成一个空格）。

- 给元素添加 `display: inline-block;` 之后，有可能会出现一些奇怪的问题，可以尝试添加 `vertical-align: top;` 解决。