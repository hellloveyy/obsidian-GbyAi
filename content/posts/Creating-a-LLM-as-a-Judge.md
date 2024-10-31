---
date: 2024-10-31
tags:
  - 大模型
  - 评分
  - 标准
title: Creating a LLM-as-a-Judge That Drives Business Results
slug: Creating-a-LLM-as-a-Judge
share: true
canonicalURL: ""
keywords: 
description: ""
series:
  - LLM
lastmod: 
lang: cn
Cover:
  image: /images/hamel-LLM-as-a-Judge-20241031195252427.webp
author: hellloveyy
---

{{< figure src="/images/hamel-LLM-as-a-Judge-20241031195252427.webp" caption="">}}
#### **简直说到我的心巴坎去了，从我做智能客服开始的时候就不止 N 次，要求团队增加一个专业的医美客服来全程跟！**

Hamel Husain 这篇内容真的很好，全是实践经验。

介绍如何帮助模型团队避免被各种指标淹没。 

据我观察他说的这些问题国内模型训练团队也都有：
- 创建大量难以管理的指标 
- 非常随意的评分标准 
- 忽视领域专家意见 
- 指标不能反映对用户或业务需求

**重要观点** 
- 真正的价值在于数据分析过程, 而不是评判器本身
- 简单的 Pass/Fail 比复杂评分系统更有效
- 过程是迭代的, 需要定期重复或在重大变更时执行
- 不能完全消除人工介入, 但可以减少所需工作量

**实施建议**
- 不要跳过数据检查步骤
- 让专家评审过程尽可能简单从简单开始, 需要时再增加复杂度
- 保持评判标准的一致性
- 关注业务目标而非技术指标

**常见误区**
- 过早使用复杂评分系统
- 忽视领域专家意见
- 过分依赖现成的评估框架
- 期望完全消除人工介入

{{< figure src="/images/未命名-20241031194707902.webp" caption="">}}

原文地址： https://hamel.dev/blog/posts/llm-judge/