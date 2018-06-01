---
title: 小程序插件分析报告
date: 2018-06-01 14:49:35
categories:
tags: weixinxiaochengxu
author: smileBin-web
---
# 小程序插件学习报告
## 1、小程序插件的介绍 [插件介绍](https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/)

> 插件是对一组 js 接口或[自定义组件](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/)的封装，用于提供给第三方小程序调用。插件必须嵌入在其他小程序中才能被用户使用。
> 插件开发者可以像开发小程序一样编写一个插件并上传代码，在插件发布之后，其他小程序方可调用。小程序平台会托管插件代码，其他小程序调用时，上传的插件代码会随小程序一起下载运行。
> 相对于普通 js 文件或自定义组件，插件拥有更强的独立性，拥有独立的 API 接口、域名列表等，但同时会受到一些限制，如一些 API 无法调用或功能受限。API的限制请参考 [可用的API](https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/api-limit.html)

#### Tip: 

> 开发一个插件和开发小程序一样需要上传，审核，发布上线经历一个较为繁琐的周期，因此对于一些较为简单的功能js模块或是自定义组件不适合应用插件，并且插件会随小程序一起下载并没有缩减资源包的大小。

> 基于一个小程序的appId 只能开发一个小程序插件, 他要有自己独立的API接口 能够提供服务 不能作为demo提交审核和发布（比小程序的审核更加严格）。

> 使用他人的插件时 目前还查阅不到插件的使用文档 个人推测这个为插件市场铺路 往后可能要付费使用

#### 插件可以是:
> 提供查询快递信息的服务

>  提供查询天气的服务

>  提供打车（滴滴）的服务 - 可以使用滴滴提供的组件，直接嵌入自己的小程序，实现打车功能）

> 提供外卖（美团外卖）的服务 - 例如每个餐厅需要的小程序风格都不一样，但他都需要外卖功能，那这时就可以给餐厅都定制一个小程序，在外卖部分的功能可以直接使用美团外卖提供的外卖插件

>  提供征信服务 - 例如p2p小程序大部分要使用征信，如果有人提供一个征信服务的插件，那直接拿来使用，就减少了很大的开发量，没有插件之前，你要不然自己做，要不然你可以使用小程序webview功能打开征信网站（需要添加webview允许域名才行），但这样的体验远远没有小程序好和直接

## 2、小程序的兼容分析报告

> 插件的开发和使用自小程序基础库版本 1.9.6 开始支持 有关基础库的介绍请参考 [基础库](https://developers.weixin.qq.com/miniprogram/dev/framework/client-lib.html)

> 截止2018/5/30 17:47 可支持小程序插件的用户占比为 58.95% 这个比例会一直上升 希望我们发布上线的时候能够达到一个能接受的占比。

> 截止2018/6/1 16：41 可支持小程序插件的用户占比已达98.23%

## 3、小程序插件的接入（包括开发和使用）请参考 [插件接入指南](https://developers.weixin.qq.com/miniprogram/introduction/plugin.html#%E5%B0%8F%E7%A8%8B%E5%BA%8F%E6%8F%92%E4%BB%B6%E5%8A%9F%E8%83%BD%E4%BB%8B%E7%BB%8D)


## 4、插件的开发 请参考 [开发插件](https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/development.html)

## 5、插件的使用 请参考 [使用插件](https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/using.html)