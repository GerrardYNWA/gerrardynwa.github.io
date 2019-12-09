title: LeetCode Biweekly Contest 14
date: 2019-12-02 23:07:49
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第14场双周赛

<!-- more -->

## 1. [Hexspeak](https://leetcode.com/contest/biweekly-contest-14/problems/hexspeak/)

```C++
class Solution {
public:
    string toHexspeak(string num) {
        string result = "";
        auto n = stol(num);
        if (n == 0) return "O";
        
        while (n > 0) {
            int m = n % 16;
            if (m >= 2 && m <= 9) {
                return "ERROR";
            } else {
                if (m == 0) {
                    result += 'O';
                } else if (m == 1) {
                    result += 'I';
                } else {
                    result += ('A' + (m - 10));
                }
            }
            
            n /= 16;
        }
        
        reverse(result.begin(), result.end());
        
        return result;
    }
};
```

## 2. [Remove Interval](https://leetcode.com/contest/biweekly-contest-14/problems/remove-interval/)

```C++
class Solution {
public:
    vector<vector<int>> removeInterval(vector<vector<int>>& intervals, vector<int>& toBeRemoved) {
        int n = intervals.size();
        if (toBeRemoved[0] >= intervals[n - 1][1] || toBeRemoved[1] < intervals[0][0]) return intervals;
        if (toBeRemoved[0] <= intervals[0][0] && toBeRemoved[1] >= intervals[n - 1][1]) return {};
        
        vector<int> nums;
        for (auto interval : intervals) {
            nums.push_back(interval[0]);
        }
        
        vector<vector<int>> result;
        int l = lower_bound(nums.begin(), nums.end(), toBeRemoved[0]) - nums.begin();
        int r = lower_bound(nums.begin(), nums.end(), toBeRemoved[1]) - nums.begin();
        for (int i = 0; i <= l - 2; i++) {
            result.push_back(intervals[i]);
        }
        
        if ((l - 1 >= 0) && (l - 1 < n)) result.push_back({intervals[l - 1][0], min(toBeRemoved[0], intervals[l - 1][1])});
        
        if ((r - 1 >= 0) && (r - 1 < n) && toBeRemoved[1] < intervals[r - 1][1]) {
            result.push_back({toBeRemoved[1], intervals[r - 1][1]});
        }
        
        for (int i = r; i < n; i++) {
            result.push_back(intervals[i]);
        }
        
        return result;
    }
};
```

## 3. [Delete Tree Nodes](https://leetcode.com/contest/biweekly-contest-14/problems/delete-tree-nodes/)

```C++
class Solution {
public:
    int deleteTreeNodes(int nodes, vector<int>& parent, vector<int>& value) {
        for (int i = nodes - 1; i >= 0; i--) {
            int j = i;
            while (parent[j] != -1) {
                value[parent[j]] += value[j];
                j = parent[j];
            }
        }
        
        vector<vector<int>> links(nodes);
        for (int i = 0; i < nodes; i++) {
            if (parent[i] != -1) {
                links[parent[i]].push_back(i);
            }
        }
        
        if (value[0] == 0) return 0;
        
        for (int i = 0; i < nodes; i++) {
            if (value[i] == 0) {
                for (int val : links[i]) {
                    value[val] = 0;
                }
            }
        }
        
        int result = 0;
        for (int v : value) {
            if (v != 0) result++;
        }
        
        return result;
    }
};
```

## 4. [Number of Ships in a Rectangle](https://leetcode.com/contest/biweekly-contest-14/problems/number-of-ships-in-a-rectangle/)

```C++
/**
 * // This is Sea's API interface.
 * // You should not implement it, or speculate about its implementation
 * class Sea {
 *   public:
 *     bool hasShips(vector<int> topRight, vector<int> bottomLeft);
 * };
 */

class Solution {
public:
    int helper(Sea& sea, int x1, int y1, int x2, int y2) {
        if (x1 < x2 || y1 < y2) return 0;
        if (!sea.hasShips({x1, y1}, {x2, y2})) return 0;
        if (x1 == x2 && y1 == y2 && sea.hasShips({x1, y1}, {x2, y2})) return 1;
        
        int a = (x1 - x2) / 2, b = (y1 - y2) / 2;
        
        return helper(sea, x2 + a, y2 + b, x2, y2) + 
               helper(sea, x1, y2 + b, x2 + a + 1, y2) + 
               helper(sea, x2 + a, y1, x2, y2 + b + 1) + 
               helper(sea, x1, y1, x2 + a + 1, y2 + b + 1);
    }
    
    int countShips(Sea sea, vector<int> topRight, vector<int> bottomLeft) {
        return helper(sea, topRight[0], topRight[1], bottomLeft[0], bottomLeft[1]);
    }
};
```

