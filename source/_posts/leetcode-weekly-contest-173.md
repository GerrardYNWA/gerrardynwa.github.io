title: LeetCode Weekly Contest 173
date: 2020-01-29 15:08:15
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第173场周赛

<!-- more -->

## 1. [Remove Palindromic Subsequences](https://leetcode.com/contest/weekly-contest-173/problems/remove-palindromic-subsequences/)

```C++
class Solution {
public:
    int removePalindromeSub(string s) {
        int n = s.length();
        if (n == 0) return 0;
        
        int l = 0, r = n - 1;
        while (l <= r) {
            if (s[l] == s[r]) {
                l++, r--;
            } else {
                return 2;
            }
        }
        
        return 1;
    }
};
```

## 2. [Filter Restaurants by Vegan-Friendly, Price and Distance](https://leetcode.com/contest/weekly-contest-173/problems/filter-restaurants-by-vegan-friendly-price-and-distance/)

```C++
class Solution {
public:
    vector<int> filterRestaurants(vector<vector<int>>& restaurants, int veganFriendly, int maxPrice, int maxDistance) {
        vector<int> result;
        for (int i = 0; i < restaurants.size(); i++) {
            if (veganFriendly) {
                if (restaurants[i][2] && restaurants[i][3] <= maxPrice && restaurants[i][4] <= maxDistance) result.push_back(i);
            } else {
                if (restaurants[i][3] <= maxPrice && restaurants[i][4] <= maxDistance) result.push_back(i);
            }
        }
        
        sort(result.begin(), result.end(), [&restaurants](int i, int j) {
            if (restaurants[i][1] == restaurants[j][1]) {
                return restaurants[i][0] > restaurants[j][0];
            } else {
                return restaurants[i][1] > restaurants[j][1];
            }
        });
        
        for (int i = 0; i < result.size(); i++) {
            result[i] = restaurants[result[i]][0];
        }
        
        return result;
    }
};
```

## 3. [Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/contest/weekly-contest-173/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/)

```C++

```

## 4. [Minimum Difficulty of a Job Schedule](https://leetcode.com/contest/weekly-contest-173/problems/minimum-difficulty-of-a-job-schedule/)

```C++
class Solution {
public:
    int minDifficulty(vector<int>& jobDifficulty, int d) {
        int n = jobDifficulty.size(), inf = 1e9;
        if (n < d) return -1;
        
        vector<int> dp(n + 1, inf);
        dp[n] = 0;
        for (int t = 1; t <= d; t++) {
            for (int i = 0; i <= n - t; i++) {
                int maxd = 0;
                dp[i] = inf;
                for (int j = i; j <= n - t; j++) {
                    maxd = max(maxd, jobDifficulty[j]);
                    dp[i] = min(dp[i], maxd + dp[j + 1]);
                }
            }
        }
        
        return dp[0];
    }
};
```

