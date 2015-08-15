---
title:  "Templates and tools"
date:   2015-08-15 15:10:00
description: "C++11, VIM, syntastic, singlecompile, cgdb"
---

We as programmers tend to focus a lot on our development environment, and I have
the same problem. My top repo on Github are my
[dotfiles](http://github.com/palcu/dotfiles) with my bootstrapping script
written in Ansible.

However, when you are preparing for interviews, you should keep technologies to 
the minimum. You might have to write your code in just a Google Docs document.
But still, you don't want to spend most of your time when you are training with
adding spaces for indentantion.

For the code structure I absolutely love the way LeetCode structures your code.

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

    }
};
```

This is the template you get for the [two sum][1] problem. It forces you to
think what methods are private or public. This is how I write all the problems
on my whiteboard. After that I open VIM, copy the code on my laptop, save the
file and let the [`syntastic`][2] plugin to check if I have any syntax errors.
I've [configured][3] it to use the C++11 standards. Finally, I copy paste the
code in LeetCode and submit the problem.

Best case scenario is that I get and accepted solution and turn the music louder
in my house. However, that happens seldom. My next step is to try and debug the
problem on paper, without any help from breakpoints or `printfs`. Usually, I
forget a case in my code and I'll add it on the spot.

Worst case scenario is when I don't have any idea why my solution fails. This is
the time when I add the headers and a `main` function, and start debugging with
prints.

```c++
#include <vector>
#include <utility>
#include <iostream>
using namespace std;

const int N = 10007;

class Solution {
    vector<pair<int, int>> hash[N];
    
    int search_for(int x) {
        int key = x % N;
        key = key > 0 ? key : -key;

        for (int i=0; i<hash[key].size(); i++) {
            if (hash[key][i].first == x)
                return hash[key][i].second;
        }
        return -1;
    }

    void insert_in_hash(int x, int pos) {
        int key = x % N;
        key = key > 0 ? key : -key;

        hash[key].push_back(make_pair(x, pos));
    }

public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (int i=0; i<nums.size(); i++) {
            int solution = search_for(target-nums[i]);
            if (solution >= 0) {
                vector<int> sol;
                if (i < solution)
                    sol = {i+1, solution+1};
                else
                    sol = {solution+1, i+1};
                return sol;
            } else insert_in_hash(nums[i], i);
        }
    }
};

int main() {
    vector<int> v = {-1,-2,-3,-4,-5};
    Solution sol;
    vector<int> x = sol.twoSum(v, -8);
    for(auto i : x)
        cout << i << endl;
    return 0;
}
```
[_two-sum.cpp_](https://github.com/palcu/Algorithm-Contest-Sources/blob/master/LeetCode/two-sum.cpp)

For compiling and running this faster, I use the [`SingleCompile`][5] plugin.
My [config][6] is that whenever I press `F9`, the file gets compiled with 
C++11 and I get to see the output of running it.

If my solution gets to complicated, my last tool I use is [`cgdb`][4]. It's an
improved version of `gdb` that shows me a split pane between my code and my
`gdb` output.

![cgdb](/assets/images/cgdb.png)

[1]: https://leetcode.com/problems/two-sum/
[2]: https://github.com/scrooloose/syntastic
[3]:
https://github.com/palcu/dotfiles/blob/7d5796369e78f3914ad0fcd2e50c201863f8bd38/home/.vimrc#L85-L88
[4]: https://cgdb.github.io
[5]: https://github.com/xuhdev/SingleCompile
[6]:
https://github.com/palcu/dotfiles/blob/7d5796369e78f3914ad0fcd2e50c201863f8bd38/home/.vimrc#L97-L99
