---
layout: post
title: "When should I use the new keyword in C++?"
description: "One of the questions that bugged me"
date: "Fri Nov 06 14:09:03 +0200 2015"
---

I started today solving some linked lists questions. After finishing some LeetCode problems, I went to HackerRank. I immediately stopped at [`Insert a node at the tail of a linked list`](https://www.hackerrank.com/challenges/insert-a-node-at-the-tail-of-a-linked-list) and spent one hour debugging why this does not work:

```cpp
Node* Insert(Node *head,int data)
{
    Node node;
    node.data = data;
    node.next = nullptr;

    if (head == nullptr) {
        return &node;
    }

    Node* p = head;
    while (p->next != nullptr)
        p = p->next;
    p->next = &node;
    return head;
}
```

I guess I didn't [RTFM](http://stackoverflow.com/questions/655065/when-should-i-use-the-new-keyword-in-c):

> Method 2 (not using new): Memory is no longer allocated when it goes out of scope. (i.e. you shouldn't return a pointer to an object on the stack)
