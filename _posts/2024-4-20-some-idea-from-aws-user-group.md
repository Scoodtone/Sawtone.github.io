---
layout: post
title: AI | 生成式 AI —— Amazon User Group 北京站参会小记
categories: [AI, Life]
description: some-idea-from-aws-user-group
keywords: AI, Life, uncompleted
---


# 与三两好友一同参与 AWS User Group 线下活动，主题为生成式 AI，体验很棒

活动链接：https://mp.weixin.qq.com/s/R4IaPn6e0hBX7FBiL98fGA
活动图集：https://sawtone.github.io/fragment/figures-from-aws-user-group/

## 目录

见页面右侧

### 前言——我的 AI 经历

参加这次活动前我仔细回想，发现自己对于生成式 AI 涉猎较广，但了解极浅

于是顺便借此机会，回想与总结了自己这方面的经历与经验

主要但不限于：

**InternLM**：2023.10 - 2024.4

参与第一期实战营内测、公测，第二期实战营公测

探索与发布 windows 环境量化搭建 InternLM-7B 博客

阅读与修改部分模型代码，实现了 demo 中 streamlit 到 Flask 的转变

使用 nodejs 作为后端、reactjs 作为前端，调用大模型实现了一个全栈项目，后因技术不精搁浅



**Coze**： 2023.12 - 2024.2 

持续跟进 Coze 社区生态建设 

帮助 Coze's Discord 社群回答用户疑问

浅层使用 Coze Bot，初步了解 Prompt 与 Plugins 对于 Agent Bot 的重要之处

初步了解 WorkFlow、Knowledge Upload 等功能



**百度灵境矩阵 Agent** (现已更名为 文心 Agent)：2024.3

完成百度灵境开发营的低代码课程与配套实验，初步探索低代码 Agent 开发，取得证书



总结：探索经历虽丰富，但并无主要成果，对原理的了解也不深刻

正因如此，接下来四位大佬的分享令我受益匪浅，且做笔记，细细品味

### 《RAG 商业落地实践踩坑》From 高原

高原大佬分享的是大模型项目的商业落地实践

**关键词**：RAG、Agent、RolePlay、商业落地

佬由自己对接甲方的一次经历详细描述了大模型产品商业落地中的一些踩坑与解决办法

主要有以下几点：



|        踩坑         |                           详细描述                           |                         佬的解决办法                         |
| :-----------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   RAG无法有效检索   | 甲方提供了一系列产品与相关数据，呈现在表格里是一对多的关系，但 RAG 无法通过检索表格内产品数据从而根据对应关系找到产品 | 将产品的每个数据都转换为FAQ格式，通过设定问题的方式，将所有数据以问答形式传给大模型，大模型后续可通过embedding检测相似度并输出 |
|   甲方不满意效果    | 每次解决问题后，甲方会提出新的问题，如果不设立一种较为客观的评价标准，项目就很难真正落地 | 双方确认了一种评分方案，甲方设置10人左右的评价组，每次交付任务后对效果进行评分，取平均值后大于8分即视为项目成功完成，乙方记录评分变化趋势并做出针对性改进 |
| Embedding相似度不准 | 相似度检测太为死板，最想得到的答案可能并不是相似度最高的几项，这时若context 文本长度不足，就会丢失重要信息作为 prompt | 暴力解法：更换上下文长度更长的大模型，使得相似度不够的最优解也能被大模型读取；更好的方法：细化分类器、重写FAQ，增加匹配度，使得大模型使用 Embedding 检测相似度更为科学有效 |
|   大模型编造内容    | 大模型存在一定程度的幻觉，喜欢自己编造并不存在的内容以尽可能达成用户的需求，这在一些场景下是绝对不可以出现的 | 再次调用大模型检测输出，若大模型生成的内容经检测并不在知识库与白名单内，就由检测大模型进行打回并重新生成，让大模型自己为自己兜底 |
| 多次回复稳定性不好  | 乙方调试好大模型后发送给甲方，甲方测试人员在多次测试下仍然会测试出一些问题，大模型在多次测试在稳定性不好 | 用更长的测试时间确保更好的稳定性，对同一个问题用几十遍甚至上百遍的测试以确保大模型稳定性。测试没有捷径，如果硬要说有的话，那就是提前准备好测试工具与测试脚本 |

值得一提的是，在高佬分享的大模型项目落地实践中，大模型担任着多种角色：

它既可以作为**分类器**分类当前会话类型，也可以根据提供的历史记录和 prompt **重构问题**，可以根据分类结果和最终问题**生成答案**，更可以**检测回答**合理性、为自己兜底。

我认为多次调用大模型来处理不同的问题，最终达成目的，是大模型项目落地中不可或缺的部分。

回观我自己的项目，我便极其缺失多次调用大模型的能力。对于大模型代码了解的不够深入与项目经验的缺乏，导致我只能机械地使用相关回复函数，这是我需要认真反思与进步的地方，也是我最深的体会，感谢高佬。


### 《Foundation Models on Amazon Bedrock 初体验》From 沈鸿

沈鸿大佬分享的主要是 Claude 3 的构建与使用（基于 Amazon Bedrock）

**关键词**：Claude 3、Prompt Engineering、参数调整、Amazon Bedrock

受益匪浅，一定程度上帮助我对 ChatGPT 与 Claude 的输出进行对比，进一步提升效率。

### 《WhaleStudio 让大模型成为自己数据的百科全书》From 郭炜

郭炜大佬分享的主要是基于 WhaleStudio 生成企业数据百科全书

**关键词**：WhaleStudio、大模型、工作流、大数据、数据库

相关内容偏向企业级，不过还是认真聆听全程，感觉有一种大型 RAG + Agent 的感觉，很酷。


### 《如何安全高效地构建生成式 AI 应用》From 陈琪

陈琪大佬分享的是 Amazon Bedrock 的工作流程与生成式 AI 安全知识

**关键词**：Claude 3、Prompt Engineering、参数调整、Amazon Bedrock

陈佬分享的很多内容都很细节，图也干货满满，从多个维度讲述了生成式 AI 的安全问题，这块我听的还蛮仔细的，安全范围矩阵视角、安全威胁分布以及相关具体场景分析都令我受益匪浅，许多场景与图片我都予以留存在活动图集里，留待日后细细品味。

### 后记



