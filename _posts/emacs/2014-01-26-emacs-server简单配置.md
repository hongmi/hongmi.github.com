---
layout: post
title:  emacs server简单配置
category : emacs
tags : [emacs, server]
---
{% include JB/setup %}

常见到emacs server可以加速emacs，然今日终于一试。  
用起来是极为简单的  

   emacs --daemon

启动server，然后执行
  
    emacsclient filename

即可。编辑完了使用ctrl+x,#(server-edit)即可进行提交和关闭。
