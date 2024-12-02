---
date: 2024-11-26
tags:
  - comfyui
title: comfyui官方桌面版V1尝鲜
slug: comfyui-desktop
share: true
canonicalURL: 
keywords: 
description: 
series:
  - comfyui
  - Tools
lastmod: 
lang: cn
Cover:
  image: /images/comfyui-desktop-20241126170651399.webp
author: hellloveyy
---
## 客户端

今天收到了 comfyui 桌面版的下载邮件了，突然发现人家开源了。

GitHub 地址： https://github.com/Comfy-Org/desktop
官方指南： https://comfyorg.notion.site/ComfyUI-Desktop-User-Guide-1146d73d365080a49058e8d629772f0a
申请地址： https://www.comfy.org/waitlist

{{< figure src="/images/screenshot-20241126-164341.webp" caption="">}}


实际界面体验如下:

 {{< figure src="/images/screenshot-20241126-160323.webp" caption="">}}

{{< figure src="/images/screenshot-20241126-160332.png" caption="">}}

{{< figure src="/images/screenshot-20241126-160346.webp" caption="">}}

- 自行下载依赖以及包
{{< figure src="/images/screenshot-20241126-160440.png" caption="">}}

- 默认文生图工作流
{{< figure src="/images/screenshot-20241126-163358.webp" caption="">}}

- 文件夹内容
{{< figure src="/images/comfyui-desktop-20241126171721972.webp" caption="">}}

> 附带一下最近学习的一点小笔记（持续更新）
> 
> 比较好的自学网站： https://www.comflowy.com/zh-CN/docs 
> 
> 比较好的课程可以去 B 站搜小王子

## 云安装

下载comfyui

```
!git clone https://github.com/comfyanonymous/ComfyUI.git
```

安装管理插件包

```
!cd ComfyUI/custom_nodes && git clone https://github.com/ltdrdata/ComfyUI-Manager.git
!cd ComfyUI/custom_nodes && git clone https://github.com/AIrjen/OneButtonPrompt.git
!cd ComfyUI/custom_nodes && git clone https://github.com/pythongosssss/ComfyUI-Custom-Scripts.git
```

下载扩散模型

```
!wget -P ./ComfyUI/models/checkpoints  https://pai-aigc-photog.oss-cn-hangzhou.aliyuncs.com/webui/ChilloutMix-ni-fp16.safetensors
!wget -P ./ComfyUI/models/vae  https://pai-aigc-photog.oss-cn-hangzhou.aliyuncs.com/webui/vae-ft-mse-840000-ema-pruned.ckpt
```

启动comfyui服务

```
!cd ./ComfyUI/ && python main.py
```

## 工作流

- 基础
{{< figure src="/images/comfyui-desktop-20241126173931407.webp" caption="">}}

- 最基础的文生图
{{< figure src="/images/comfyui-desktop-20241126174001685.webp" caption="">}}

{{< figure src="/images/comfyui-desktop-20241126174042920.webp" caption="">}}

## 实用Tip&工具

1. 操作按钮
	- 修改语言：ACLTranslation-langualge
	- 自动补全关键词：Text Autocomplete: enabled
2. ComfyUI-Detail-Daemon 可以大幅增加 FLUX 生成图像的细节。
3. 提示词自动化书写技巧
- 基础
	- 精准表达意图，长度最好保持在 75 个 token（或约 60 个字）以内
	- 越重要的词放在靠前的位置
	- 使用逗号分隔，输入 (keyword:weight) 方式来控制关键词的权重，比如 (hight building: 1.2 ) 就意味着 hight building 的权重变高

- 模板
	- Subject：因为主体是最重要的，所以主体一般会放在首位。
	- Environment：环境包含：
		- 主体周围的环境，比如说「在一片森林里」、「在一片草地上」等等。
		- 灯光，比如「闪电」、「月光」等等。
		- 天气，比如「下雨」、「下雪」等等。

	- Medium：媒介可以是图片的拍摄媒介，如「相机」，亦或者承载的媒介，比如「油画」。
	- Style：可以用 4W 记忆：
		- When：什么年代的风格？
		- Who：你想要谁的风格？（人或组织）
		- What：什么艺术类型的风格？或者艺术运动的风格？
		- Where：什么国家的风格？

