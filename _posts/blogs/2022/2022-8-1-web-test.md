---
layout: post
title: 网站压力测试
experpt: "使用LOCUST测试网站性能"
modified: 
tags: [thoughts, research]
comments: true
category: blog
---



自己的几个小型网站上线后，因为服务器性能较弱，也不知道很多人访问后，服务器会不会吃不消，于是 LOCUST做了一个简单的测试，记录如下。



## LOCUST 简介

Python开发的压力测试工具，可以定义用户行为，如登录、浏览等。



**安装**

```
pip3 install locust
```

**验证是否安装成功**

```
locust -V
locust 2.10.2
```



**写测试行为**

```python
from locust import HttpUser, task

class HelloWorldUser(HttpUser):
    @task
    def hello_world(self):
        self.client.get("/")
        self.client.get("/blogs")
        self.client.get("/resume")
        self.client.get("/blog/metaphor")
        self.client.get("/blog/CDP/")
```

**启动locust**

将上方文件保存为`locustfile.py`并存入`web-test`文件夹，在Terminal中浏览至该文件夹，并输入

```shell
locust
```



启动后，在浏览器中输入 `http://localhost:8089/`即可进入图形界面。



**开始测试**

![测试界面](/assets/blog-images/20220801/GUI.png)

**服务器结果**

服务器毫无波澜，响应速度也不错，比较放心了。

![服务器性能](/assets/blog-images/20220801/server-performance.png)

