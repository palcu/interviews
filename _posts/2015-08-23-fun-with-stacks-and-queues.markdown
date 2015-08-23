---
title:  "Fun with stacks and queues"
date:   2015-08-23 19:00:00
description: "Simulating one with another"
---

There are the 2 standard problems.

## Implement a queue using stacks

```c++
class Queue {
private:
    stack<int> s1, s2;

    void move_stack_elements(stack<int>& from, stack<int>& to) {
        while (!from.empty()) {
            to.push(from.top());
            from.pop();
        }
    }
public:
    void push(int x) {
        move_stack_elements(s1, s2);
        s1.push(x);
        move_stack_elements(s2, s1);
    }

    void pop(void) {
        s1.pop();
    }

    int peek(void) {
        return s1.top();
    }

    bool empty(void) {
        return s1.empty();
    }
};
```

## Implement a stack with queues

```c++
class Stack {
    queue<int> q1, q2;

    void moveBetweenQueues(queue<int>& from, queue<int>& to) {
        while (!from.empty()) {
            to.push(from.front());
            from.pop();
        }
    }

public:
    void push(int x) {
        moveBetweenQueues(q1, q2);
        q1.push(x);
        moveBetweenQueues(q2, q1);
    }

    void pop() {
        q1.pop();
    }

    int top() {
        return q1.front();
    }

    bool empty() {
        return q1.empty();
    }
};
```

The implementations are one mirroring the other. However, for the second problem
we observe that we can ditch the second queue and just reverse the first one
till our first element becomes the last.

```c++
class Stack {
    queue<int> q1;

    void reverseQueue() {
        for (int i=0; i<q1.size() - 1; i++) {
            q1.push(q1.front());
            q1.pop();
        }
    }

public:
    void push(int x) {
        q1.push(x);
        reverseQueue();
    }

    void pop() {
        q1.pop();
    }

    int top() {
        return q1.front();
    }

    bool empty() {
        return q1.empty();
    }
};
```

Also, keep in mind that the method for accessing an element from a stack is
`top`, and the one for the queue is `front`.

For documentation reference I usually use [devdocs.io](http://devdocs.io/).

![devdocs](/assets/images/devdocs.png)
