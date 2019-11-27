title: Leetcode Weekly Contest 164 (Virtual)
date: 2019-11-25 16:33:24
categories: Algorithm 

tags: [leetcode]
---

　　LeetCode第164场周赛（Virtual）

<!-- more -->

## 1. [Minimum Time Visiting All Points](https://leetcode.com/contest/weekly-contest-164/problems/minimum-time-visiting-all-points/)

```C++
class Solution {
public:
    int minTimeToVisitAllPoints(vector<vector<int>>& points) {
        int sum = 0;
        for (int i = 1; i < points.size(); i++) {
            sum += max(abs(points[i][0] - points[i - 1][0]), abs(points[i][1] - points[i - 1][1]));
        }
        
        return sum;
    }
};
```

## 2. [Count Servers that Communicate](https://leetcode.com/contest/weekly-contest-164/problems/count-servers-that-communicate/)

```C++
class Solution {
public:  
    int countServers(vector<vector<int>>& grid) {
        int ans = 0;
        int m = grid.size();
        int n = grid[0].size();
        vector<int> sum_row(m, 0), sum_col(n, 0);
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                sum_row[i] += grid[i][j];
                sum_col[j] += grid[i][j];
            }
        }
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1 && (sum_row[i] > 1 || sum_col[j] > 1)) {
                    ans++;
                }
            }
        }
        
        return ans;
    }
};
```

## 3. [Search Suggestions System](https://leetcode.com/contest/weekly-contest-164/problems/search-suggestions-system/)

```C++
class Solution {
public:
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
        int len = searchWord.length();
        vector<vector<string>> results;
        
        sort(products.begin(), products.end());
        
        for (int i = 0; i < len; i++) {
            vector<string> result;
            
            for (auto p : products) {
                if (result.size() >= 3) {
                    break;
                } else if (p.length() > i && p.substr(0, i + 1) == searchWord.substr(0, i + 1)) {
                    result.push_back(p);
                }
            }
            
            results.push_back(result);
        }
        
        return results;
    }
};
```

## 4. [Number of Ways to Stay in the Same Place After Some Steps](https://leetcode.com/contest/weekly-contest-164/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps/)

```C++
static int MOD = 1e9 + 7;

class Solution {
public:
    vector<vector<int>> memo;
    
    int numWays(int steps, int arrLen) {
        memo.resize(steps / 2 + 1, vector<int>(steps + 1, -1));
        
        return dfs(arrLen, 0, steps);
    }
    
    int dfs(int arrLen, int pos, int steps) {
        if (steps == 0 && pos == 0) return 1;
        if (pos < 0 || pos >= arrLen || steps == 0 || pos > steps) return 0;
        
        if (memo[pos][steps] != -1) return memo[pos][steps];
        
        int stay = dfs(arrLen, pos, steps - 1) % MOD;
        int left = dfs(arrLen, pos - 1, steps - 1) % MOD;
        int right = dfs(arrLen, pos + 1, steps - 1) % MOD;
        
        return memo[pos][steps] = ((stay + left) % MOD + right) % MOD;
        
    }
};
```

