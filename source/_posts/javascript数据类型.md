---
title: JavaScript 数据类型
date: 2018-04-12 22:44:04
---

## 基本类型

六种基本类型：Number、String、Boolean、Symbol、null、undefined。

### Number

| 进制 | 说明 | 示例 |
| :-: | :-:| :-: |
| 十进制 | - | 123 |
| 十进制 | 浮点数 | 1.23 |
| 十进制 | 科学计数 | 1.23e2 = 123 |
| 二进制 | 以 0b 开头 | 0b11 |
| 八进制 | 以 0 开头 | 011 |
| 十六进制 | 以 0x 开头 | 0x11 |

### String

- 空字符串： `''`

- 非空字符串： `'abc'` `' '`

- 多行字符串：
    ```javascript
    // 无回车符
    var s = '123' + 
            '456'
    s.length  // 6

    // 无回车符
    var s = '123\
    456'
    s.length  // 6

    // 包含一个回车符
    var s = `123
    456`
    s.length  // 7
    ```

### Boolean

只有两个值：true 和 false

### null 和 undefined

- 如果一个变量没有赋值，那么它就是 undefined。

- 惯例 - 如果要声明一个对象，且暂时没有值，可以初始化为 null。

- 惯例 - 如果要声明一个非对象，且暂时没有值，可以初始化为 undefined。

## 复杂类型

只有一种复杂类型：Object。

对象又可以分为三种子类型：Object（狭义的对象）、Array、Function。

复杂类型由基本类型组成。

### Object（狭义的对象）

#### 键名

- object 的所有键名都是字符串，但有些情况可以省略引号。

- 如果键名是数值，会被自动转为字符串。
    ```
    var obj = {
        1: 'a',
        2: 'b'
    }
    // 等同于
    var obj = {
        '1': 'a',
        '2': 'b'
    }
    ```

- 如果键名不是数值，且没有加引号，则必须以标识符（变量名）的规定命名；如果加引号，则没有这样的限制。
    ```
    // 报错
    var obj = {
        1a: 'hello'
    }
    
    // 正确
    var obj = {
        '1a': 'hello',
        '2 b': 'world'
    }
    ```

#### 添加属性

- 用方括号运算符 `object['key']` 添加属性，键名必须加上引号，否则会被当做变量。如果键名是数值，可以不用加引号，会被自动转为字符串。
    ```
    var obj = {}
    obj[a] = 'hello'  // 报错
    obj['a'] = 'hello'  // 正确
    obj[1] = 'world'  // 正确
    obj['1'] = 'world'  // 正确
    obj[2b] = 'hi'  // 报错
    obj['2b'] = 'hi'  // 正确
    ```

- 用点运算符 `object.key` 添加属性，键名必须符合标识符（变量名）规定。
    ```
    var obj = {}
    obj.a = 'hello'  // 正确
    obj.1 = 'world'  // 报错
    obj.2b = 'hi'  // 报错
    ```

#### 读取属性

- 用方括号运算符 `object['key']` 取值，键名必须加上引号，否则会被当做变量。如果键名是数值，可以不用加引号，会被自动转为字符串。
    ```
    var obj = {
        a: 'hello',
        1: 'world',
        2b: 'hi'
    }
    obj['a']  // 'hello'
    obj[a]  // 报错，因为 a 被当成了变量，变量 a 不存在
    obj['1']  // 'world'
    obj[1]  // 'world'
    obj[2b]  // 报错
    obj['2b']  // 'hi'
    ```

- 如果键名符合标识符（变量名）规定时，可以用点运算符 `object.key` 取值。
    ```
    var obj = {
        a: 'hello',
        1: 'world',
        2b: 'hi'
    }
    obj.a  // 'hello'
    obj.1  // 报错
    obj.2b  // 报错
    ```

#### 其他操作

- `key in object` 用于判断一个属性是否存在于 object 中，如果存在就返回true，否则返回false。
    ```
    var obj = { p: 1 }
    'p' in obj // true
    ```

- `for...in` 用于遍历 object 的属性。
    ```
    var obj = { a: 1, b: 2, c: 3 }
    for(var key in obj) {
        console.log(key)
    }
    // 'a'
    // 'b'
    // 'c'
    for(var key in obj) {
        console.log(obj[key])  // 注意这里 typeof key 为 string
    }
    // 1
    // 2
    // 3
    ```

- `Object.keys()` 可以查看一个对象的所有属性。
    ```
    var obj = { a: 1, b: 2, c: 3 }
    Object.keys(obj)  // ['a', 'b', 'c']
    ```

- `delete obj.key` 用于删除 object 中的属性，删除成功后返回 true。
    ```
    var obj = { p: 1 }
    delete obj.p  // true
    obj.p  // undefined
    ```