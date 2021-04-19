---
title: x86 启动顺序
date: 2021-04-14 09:21:09
tags: 计算机
categories: 计算机
---

### x86启动顺序 - 第一条指令
- CS = F000H, EIP = 0000FFF0H
- 实地址是：  
    Base + EIP = FFFF0000H + 0000FFF0H = FFFFFFF0H  
    这是BIOS的EPROM（Erasable Programmable Read Only Memory）所在地
- 当CS被新值加载，则地址转换规则将开始起作用
- 通常第一条指令是一条长跳转指令(这样CS和EIP都会更新)到BIOS代码中执行