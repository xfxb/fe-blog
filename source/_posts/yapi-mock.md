---
title: yapi 关于mock功能的资料整理
date: 2018-07-17 11:30:21
categories:
tags: yapi
author: maiyan
---

# mock功能的两种方式

## 方式一：利用 jsopn5 + Mock.js

>原理：基于 Mockjs，跟 Mockjs 区别是 yapi 基于 json5 + 注释 定义 mock 数据，无法使用 Mock.js 原有的函数功能。

### JSON5

作用：是对 JSON 的一种推荐扩展，旨在使人类更易于手动编写和维护

JSON5 与 JSON 格式的区别

- key 只要是有效的标识符，则可以不加引号。即使是 ES5 中的保留关键字
- key-value 都可以使用单引号
- 对象和数组尾巴都可跟着逗号
- 字符串可以是多行的，只要加上反斜杠
- 数字可以是十六进制（基数为16）／以小数点开头或结尾／包括Infinity，-Infinity，NaN和-NaN／以明确的加号开始。
- **允许使用注释，单行多行都可以**

### Mock.js

作用：生成随机数据，拦截 Ajax 请求

#### Mock.js 的语法规范包括两部分：

1. 数据模板定义 [【使用文档】](https://github.com/nuysoft/Mock/wiki/Syntax-Specification#%E6%95%B0%E6%8D%AE%E6%A8%A1%E6%9D%BF%E5%AE%9A%E4%B9%89%E8%A7%84%E8%8C%83-dtd) [【全部示例】](http://mockjs.com/examples.html)

    数据模板中的每个属性由 3 部分构成：属性名、生成规则、属性值

    ``` js
    'name|rule': value

    // 属性名   name
    // 生成规则 rule
    // 属性值   value
    ```

    yapi官方例子：
    ```js
    {
        "name|regexp": "[a-z0-9_]+?",
        "type|regexp": "json|text|xml"
    }
    ```

2. 数据占位符定义  [【使用文档】](https://github.com/nuysoft/Mock/wiki/Syntax-Specification#%E6%95%B0%E6%8D%AE%E5%8D%A0%E4%BD%8D%E7%AC%A6%E5%AE%9A%E4%B9%89%E8%A7%84%E8%8C%83-dpd)  [【全部示例】](http://mockjs.com/examples.html#DPD)

    占位符 只是在属性值字符串中占个位置，并不出现在最终的属性值中。

    占位符 的格式为：

    ```js
    @占位符
    @占位符(参数 [, 参数])
    ```

    yapi官方例子：
    ```js
    {
        "errcode": 0,
        "errmsg": "@word",
        "data": {
        "id": "@id", //@id 随机生成 id
            "name": "@name" //@name 随机生成用户名
        }
    }
    ```

#### 支持替换请求的 query, body 参数

```js
{
  "name": "${query.name}", //请求的url是/path?name=xiaoming, 返回的name字段是xiaoming
  "type": "${body.type}",   //请求的requestBody type=1,返回的type字段是1
  
}

```

-------

## 方式二. json-schema

JSON Schema是基于JSON格式，用于定义JSON数据结构以及校验JSON数据内容。

>开启 json-schema 功能后，将不再使用 Mock.js 解析定义的返回数据，而是根据 json-schema 定义的数据结构，生成随机数据。

json-schema 参数比较多建议使用可视化工具入门
[【 json-schema-editor-visual 在线转换编辑器 】](http://yapi.demo.qunar.com/editor/)

### 常见 json-schema 关键字

| 关键字 | 描述 |
| :- | :- |
| $schema | 表示该JSON Schema文件遵循的规范 |
| title | 为该JSON Schema文件提供一个标题 |
| description | 关于该JSON Schema文件的描述信息 |
| type | 表示待校验元素的类型（例如，最外层的type表示待校验的是一个JSON对象，内层type分别表示待校验的元素类型为，整数，字符串，数字） |
| properties | 定义待校验的JSON对象中，各个key-value对中value的限制条件 |
| required | 定义待校验的JSON对象中，必须存在的key |
| minimum | 用于约束取值范围，表示取值范围应该大于或等于minimum |
| exclusiveMinimum | 如果minimum和exclusiveMinimum同时存在，且exclusiveMinimum的值为true，则表示取值范围只能大于minimum |
| maximum | 用于约束取值范围，表示取值范围应该小于或等于maximum |
| exclusiveMaximum | 如果maximum和exclusiveMaximum同时存在，且exclusiveMaximum的值为true，则表示取值范围只能小于maximum |
| multipleOf | 用于约束取值，表示取值必须能够被multipleOf所指定的值整除 |
| maxLength | 字符串类型数据的最大长度 |
| minLength | 字符串类型数据的最小长度 |
| pattern | 使用正则表达式约束字符串类型数据 |

# 参考资料

[yapi Mock介绍](https://yapi.ymfe.org/documents/mock.html)

[JSON5 更舒服的 JSON 格式](https://wxnacy.com/2018/02/18/json5/) 

[Mock.js](https://github.com/nuysoft/Mock/wiki) 

[JSON开发笔记（二）—— JSON Schema实战（上）](https://blog.csdn.net/qiumengchen12/article/details/72650291)