- 图生文反推
- 自动写反推
- 节点预设
- SDXL风格预设

## 名词释义

1. CFGscale：关键词与图片的相关性，越高与关键词越贴切，建议3-9之间，使用模型建议即可
2. 采样器：Eular_ancestral 遇事不决就用;dpmpp_2m_sde 比较百搭
3. 调度器：normal，限行均速降噪；karras,刚开始降噪比较缓慢，中间增速，最后又缓慢；
4. 降噪：重绘幅度，文生图的时候默认保持1。
5. 默认负向关键词：embedding: easy negative

## 提示词书写方法与技巧

图生文提示词反推插件：WD14Tagger

反向提示词自动填写插件：one button prompt （auto negative）

自动风格化提示词：sdxl_prompt_styler

## 中文提示词书写

插件：AlekPet 包含6个节点

- Argos：纯本地翻译不需要网络
- google translate：需要网络+魔法（不好用）
- Clip 翻译高级：需要网络，可切换不同翻译API

{{< figure src="/images/comfyui-desktop-20241126174059936.webp" caption="">}}

## ComfyUI必备工作流和模型网站+如何解决图像颜色发灰问题

1. Http://openart.ai 
2. Http://liblib.ai 中国最大
	- 可以在线生图，但是所有的节点都是内置好的，不能自己添加
3. Http://civitai.com 全球最大最全
4. Http://comfy.icu 调用平台工作流直接生成，并可以直接在线调整


Ps: 
1. 各个模型最好做文件夹分类，文件夹名称使用英文
2. Checkpoint 高级（pysss）, 可以直接展示文件夹，模型信息和预览图
3. 如果图像发灰需要单独加载一个 vae 模型，不过目前最新的模型基本上都自带 vae 解码

## 图生图基础工作流搭建+人物转绘+Controlnet 线稿应用

### 简单转绘
1. 使用节点：**加载图像->vae 编码->复制 latent 批次**->K 采样器
	{{< figure src="/images/comfyui-desktop-20241127144531887.webp" caption="">}}
2. 人物转绘：正向关键词填写人物特征
3. 降噪：控制重绘幅度，越高就跟原图越不像
4. 改变图像大小：加载图像->**图像缩放节点**->vae 编码->复制 latent 批次->K 采样器
5. 图像对比：节点 **rgthree** ，放在 vae 解码之后，替换预览即可
6. 生成图之后播放声音：节点 **Custom Scripts**
### Controlnet
1. 大模型什么版本就选择什么版本的 controlnet
2. 使用节点：
	{{< figure src="/images/comfyui-desktop-20241127160237006.webp" caption="">}}


## 节点整合实现高效工作流
### 节点整合最简文生图

- Efficiency Node  

{{< figure src="/images/comfyui-desktop-20241128151014455.webp" caption="">}}

- Easy Use

{{< figure src="/images/comfyui-desktop-20241128153701644.webp" caption="">}}

- Segmentation 抠图和蒙版

{{< figure src="/images/comfyui-desktop-20241128162313285.webp" caption="">}}


## 实时渲染出图与 Turbo Lightning 和 LCM 模型讲解

Turbo 模型特点：仅需要 4-8 步

Lightning 参数：
- 尺寸由模型版本决定 SDXL 1024*1024
- 步数：4-8
- CFG：1-2
- 采样器调度器使用作者推荐

LCM 特点：Low Compute Model
- 对核心算法进行了深度优化的微调模型可以大幅度减少生成图的计算数量

实时渲染节点:（效果一般）
- Mixlab
{{< figure src="/images/comfyui-desktop-20241129172812967.webp" caption="">}}

## ComfyUI 加速出图（TensorRT）

