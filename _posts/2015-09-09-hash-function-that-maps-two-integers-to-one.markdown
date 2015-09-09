---
layout: post
title: "Hash function that maps two integers to one"
description: "Cantor pairing function"
date: "Wed Sep 09 17:02:14 +0300 2015"
---

> Given n points on a 2D plane, find the maximum number of points that lie on
> the same straight line.

[_LeetCode_](https://leetcode.com/problems/max-points-on-a-line/)

The first solution that comes to mind is to see if each point is on the line
formed by each pair of points. This has O(N^3) complexity.

Next you can do a radial line sweep from each point in O(N^2 * log n). Romanian
explanation on [Infoarena][0].

Finally, the best solution in O(N^2) is to count the slopes for each pair of
points.

```c++
int slope = (x0 - x1) / (y0 / y1)
```

However, that poses another problem: how do you compute the hash key for the
slopes? First, you have to simplify the fraction till the numerator and
denominator are relatively prime. My first idea was that the key should be a
string:

```
string key = string(x) + "/" + string(y)
```

But the interviewer I think will laugh at me. Also, keeping a double as the key
I think will make somebody throw me from the window of the office (and buildings
these days have lots of floors).

So, I need a bijective function between a pair of integers and an integer. If I
knew that numbers were no bigger then let's say 2^16, I could have used:

```c++
int key = a * 2<<16 + b;
```

But, LeetCode does not say anything about the bounds. However, I've found the
Cantor pairing function on the internet, which is cute and easy to remember:

```c++
int getCantor(int x, int y) {
    return (x + y) * (x + y + 1) / 2 + x;
}
```

Finally, there is an even better function on [StackOverflow][1] and [here][2] is
my code for the problem.

[0]: http://www.infoarena.ro/algoritmi-de-baleiere#baleiere_radiala
[1]: http://stackoverflow.com/questions/919612/mapping-two-integers-to-one-in-a-unique-and-deterministic-way
[2]: https://github.com/palcu/Algorithm-Contest-Sources/blob/master/LeetCode/max-points-on-a-line.cpp
