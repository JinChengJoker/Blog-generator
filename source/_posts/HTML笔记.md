---
title: HTML 笔记
date: 2018-03-08 21:18:03
---

HTML(HyperText Markup Language) 超文本标记语言。

## HTML 的一些版本

- HTML 4.01
    以前的版本，提供的标签很少。

- XHTML
    主要特征是所有标签需要闭合，例如 `<input type="text" />` 。

- HTML 5
    现在流行使用的版本，新增了很多标签，例如 `nav` `main` `footer` 等等。
    部分标签不需要闭合 `<input type="text">` ，同时兼容上面两个版本。

- HTML 5.1
    已经发布的版本，但并未广泛使用。


## 规范文档

- 由 W3C 制定规范文档
    W3C(World Wide Web Consortium) 万维网联盟是由 Sir Timothy John Berners-Lee（李爵士）于1994年10月创立。

- 根据浏览器总结文档
    W3C 根据浏览器的实际情况总结文档，不是凭空想象。

- MDN
    MDN Web Docs（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个网络技术开发文档的免费网站。


## DOCTYPE

在最顶部第一行用来声明文档类型，声明 HTML 5：
```
<!DOCTYPE html>
```
除了 HTML 5 的声明，其他的版本都很复杂难记。。例如声明 HTML 4.01：
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```


## 声明 charset

在 head 中用 mate 标签声明当前页面的 charset：
```
<!-- HTML 5 -->
<meta charset="utf-8">
```
```
<!-- 这种写法已过时 -->
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
```


## HTTP-Server 工具

可以安装一个小工具来快速搭建一个本地服务器：
```
$ npm install -g http-server
$ http-server    // 开启服务
$ http-server -c-1    // 开启服务且不要缓存
```


## noscript 标签

如果浏览器禁用/不支持 javascript，则会显示 noscript 标签里的内容：
```
<noscript>
    <a href="http://www.baidu.com">打开百度</a>
    <p>如果你禁用了 JavaScript，那么你就可以看到这段话。</p>
</noscript>
```


## iframe 标签

一般用于在页面中嵌套另一个页面：
```
<iframe name="xxx" src="http://baidu.com" frameborder="0"></frame>
```

- `frameborder` 属性
    设置嵌入页面的边框，默认值为1，设置为0则表示无边框。


## a 标签

- `download` 属性
    ```
    <a href="http://baidu.com" download="baidu">点击下载</a>
    ```
    表示浏览器应该下载 URL，而不是导航到 URL。如果该属性有值，那么它将在保存提示中用作预先填写的文件名。

- `javascript` 伪协议
    点击 `a` 标签可以执行 `alert('Hello!')`：
    ```
    <a href="javascript: alert('Hello!');">点击我</a>
    ```
    可以实现点击 `a` 标签不跳转：
    ```
    <a href="javascript:;">点击我</a>
    ```


## input 标签

```
<input type="text" name="username">
```

- `name` 属性
    用于 `form` 表单提交时获取该 `input` 的值，如果没有该属性，则获取不到值。


## label 标签

一般与 `input` 配合使用，实现点击 `label` 即选中 `input`：
```
<label for="name">用户名：</label>
<input id="name" type="text" name="username">
```

- `for` 属性
    属性值需要与 `input` 的 `id` 对应绑定

还有一种便捷写法不需要绑定 `id`：
```
<label>
用户名：<input type="text" name="username">
</label>
```

## table 标签

- `border` 属性
    用于设置 `table` 的边框，单位为 `px`。
    但 MDN 建议不要使用这个属性, 该属性已废弃，应该用 CSS 代替。

-  `colgroup` `col` 标签
    可以通过 `class` 和 `span` 来统一设置 `table` 列的样式，但只有少数属性有效：
    ```
    <style>
        .column1 {
            width: 100px;
            background-color: red;
        }
        column2-3 {
            width: 200px;
            background-color: pink;
        }
    </style>
    ```
    ```
    <table>
        <colgroup>
            <col class="column1">
            <col class="column2-3" span="2">
        </colgroup>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>金成</td>
                <td>男</td>
                <td>24</td>
            </tr>
            <tr>
                <td>XXX</td>
                <td>X</td>
                <td>xx</td>
            </tr>
        </tbody>
    </table>
    ```