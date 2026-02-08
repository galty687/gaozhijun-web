---
layout: post
title: Vercel Webhook
excerpt: "Vercel 通过Webhook连接 github仓库"
modified: 
tags: [部署]
comments: true
category: GenAI
---

1. 在Vercel中，添加Webhook，取一个名字以及指定Branch，会自动生成webhook URL
	 ![webhook](/assets/blog-images/202312/webhook.png)
	
2. 在 Github 仓库中，将	Webhook URL 填入

	![github-webhook](/assets/blog-images/202312/github-webhook.png)

3. 后续每次更新后，便可实现Vercel自动部署
