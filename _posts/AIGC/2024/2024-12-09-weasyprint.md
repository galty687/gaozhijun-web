---
layout: post
title: Weasyprint定制PDF
excerpt: "使用CSS Page Media 输出PDF"
modified: 
tags: [LLM, Chatgpt]
comments: true
category: AIGC

---


CSS 支持Page Media之后，给定制PDF带来了无数的便利，尤其是对于技术写作人士来说。


## 安装



```bash
brew install weasyprint
```



但是运行后会遇到下方错误：



```bash
OSError: cannot load library 'gobject-2.0-0': dlopen(gobject-2.0-0, 0x0002): tried: 'gobject-2.0-0' (no such file), '/System/Volumes/Preboot/Cryptexes/OSgobject-2.0-0' (no such file), '/Users/zhijungao/ENTER/lib/python3.10/site-packages/../../gobject-2.0-0' (no such file), '/Users/zhijungao/ENTER/bin/../lib/gobject-2.0-0' (no such file), '/usr/lib/gobject-2.0-0' (no such file, not in dyld cache), 'gobject-2.0-0' (no such file), '/usr/local/lib/gobject-2.0-0' (no such file), '/usr/lib/gobject-2.0-0' (no such file, not in dyld cache).  Additionally, ctypes.util.find_library() did not manage to locate a library called 'gobject-2.0-0'
```



解决方法：

```bash

# 来源：https://github.com/Kozea/WeasyPrint/issues/1448
# The problem was that symlinks to the libraries were not created (can't say should it be done by homebrew or weasyprint when installation


sudo ln -s /opt/homebrew/opt/glib/lib/libgobject-2.0.0.dylib /usr/local/lib/gobject-2.0
sudo ln -s /opt/homebrew/opt/pango/lib/libpango-1.0.dylib /usr/local/lib/pango-1.0
sudo ln -s /opt/homebrew/opt/harfbuzz/lib/libharfbuzz.dylib /usr/local/lib/harfbuzz
sudo ln -s /opt/homebrew/opt/fontconfig/lib/libfontconfig.1.dylib /usr/local/lib/fontconfig-1
sudo ln -s /opt/homebrew/opt/pango/lib/libpangoft2-1.0.dylib /usr/local/lib/pangoft2-1.0



```



## 使用

在index中关联css后，可以用weasypritn直接发布

```bash
weasyprint index.html pku.pdf                  
```



## Weasyprint支持的发布

具体功能点可见：https://print-css.rocks/lessons

简要来说，在Laytout上只支持Flex，不支持grid，对于定制技术文档这类PDF的样式来说已经足够啦。



## 参考

1. [weasyprint github](https://github.com/Kozea/WeasyPrint/issues/1448)
2. [Print CSS Lessons](https://print-css.rocks/lessons)
