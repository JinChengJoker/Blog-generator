---
title: AJAX
date: 2018-07-05 01:46:17
---

全称 Async Javascript and XML。

## 使用 XMLHttpRequest

浏览器提供了一个 `XMLHttpRequest` 方法，可以通过 `new XMLHttpRequest()` 创建一个可以发起 HTTP 请求的对象。

```javascript
let request = new XMLHttpRequest()  // 创建 HTTP 请求对象
request.open('POST', '/xxx')  // 初始化请求，默认为异步
request.setRequestHeader('Content-Type', 'x-www-form-urlencoded')
request.send('这是要发送的数据')  // 发送请求
request.onreadystatechange = () = {
    if(request.readyState === 4) {  // 请求和响应已完毕
        if(request.status >= 200 && request.status < 300) {
            console.log('请求成功')
            console.log(request.getResponseHeader('Content-Type'))
            console.log(JSON.parse(request.responseText))
        } else if(request.status >= 400) {
            console.log('请求失败')
        }
    }
}
```

在 `request` 对象中：

- `setRequestHeader()` 可以设置 HTTP 请求头（即第二部分），但必须在 `open()` 和 `send()` 之间调用。
- `send()` 可以设置 HTTP 请求的 body（即第四部分）。
- `onreadystatechange` 可以监听 `readyState` 值的变化。
- `readyState` 表示请求的 5 种状态。
    - `0` 未打开。`open()` 方法还未被调用
    - `1` 未发送。`open()` 方法已经被调用
    - `2` 已获取响应头。`send()` 方法已经被调用，响应头和响应状态已经返回
    - `3` 正在下载响应体。响应体下载中，`responseText` 中已经获取了部分数据
    - `4` 请求完成。整个请求过程已经完毕
- `getResponseHeader()` 可以获取 HTTP 响应头。


## 同源策略

因为安全问题，浏览器规定：只有在 **协议、域名、端口号** 一模一样的情况下，才可以通过 **AJAX** 发送请求。

**那为什么 `form` 没有跨域问题？**

因为用 `form` 发请求会刷新或离开当前页面，且用 `form` 提交到另一个域名之后，原页面的脚本无法获取新页面中的内容。

所以浏览器认为这是安全的。

实际上用 `<a>`、`<img>`、`<link>`、`<script>` 这些标签都可以发起请求，且都没有同源策略的限制。

而 AJAX 是可以直接读取响应内容的，因此浏览器不允许这样做。


## CORS（跨域资源共享）

全称 Cross-Origin Resource Sharing

虽然浏览器制定了同源策源，但是我们可以通过 CORS 来突破它，即跨域。

在服务器的响应中添加：

```javascript
response.setHeader('Access-Control-Allow-Origin', 'http://xxx')
// 或者四海皆兄弟
response.setHeader('Access-Control-Allow-Origin', '*')
```