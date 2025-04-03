---
date: 2025-03-20
tags:
  - 微信
title: 企微、个微机器人调研
slug: wechat-bot
share: true
canonicalURL: ""
keywords: 
description: ""
series:
  - Tools
  - 产品
lastmod: 
lang: cn
Cover:
  image: /images/post-20240111195047056.webp
author: hellloveyy
---

> 最近一段时间调研个微、企微机器人的结论，和一些结合微信比较好的项目
> 叠甲: 仅代表此时此刻 2025 年 3 月，调研不易，需要的盆友们各取所需吧。

## 开源项目 ：
1. Wechaty 大部分微信机器人项目的基石，很多开源项目都是来源于此，支持的协议也是最多的，目前试用了它的网页版，基本的收发消息是可以用的，但是限制 2017 年之前注册的个微。iPad付费版慎用，听说被腾讯告了。 https://wechaty.js.org

2. Wechat4u 支持个微，使用 Webhook 协议，github star 1.8 k https://github.com/nodeWechat/wechat4u ，大部分个人开发者使用的项目，包括 idoubi 开发的知了阅读（转发文章获取总结）

3. Gewechat 支持个微，免费版 pad 协议，github star 2.5 k https://github.com/Devo919/Gewechat ，根据当前项目延伸出 dify-on-wechat, coze-on-wechat 等，gewechat要求必须搭建服务到同省服务器或者电脑里方可正常使用

4. Chatgpt-on-wechat 使用公众号、企微自建应用、钉钉、飞书等接入通道，其他通道为历史产物已不维护。感觉基本已经废废了，在 ChatGPT 火起来的时候狂飙 35 k star https://github.com/zhayujie/chatgpt-on-wechat ，当时还是支持个微的，企微是单独收费。前两天部署试了一下，历史的 Webhook 协议通道登录就被踢下线了。不过感觉可以联系一下官方使用收费版的 Pad 协议，替你们问过了专业版 7980+托管费 5000/账号/年

5. Dify-on-wechat 支持个微，继承自 Chatgpt-on-wechat，支持 itchat 协议（已废弃）、Gewechat 协议，Github star 2 k https://github.com/hanfangyuan4396/dify-on-wechat.

6. Wechat-bot 基于wechaty 框架，支持企微和个微。建议使用 Pad 协议，Github star 8 k https://github.com/wangrongding/wechat-bot ，糅合了各种 LLM 服务（DeepSeek / ChatGPT / Kimi / 讯飞）

7. WeChatFerry 基于 PC 端 hook 技术，拦截微信请求，项目以及整个技术栈开源，GitHub star 5.7 k https://github.com/lich0821/WeChatFerry

8. Dify-Enterprise-WeChat-bot https://github.com/luolin-ai/Dify-Enterprise-WeChat-bot ,基于 windows 和指定企业微信版本，不过私人版本需要联系作者

9. LangBot GitHub star 9.8 k https://github.com/RockChinQ/LangBot ,支持的模型生态比较丰富，还支持 MCP。支持的 IM 平台比较多（包括企微和个微），一直处于更新状态，个微使用 GeweChat 协议。

## 收费项目 ：
- Workbot  https://github.com/xlrpa/WorkBot
- Worktool  https://github.com/gallonyin/worktool
安卓端 APP 需要自己提供一台手机（需可运行企微/微信，手机型号和系统版本不限，本软件兼容 99% 的安卓手机）。使用安卓系统的官方无障碍服务，并在此基础上自研自动化框架，无 hook 函数、无侵入、无破坏、无内存修改，与 PC 端 RPA 完全不同。这两家供应商对比下来 Workbot 相对靠谱并且支持公对公转账和发票。

- 集简云：托管账户数量决定了添加外部联系人账户的数量（1个托管账户主动加好友不超过20个/天），同时最大处理对话的数量 （建议1个托管账户同时处理对话在5个内，否则会比较慢）。1-9个，3000元/托管账户/年；10-49个托管账户 2500元/托管账户/年；50个以上 2000元/托管账户/年

- LinkAI：自研协议，Chatgpt-on-wechat 开发商, 专业版 7980+托管费 5000/账号/年


## 协议分类 ：
- 安卓无障碍+RPA
	项目：Workbot、Worktool
	封号风险：据称为 0，但是实际使用还是有一定封号概率
- Pad ：大部分都是收费的，目前只有 Gewechat 免费
- Pad Local：Pad 协议的升级版，单账号 200/月，1200/年
- Webhook：
	项目：wechat4u，itchat
- Windows：安装指定版本的微信客户端
	项目：WeChatFerry






