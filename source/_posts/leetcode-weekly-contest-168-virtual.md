title: LeetCode Weekly Contest 168 (Virtual)
date: 2019-12-25 15:06:28
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第168场周赛（Virtual）

<!-- more -->

## 1. [Find Numbers with Even Number of Digits](https://leetcode.com/contest/weekly-contest-168/problems/find-numbers-with-even-number-of-digits/)

```C++
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int ans = 0;
        for (int num : nums) {
            int cnt = 0;
            while (num) {
                cnt++;
                num /= 10;
            }
            
            if (!(cnt & 1)) ans++;
        }
        
        return ans;
    }
};
```

## 2. [Divide Array in Sets of K Consecutive Numbers](https://leetcode.com/contest/weekly-contest-168/problems/divide-array-in-sets-of-k-consecutive-numbers/)

```C++
class Solution {
public:
    bool isPossibleDivide(vector<int>& nums, int k) {
        if (k == 1) return true;
        if (nums.size() % k != 0) return false;
        
        multiset<int> st(nums.begin(), nums.end());
        while (!st.empty()) {
            int num = *(st.begin());
            for (int i = 1; i < k; i++) {
                if (st.find(num + i) == st.end()) return false;
            }
            
            for (int i = 0; i < k; i++) {
                st.erase(st.find(num + i));
            }
        }
        
        return true;
    }
};
```

## 3. [Maximum Number of Occurrences of a Substring](https://leetcode.com/contest/weekly-contest-168/problems/maximum-number-of-occurrences-of-a-substring/)

```C++

```

## 4. [Maximum Candies You Can Get from Boxes](https://leetcode.com/contest/weekly-contest-168/problems/maximum-candies-you-can-get-from-boxes/)

```C++

```

