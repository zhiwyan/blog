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
};
```

### 通用数据结构

- 双向循环链表
```
typedef struct foo {
    ElemType data;
    struct foo *prev;
    struct foo *next;
} foo_t;
```

- uCore的双向链表结构定义
```
struct list_entry {
    struct list_entry *prev,*next;
};

typedef struct {
    list_entry_t free_list;
    unsigned int nr_free;
} free_area_t;

struct Page {
    atomic_t ref;
    .......
    list_entry_t page_link;
}
```

- 链表操作函数
```
    list_init(list_entry_t *elm)
    list_add_after和list_add_before
    list_del(list_entry_t *listelm)
```

- 访问链表节点所在的宿主数据结构
```
free_area_t free_data;
list_entry_t *le = &free_area.free_list;
while((le=list_next(le)) != &free_area.free_list) {
    struct Page *p = le2page(le, page_link);
    ......
}

#define le2page(le, member)  to_struct((le), struct Page, member)
#define to_struct(ptr, type, member)    ((type *)((char *)(ptr) - offsetof(type, member)))
#define offsetof(type, member)  ((size_t)(&((type *)0)->member))
```