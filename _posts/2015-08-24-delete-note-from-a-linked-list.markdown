---
title:  "Delete node from a linked list"
date:   2015-08-24 08:00:00
description: "Simple problem?... always has a trick"
---

> Write a function to delete a node (except the tail) in a singly linked list,
> given only access to that node.

My first thought was:

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```

However, we can do this in a neatly way:

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        *node = *node->next;
    }
};
```
