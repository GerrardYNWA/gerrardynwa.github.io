title: LeetCode Weekly Contest 176
date: 2020-02-16 15:08:15
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第176场周赛

<!-- more -->

## 1. [Count Negative Numbers in a Sorted Matrix](https://leetcode.com/contest/weekly-contest-176/problems/count-negative-numbers-in-a-sorted-matrix/)

```C++
class Solution {
public:
    int countNegatives(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        int r = m - 1, c = 0, ans = 0;
        while (r >= 0 && c < n) {
            if (grid[r][c] < 0) {
                r--;
                ans += (n - c);
            } else {
                c++;
            }
        }
        
        return ans;
    }
};
```

## 2. [Product of the Last K Numbers](https://leetcode.com/contest/weekly-contest-176/problems/product-of-the-last-k-numbers/)

```C++

```

## 3. [Maximum Number of Events That Can Be Attended](https://leetcode.com/contest/weekly-contest-176/problems/maximum-number-of-events-that-can-be-attended/)

```C++

```

## 4. [Construct Target Array With Multiple Sums](https://leetcode.com/contest/weekly-contest-176/problems/construct-target-array-with-multiple-sums/)

```C++
class Solution {
public:
    bool isPossible(vector<int>& target) {
        long long sum = 0;
        int n = target.size();
        priority_queue<int> p;
        for (int i = 0; i < n; i++) {
            sum += target[i];
            p.push(target[i]);
        }
        
        while (p.top() != 1) {
            int t = p.top();
            p.pop();
            
            sum -= t;
            
            if (sum >= t) return false;
            
            int num = t - sum;
            sum += num;
            p.push(num);
        }
        
        return true;
    }
};
```

