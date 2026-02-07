---
layout: post
title: 配置 Claude Code 远程工作
excerpt: "远程 Vibe Coding 实录"
modified: 
tags: [LLM, Chatgpt]
comments: true
category: AIGC

---



随着使用Claude Code越来越多，经常需要在外的时候也要云监工Claude Code的干活，一番尝试终于实现了。



## 工具链

1. Tailscale （实现虚拟局域网）
2. Termius (SSH 登录)
3. Tmux (会话保持)



## 流程

### Tailscale

0. 在Mac和 iPhone 上分别下载对应客户端，分别登录。

1. 启动 Tailscale. 打开 Tailscale 应用，登录并确保连接状态为 "Connected"。记下 Mac 的 Tailscale IP（通常是 `100.x.x.x`）。
2. 在手机上登录后，即可自动连接上。

这个时候，电脑和手机无论在哪里，都是组成了虚拟局域网。





### Termius

0. 在Mac和 iPhone 上分别下载对应客户端，分别登录。
1. 在Mac上新增一个 host，Address 填写上方Tailscale分配的 100.x.x.x ip
2. Credentials 是 Mac 的电脑的用户名和密码

要确保Mac开启了允许SSH登录，如果没有开，可以运行下方命令开启

```
sudo systemsetup -setremotelogin on
```



![termius-iphone](/assets/blog-images/2026/termius-iphone.PNG)

### Tmux

tmux 是终端复用器，核心功能三个：
1. 会话持久化：关掉终端或断开 SSH，程序继续在后台运行。重新连接后可以恢复到离开时的状态。这就是你用手机远程操作 Claude Code 的关键。

2. 分屏：一个终端窗口里同时显示多个面板，比如左边写代码、右边看日志。

  ```
  Ctrl+B, %    # 左右分屏
  Ctrl+B, "    # 上下分屏
  Ctrl+B, 方向键  # 切换面板
  ```

  

3. 多窗口：类似浏览器标签页，可以在多个全屏终端之间切换。

  ```
  Ctrl+B, C    # 新建窗口
  Ctrl+B, N    # 下一个窗口
  Ctrl+B, P    # 上一个窗口
  ```

  



```
# 创建会话
tmux new -s claude 

# 运行 Claude Code
claude

# 按 Ctrl+B, D 断开（Claude Code 继续运行）


# 手机 SSH 连上后， 
# 接回去，继续用
tmux attach -t claude 


如果想重新创建，先删旧的：
tmux kill-session -t claude
tmux new -s claude

```



### 远程提醒

终端 bell 通知

Termius 支持终端 bell 声音提示。在 `~/.tmux.conf` 中添加：

```
set -g monitor-bell on
set -g bell-action any
```

当 Claude Code 等待确认时如果触发 bell，手机上 Termius 会有提醒。