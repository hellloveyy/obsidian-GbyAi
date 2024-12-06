---
date: 2024-12-05
tags:
  - Claude
  - MCP
  - python
title: Claude MCP 小示例以及一些想法
slug: MCP-sqlite-example-and-fix-problem
share: true
canonicalURL: ""
keywords: 
description: ""
series:
  - Claude
  - Tools
lastmod: 
lang: cn
Cover:
  image: /images/MCP-sqlite-example-and-fix-problem-20241205144747998.webp
author: hellloveyy
---

{{< figure src="/images/MCP-sqlite-example-and-fix-problem-20241205144747998.webp" caption="">}}


> Anthropic 前两天发布了 MCP，很多人觉得和 FC、Plugins 是一个路数并不看好，持观望态度。我自己是参照官网整体走了一遍流程，说一下自己的看法，以及遇到的小坑。（小声蛐蛐官网居然不写这些小点）

## 个人看法

1. 不管成不成，先用你自己的 Claude 客户端，做一个提升你效率的工具体验一下才有资格去评论。即使不成，收益总是你自己的嘛
	- 可以在官网看十几个 case，并且 GitHub 开源的 MCP 应用已经不少了
	- https://github.com/modelcontextprotocol/servers
2. 如果 MCP 成了，就像是 VS Code 的 LSP 协议，借着开源的春风，那么这个玩意有可能会做出**个人 PC 的超级入口**。当然这就得看 mac 和 win 同不同意了，毕竟人家也想做嘛。但是你不动， anthropic 替你先发。😁
3. MCP 和 Plugins 很像，但是 Plugins 你需要去上传数据等到第三方平台，MCP 虽然也有泄漏的风险但是相对少一些，而且数据在本地，也省的我 ChatGPT 也传一份，coze 也传一份... 好多 agent 平台啊
4. MCP 和 FC 对比
	- 目的都是为了让大模型调用外挂能力，扩展更多的上下文，实现更多的能力，满足用户需求
	- 接入方式一个是在模型方写调用描述，一个在 MCP client 写描述，都是哪里用在哪里写，都是服务发现的那一套。不过 MCP 更规范扩展性更强，有更多的指导意义，但是其实从 agent 开始流行之后 GitHub 就有很多去中心化的协议了，只不过不是大厂发布核心影响力不够。
	- 难点都是模型的意图识别，用户 query 找到最匹配的能力（外挂），路由啊路由，难得都是在海量的质量参差不齐的应用里面找到最合适的一个。
	- 实现上孰优孰劣真不好说，但是个人使用方面觉得 MCP 更方便


## 实操原理

{{< figure src="/images/MCP-sqlite-example-and-fix-problem-20241205173542947.webp" caption="">}}

1. MCP Server 实现步骤：
    - 首先，通过详细描述 prompts、resources 和 tools，明确定义服务的具体能力；
    - 接着，使用 server.setRequestHandler 方法，精确配置接收到客户端请求后的处理逻辑和响应机制；
    - 最终，将 server 与 transport 建立连接，在本地环境中开启监听，等待处理客户端的 RPC 请求。
2. MCP 客户端接入流程：
    - 在客户端设计配置界面，允许用户预先录入并管理所需的 MCP Servers 信息；
    - 客户端启动时，连接 transport，通过 client.getServerCapabilities() 方法获取已配置 MCP Servers 的全部能力，包括 prompts、resources 和 tools 等详细信息；
    - 当用户在客户端提出问题时，将用户的询问与 MCP Servers 的能力描述一同提交给大模型，进行意图识别，由大模型判断需要调用的服务及其参数；
    - 客户端根据大模型的建议，携带特定的 MCP Server 名称和对应参数，发起 RPC 请求，获取服务响应的数据；
    - 最后，客户端将原始用户问题和 MCP Server 返回的数据一并提交给大模型，实现一次增强生成（可以理解为 RAG：Rpc-call-Augmented Generation）。
3. 文档教学
	- https://www.youtube.com/watch?v=EMfBscUM2v8&ab_channel=NiceKateAI
	- https://modelcontextprotocol.io/quickstart#installing-prerequisites-macos

## 一点小坑

> Could not attach to MCP server sqlite 怎么处理

1. 如果你发现你按照官方没有找到 `claude_desktop_config.json` 文件，请在 `claude -> setting -> Developer` 点击 edit config，或者在当前目录自行生成文件
{{< figure src="/images/MCP-sqlite-example-and-fix-problem-20241205170556225.webp" caption="">}}

2. 需要在上方操控栏找到 help 和 Developer 里面打开相应的权限，并且在添加过配置项之后，重启 Claude 客户端
{{< figure src="/images/MCP-sqlite-example-and-fix-problem-20241205170635423.webp" caption="">}}

3. 最后你的输入框旁边出现扳手图标 (🔧) 就代表 ok 了
{{< figure src="/images/MCP-sqlite-example-and-fix-problem-20241205170642302.webp" caption="">}} 

部分参考 issu： https://github.com/orgs/modelcontextprotocol/discussions/50