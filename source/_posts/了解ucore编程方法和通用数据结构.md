---
title: 了解ucore编程方法和通用数据结构
date: 2021-04-06 20:12:50
tags:
---

## 了解ucore编程方法和通用数据结构


### 面向对象编程方法
- ucore主要基于C语言设计，采用了一定的面向对象编程方法。
```
/lab2/kern/mm/pmm.h
-------------------
struct pmm_manager {
    const char *name;
    void (*init)(void);

    void (*init_memmap)(struct Page *base, size_t n);

    struct Page *(*alloc_pages)(size_t n);
    void (*free_pages)(struct Page *base, size_t n);
    size_t (*nr_free_pages)(void);
    void (*check)(void);
}
```


### 通用数据结构