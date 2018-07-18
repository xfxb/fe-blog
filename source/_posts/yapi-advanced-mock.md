---
title: yapi 高级Mock功能资料整理
date: 2018-07-18 16:11:45
categories:
tags: yapi
author: maiyan
---

# Mock 优先级说明

请求 Mock 数据时，规则匹配优先级：`Mock 期望 > 自定义 Mock 脚本 > 普通 Mock`。

如果前面匹配到 Mock 数据，后面 Mock 则不返回。

# Mock 望期 

>“期望”意思是，当你输请求参数是这个的时候，我给你返回一个特殊的数据。例如，手机号11234567890是管理员账号，管理员返回数据要和普通成员不一样，这时候我们就可以使用期望来处理。

## 期望例子：

[https://yapi.blissmall.net/project/16/interface/api/1234](https://yapi.blissmall.net/project/16/interface/api/1234)

```js
// https://yapi.blissmall.net/mock/16/testExpectation?phoneNumber=11234567890
{
    "data": "管理员的手机号码"
}
```

```js
// https://yapi.blissmall.net/mock/16/testExpectation?phoneNumber=12577321332
{
    "data": "不是管理员的手机号码"
}
```

# Mock 脚本

>“脚本”则是可以自己写JavaScript逻辑，自己创造数据，想返回什么就是什么，可以说是数据伪造的终极解决方案。

## 全局变量

请求

* `header` 请求的 HTTP 头
* `params` 请求参数，包括 Body、Query 中所有参数
* `cookie` 请求带的 Cookies

响应

* `mockJson` 接口定义的响应数据 Mock 模板

* `resHeader` 响应的 HTTP 头

* `httpCode` 响应的 HTTP 状态码

* `delay` Mock 响应延时，单位为 ms

* `Random` Mock.Random 方法，详细使用方法请查看 [Wiki](https://github.com/nuysoft/Mock/wiki/Mock.Random)

## 脚本例子：

[https://yapi.blissmall.net/project/16/interface/api/1242](https://yapi.blissmall.net/project/16/interface/api/1242)

### 脚本

```js
// https://yapi.blissmall.net/mock/16/testScript?pageNum=2&pageSize=10

let data = {}
data.item = []
data.total = Random.integer(5, 30)

for (let i = 0; i < params.pageSize; i++ ){
    data.item.push({
        userId: Random.guid(),
        userName: Random.name(),
        mail: Random.email()
    })
}

const isSuccess = Random.boolean()

mockJson = {
    params: params,
    data,
    status: isSuccess ? "success" : "error",
    code: isSuccess ? 200 : Random.integer(100, 199),
    msg: isSuccess ? "处理成功!" : `处理失败！- ${Random.cparagraph(1)}`
}
```

### 返回结果

```json

{
    "data": {
        "item": [
            {
                "userId": "Ed2c33eE-CdDf-b831-EFFe-bD23F16145C9",
                "userName": "Linda Young",
                "mail": "u.oyt@isice.gm"
            },
            {
                "userId": "C76B8E71-eACD-EFBC-fcDb-eE41C99FDc48",
                "userName": "Barbara Hall",
                "mail": "o.wtkvkmfk@lfoigssk.org"
            },
            {
                "userId": "c379b82a-0AC3-F951-Fa18-383fAf4E49A8",
                "userName": "Jason Anderson",
                "mail": "k.ezvdwbcn@gvodhebxp.中国"
            },
            {
                "userId": "7e36645d-3fdB-15b8-B8A1-aA16bd549FDf",
                "userName": "Deborah Jackson",
                "mail": "j.rmvdar@fvjdkrzv.bj"
            },
            {
                "userId": "8fF85fE4-b7dD-73e2-cfD3-4388e6cDaaE5",
                "userName": "Eric Wilson",
                "mail": "f.qgsoayo@yqfnya.nr"
            },
            {
                "userId": "A3842e27-BDbc-1064-b8Ee-55B45dfdEE9b",
                "userName": "Cynthia Thompson",
                "mail": "d.djskvxw@vnvh.ao"
            },
            {
                "userId": "57D63E38-d5Db-dcD9-CEe7-baE1B3d3Ef5e",
                "userName": "Patricia Lee",
                "mail": "x.zbcepw@flzlfikp.travel"
            },
            {
                "userId": "d858ecA5-B6F2-8Dd5-C79E-Bef6537CA2e9",
                "userName": "Michael Robinson",
                "mail": "v.wmpy@urejya.mm"
            },
            {
                "userId": "9B41DE77-BB5B-A7D8-fbd6-AB14CC4CADff",
                "userName": "Christopher Perez",
                "mail": "r.cnclg@ekov.cc"
            },
            {
                "userId": "1184E21A-Bb8B-7027-Af86-1d3d58F81B8B",
                "userName": "John Martinez",
                "mail": "w.nvph@ujbinowj.mh"
            }
        ],
        "total": 28
    },
    "status": "error",
    "code": 117,
    "msg": "处理失败！- 开当天好查证布说况边将也形。"
}
```

# 参考

[高级Mock](https://yapi.ymfe.org/documents/adv_mock.html#mock-%E6%9C%9F%E6%9C%9B)

[在同事的安利下，试用了下接口管理平台YApi](https://www.zhangxinxu.com/wordpress/2018/05/introduce-yapi-api/)