---
title: 实现一个简易版 jQuery API
date: 2018-05-03 21:01:56
---

> 假设基本需求如下：  
> 使用 `$('div').addClass('red')` 可以给所有 `div` 添加一个 `red` 类。  
> 使用 `$('div').setText('hello')` 可以将所有 `div` 的文本内容设置为 `hello`。

## 封装函数

根据需求分别封装出两个函数：

```javascript
function addClass(selector, className) {
    let nodes = document.querySelectorAll(selector)
    for(let i = 0; i < nodes.length; i++) {
        nodes[i].classList.add(className)
    }
}

function setText(selector, text) {
    let nodes = document.querySelectorAll(selector)
    for(let i = 0; i < nodes.length; i++) {
        nodes[i].textContent = text
    }
}
```

## 选择器前置

### 方法一：拓展 prototype

```javascript
NodeList.prototype.addClass = function(className) {
    for(let i = 0; i < this.length; i++) {
        this[i].classList.add(className)
    }
}
NodeList.prototype.setText = function(text) {
    for(let i = 0; i < this.length; i++) {
        this[i].textContent = text
    }
}
```

调用 API：

```javascript
let nodes = document.querySelectorAll('div')
nodes.addClass('red')
nodes.setText('hello')
```

### 方法二：新建构造函数

```javascript
window.jquery = function(selector) {
    let nodes = document.querySelectorAll(selector)
    nodes.addClass = function(className) {
        for(let i = 0; i < nodes.length; i++) {
            nodes[i].classList.add(className)
        }
    }
    nodes.setText = function(text) {
        for(let i = 0; i < nodes.length; i++) {
            nodes[i].textContent = text
        }
    }
    return nodes
}
```

调用 API：

```javascript
jquery('div').addClass('red')
jquery('div').setText('hello')
```

## alias

```javascript
window.$ = jquery
$('div').addClass('red')
$('div').setText('hello')
```