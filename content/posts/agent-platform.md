---
date: 2024-08-13
tags:
  - 产品
  - ToB
  - ToC
  - agent
title: AI瞎想碎片化思考系列之agent构建
slug: agent-platform
share: true
canonicalURL: ""
keywords: 
description: 
series:
  - 产品
  - agent
lastmod: 
lang: cn
Cover:
  image: /images/idea-20240813165816226.webp
author: hellloveyy
---

{{< figure src="/images/idea-20240813165816226.webp" caption="">}}

> 对目前市面上构建 agent 的平台和工具的一些思考

最近 Product Hunt 上大火的 Wordware，其目的是降低 agent 构建门槛，让创建 agent 像 notion 文档一样简单，不需要懂 workflow、不需要懂代码即可完成复杂的 agent 构建。

那先列举一下目前比较火的 agent 构建平台吧
- GPTs
- coze 以及类似大厂推出的平台（ModelScope，飞桨等）
- dify
- fastgpt
- glif 
- AutoGPT 最新版支持模块化设置
- Comfyui_LLM_party 以 comfyui 的形式构建类似 dify 的 agent 工作流
- ... 
是不是眼花缭乱，但是其实这些平台的目的也是为了降低构建 agent 的门槛，但是自从这些平台初始推出至现在，我就一直在想这类产品的构建者用户群体到底是谁呢？

是对 AI 有兴趣的普通人吗？
好像不是，因为对于这些人来说光是理解代码、工作流、记忆、变量等，这些概念就得好一阵子了

是专业的 LLM 研发工程师？
好像也不是，因为他们看不上这些玩意儿，太低级了😁

那究竟是谁呢？
我仔细想了想，代入了一下自己。好像更多的是我们这些 PM 渣渣，用来满足自己对于 AI 的一些探索乐趣，同时做一个 MVP。

最早的 agent 构建工具是 GPTs，通过自然语言描述来生成一个 agent 同时也带来了提示词工程的兴起。但是有一个弊端就是不可控，那时候即使在提示词中写好了 workflow 也有一大定的几率不按照规则去执行，尤其是较差的 LLM 那更是忽略你的 prompt 跟吃饭一样（比如那时候的文心一言 hhh）

最早在 dify 没有出来的时候我就在想，现在通过 langchain 构建 agent，对于小公司以及非 LLM 研发来说门槛过于高了，应该来做一款平台类的产品，让大家更专注于自己的思维，从而做出属于自己内心的 agent 产品。

后来 dify、fastGPT 来了，打着开源化 agent 部署平台的旗号，确实很好用解决了很大一部分小公司的需求，并且流程大部分可视化。

随着 coze 的大兴起（主要是那时候佛光普照 com 版本免费用 GPT4 接口呀），workflow 的设计也越来越严谨，加入了变量、记忆等等功能。可是我觉得并没有带来构建者用户群体的变化，反而门槛越来越高了😁

很早之前我就在想究竟这类产品的用户是谁？怎么才能让这类平台性质的产品更好用呢？能不能更 LUI？

年初的某一天，想到“每个人都能自由便捷的构建 agent 才是最好的 agent platform“，在开车突然灵感一飘而过，年龄大了记忆力不好赶紧记下来。

{{< figure src="/images/agent-platform-20240816153412887.webp" caption="">}}
（...忽略一些杂七杂八的玩意儿）

然后果然还是忘了，前两天看到 Wordware，突然想起来自己还留了一个代办呢😭

体验了一下 Wordware 感觉距离我脑海里的东西很近了，很 LUI。

抽时间想了想并且把我当前脑海里面最好的 agent 构建平台是什么样子大概画了一下图。


{{< figure src="/images/agent-platform-20240819163331370.webp" caption="">}}


- 为什么是流程图？
	- 首先你得清晰的知道自己要的是一个什么流程，才能把这个流程复现出来，即使只是一个粗略的流程图，也可以不断的根据你的思路去细化，把脑海之中要做的 agent 具象化出来。

- 技术难点
	- 平台前置不同的功能模块作为tools
	- 通过 LLM 准确判断涉及的功能模块


其实我们最终要做的 Agent 是把脑海里面的内容原封不动搬出来，不是吗？