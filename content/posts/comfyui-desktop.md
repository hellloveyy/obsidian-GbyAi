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

今天收到了 comfyui 桌面版的下载邮件了，有兴趣的可以联系我传给你。

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

附带一下最近学习的一点小笔记（持续更新）

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

1. 基础

![](https://cdn.nlark.com/yuque/0/2024/png/42422671/1730019022582-1979ee2a-7d21-4510-ba4a-4eb0a9e7a12a.png)

- 最基础的文生图

![](https://cdn.nlark.com/yuque/0/2024/png/42422671/1730019419071-5d99340e-352d-4588-a18a-3299826d1016.png)

![](https://cdn.nlark.com/yuque/0/2024/jpeg/42422671/1730018445555-b6ba6a67-f586-4b2f-af5b-5f30cb4b17ba.jpeg)

## 实用Tip&工具

1. 操作按钮

1. 修改语言：ACLTranslation-langualge
2. 自动补全关键词：Text Autocomplete: enabled

2. ComfyUI-Detail-Daemon 可以大幅增加 FLUX 生成图像的细节。
3. 提示词自动化书写技巧

1. 基础

1. 精准表达意图，长度最好保持在 75 个 token（或约 60 个字）以内
2. 越重要的词放在靠前的位置
3. 使用逗号分隔，输入 (keyword:weight) 方式来控制关键词的权重，比如 (hight building: 1.2 ) 就意味着 hight building 的权重变高

2. 模板

1. Subject：因为主体是最重要的，所以主体一般会放在首位。
2. Environment：环境包含：

- 主体周围的环境，比如说「在一片森林里」、「在一片草地上」等等。
- 灯光，比如「闪电」、「月光」等等。
- 天气，比如「下雨」、「下雪」等等。

3. Medium：媒介可以是图片的拍摄媒介，如「相机」，亦或者承载的媒介，比如「油画」。
4. Style：可以用 4W 记忆：

- When：什么年代的风格？
- Who：你想要谁的风格？（人或组织）
- What：什么艺术类型的风格？或者艺术运动的风格？
- Where：什么国家的风格？

3. 图生文反推
4. 自动写反推
5. 节点预设
6. SDXL风格预设

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

![](https://cdn.nlark.com/yuque/0/2024/png/42422671/1732511488437-3f1003a7-e472-4961-988c-a4e31bba9886.png)

## ComfyUI必备工作流和模型网站+如何解决图像颜色发灰问题