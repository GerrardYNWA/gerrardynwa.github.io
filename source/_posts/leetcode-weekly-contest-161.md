title: LeetCode Weekly Contest 161
date: 2019-11-03 20:51:02
categories: Algorithm

tags: [leetcode]
---
　　LeetCode第161场周赛
<!-- more -->

## 1. [Minimum Swaps to Make Strings Equal](https://leetcode.com/contest/weekly-contest-161/problems/minimum-swaps-to-make-strings-equal)

```C++
class Solution {
public:
    int minimumSwap(string s1, string s2) {
        if (s1.length() != s2.length()) return -1;
        
        int difference_xy = 0;
        int difference_yx = 0;
        for (int i = 0; i < s1.length(); i++) {
            if (s1[i] != s2[i]) {
                if (s1[i] == 'x') difference_xy++;
                else difference_yx++;
            }
        }
        
        if ((difference_xy + difference_yx) & 1) {
            return -1;
        } else {
            return difference_xy / 2 + difference_yx / 2 + (difference_xy % 2) * 2;
        }
    }
};
```



## 2. [Count Number of Nice Subarrays](https://leetcode.com/contest/weekly-contest-161/problems/count-number-of-nice-subarrays)

```C++
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> sums(n + 1, 0);
        
        for (int i = 0;i < n; i++) {
            sums[i + 1] = sums[i];
            
            if (nums[i] & 1) sums[i + 1]++;
        }
        
        int ans = 0;
        for (int i = 0; i < n; i++) {
            auto p = equal_range(sums.begin(), sums.end(), sums[i] + k);
            ans += (p.second - p.first);
        }
        
        return ans;
    }
};
```



## 3. [Minimum Remove to Make Valid Parentheses](https://leetcode.com/contest/weekly-contest-161/problems/minimum-remove-to-make-valid-parentheses)

```C++
class Solution {
public:
    string minRemoveToMakeValid(string s) {
        int n = s.length();
        vector<bool> flags(n, true);
        stack<int> sk;
        for (int i = 0; i < n; i++) {
            if (s[i] == '(') sk.push(i);
            else if (s[i] == ')') sk.pop();
        }
        
        while (!sk.empty()) {
            int idx = sk.top();
            flags[idx] = false;
            sk.pop();
        }
        
        string result = "";
        for (int i = 0; i < n; i++) {
            if (flags[i]) result += s[i];
        }
        
        return result;
    }
};
```



## 4. [Check If It Is a Good Array](https://leetcode.com/contest/weekly-contest-161/problems/check-if-it-is-a-good-array)

```C++
class Solution {
public:
    bool isGoodArray(vector<int>& nums) {
        int n = nums.size();
        if (n == 1 && (nums[0] == -1 || nums[0] == 1)) return true;
        
        int divisor = nums[0];
        for (int i = 1; i < n; i++) {
            divisor = gcd(nums[i], divisor);
            if (divisor == 1) return true;
        }
        
        return false;
    }
    
    int gcd(int a, int b) {
        if (b == 0) return a;
        
        return a >= b ? gcd(b, a % b) : gcd(b, a);
    }
};
```