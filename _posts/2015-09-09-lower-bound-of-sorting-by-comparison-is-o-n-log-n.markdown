---
layout: post
title: "Lower bound of sorting by comparison is O(n * log n)"
description: "An intuitive explanation from Skiena"
date: "Wed Sep 09 12:07:13 +0300 2015"
---

Found a really nice explanation on why there cannot be a sorting algorithm that
uses comparisons and can have a lower bound then O(n * log n).

> An *Ω(nlogn)* lower bound can be shown by observing that any sorting algorithm
> must behave differently during execution on each of the distinct *n!*
> permutations of *n* keys. The outcome of each pairwise comparison governs the
> run-time behavior of any comparison-based sorting algorithm. We can think of
> the set of all possible executions of such an algorithm as a tree with *n!*
> leaves. The minimum height tree corresponds to the fastest possible algorithm,
> and it happens that *lg(n!) = Θ(n log n)*.
