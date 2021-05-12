---
title: c函数调用的实现
date: 2021-05-12 21:27:58
tags:
---
## c函数的调用实现

### 其他需要注意的事项
- 参数（parameters）& 函数返回值（return values）可通过寄存器或位于内存中的栈来传递
- 不需要保存/恢复（save/restore）所有寄存器