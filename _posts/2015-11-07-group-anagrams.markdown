---
layout: post
title: "Group Anagrams"
description: "unordered_map&lt;int, vector&lt;pair&lt;vector&lt;int&gt, vector&lt;string&gt;&gt;&gt;&gt; hash"
date: "Sat Nov 07 21:21:47 +0200 2015"
---

> Given an array of strings, group anagrams together.

[_LeetCode_](https://leetcode.com/problems/anagrams/)

Damn this is pretty hardcore to get in O(no\_anagrams * size\_alphabet).

```c++
class Solution {
    typedef vector<string> vs;
    const int MAX_ALPHABET = 26;
    const int MOD = 10007;
    vector<int> primes;
    
    void gen_primes() {
        primes.push_back(2);
        
        for (int i=3; primes.size() < 26; i+=2) {
            bool isPrime = true;
            for (int x : primes)
                if (i % x == 0) {
                    isPrime = false;
                    break;
                }
            if (isPrime)
                primes.push_back(i);
        }
    }
    
    int compute(vector<int>& v) {
        int ret = 1;
        for (int i=0; i<MAX_ALPHABET; i++) {
            for (int j=0; j<v[i]; j++)
                ret = (ret * primes[i]) % MOD;
        }
        return ret;
    }
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        gen_primes();
        
        unordered_map<int, vector<
            pair< vector<int>, vector<string> >
        >> hash;
        
        for (string s : strs) {
            vector<int> count(MAX_ALPHABET, 0);
            for (char c : s)
                count[c - 'a']++;
            int key = compute(count);
            
            bool inHash = false;
            for (int i=0; i<hash[key].size(); i++)
                if (hash[key][i].first == count) {
                    hash[key][i].second.push_back(s);
                    inHash = true;
                    break;
                }
            if (!inHash) {
                hash[key].push_back({count, {s}});
            }
        }
        
        vector<vs> ret;
        for (auto hashGroup : hash) {
            // hashGroup = {key, vector< pair<vector<int>, vector<string>> >}
            cout << hashGroup.second[0].second.size() << endl;
            for (auto anagramGroup: hashGroup.second) {
                // anagramGroup = pair<vector<int>, vector<string>>
                sort(anagramGroup.second.begin(), anagramGroup.second.end());
                ret.push_back(anagramGroup.second);
            }
        }
        
        return ret;
    }
};
```

And I still don't know why range based for loops [don't work](http://stackoverflow.com/questions/33586791/range-based-for-loop-in-c).
