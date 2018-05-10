---
title: 动态 rem
date: 2018-05-10 23:21:24
---

## 什么是 rem

rem 代表根元素 `html` 的 font-size 大小。

## 添加 meta viewport

```javascript
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

## JS 动态调整 rem

```javascript
(function flexible(window, document) {
    var docEl = document.documentElement

    setRemUnit()
    setBodyFontSize()

    // reset rem unit on page resize
    window.addEventListener('resize', setRemUnit)
    window.addEventListener('pageshow', function (e) {
        if (e.persisted) {
            setRemUnit()
        }
    })

    // set 1rem = viewWidth / 10
    function setRemUnit () {
        var width = Math.min(docEl.clientWidth, 512)  // 最大 512 px
        var rem = width / 10
        docEl.style.fontSize = rem + 'px'
    }

    // adjust body font size
    function setBodyFontSize () {
        if (document.body) {
            document.body.style.fontSize = '12px'
        }
        else {
            document.addEventListener('DOMContentLoaded', setBodyFontSize)
        }
    }
})(window, document)
```

## 使用 node-sass 自动 px2rem

在 `.scss` 文件中添加
```
$designWidth : 750;  // 设计稿的宽度

@function px($px){
    @return $px / $designWidth * 10 + rem;
}
```