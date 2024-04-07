---
layout: post
title: Coze 的免费GPT4
excerpt: "使用Coze免费使用GPT4"
modified: 
tags: [LLM, Chatgpt, Coze]
comments: true
category: AIGC

---



字节Coze的海外版可以免费用gpt4，于是想到肯定有人已经想到将其封装为API服务，一搜果然有了。记录一下配置的过程，还是比较复杂的。项目地址：[coze-discord-proxy](https://github.com/deanxv/coze-discord-proxy)



## 前提条件

1. 注册Discord账号
2. 注册号Coze账号
3. 注册Render服务器



## 具体步骤

### Discord的服务器和机器人

大体步骤可以看[这篇博文](https://appscross.com/2024/02/save-20-per-month-triple-jump-free-use-of-gpt4turbo/)。

> 监听消息的bot，再reset token之后，一定要把下方的权限中的三个权限开关打开，不然就会导致 ChatGPT Next 那里一直收到不到response，一直在那typing，最后说无反应。

Discord Developer的门户：[链接](https://discord.com/developers/applications)

### 部署 coze discord proxy

整体一键部署即可，没有账号的话，会提示新建账号。

新建的时候选：

1. web service
2. 输入官方github repo的地址

需要注意的是：

1. 用[Render](https://render.com)的服务器，Zeabur的免费版用不了；
2. 环境变量更新后，会重启服务
3. 能配置的环境变量非常多，可以仔细看文档。我这里打开了：
   1. `SWAGGER_ENABLE=1`，可以将coze的gpt4，用api来使用
   2. `CHANNEL_AUTO_DEL_TIME=0`，在频道中记录聊天内容。
   3. `PROXY_SECRET`，设置api的秘钥

生成的API文档为：https://coze-discord-proxy-g080.onrender.com/swagger/index.html



### 配置 Chatgpt Next

上方配置好后，如果要在Chatgpt Next中使用，需要：

1. 在环境变量中，指定`BASE_URL`为Render中生成的URL地址，本项目的地址为：https://coze-discord-proxy-g080.onrender.com
2. 在`OPENAI_API_KEY`输入上方`PROXY_SECRET`中设置的密码。



### 唤醒Render服务器

> Render服务器的free plan，如果30分钟没有输入就会转为睡眠状态，再次有输入的时候，大概需要50秒才能唤醒。如果要不自动休眠，要交钱。
>
> Vecel服务器在等候Render的response的时候，如果超过5秒就会返回`EDGE_FUNCTION_INVOCATION_TIMEOUT` 如果需要要增加等候市场，要交钱。



总之想白嫖不容易啊，不过还是找到了解决之策。



1. 注册[cron-job.org](https://cron-job.org/en/)
2. 在Cronjobs中，设置一个任务，每15分钟访问一次服务器地址：https://coze-discord-proxy-g080.onrender.com
3. 虽然每次访问都会有`404`错误，但是render也会判断为有人在使用的，就不会休眠了。

> "Cron"这个词来源于希腊词语 "chronos"（χρόνος），意为“时间”。在Unix和类Unix系统中，它作为一个用于定时任务调度的程序，反映了其核心功能——根据时间表自动执行任务。尽管"cron"听起来像是一个缩写，但实际上它更多的是从其代表的功能“基于时间的作业调度”中提取出来的名字，而不是一个由首字母组成的缩写形式。

 
