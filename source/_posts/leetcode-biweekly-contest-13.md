title: LeetCode Biweekly Contest 13
date: 2019-11-17 15:29:20
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第13场双周赛

<!-- more -->

## 1. [Encode Number](https://leetcode.com/contest/biweekly-contest-13/problems/encode-number/)

```C++
// class Solution {
// public:
//     string encode(int num) {
//         int k = log(num + 2) / log(2) - 1;
        
//         if (int(pow(2, k + 1)) == num + 2) k--;
        
//         int b = num + 1 - (pow(2, k + 1) - 1);
//         k++, b--;
        
//         string result(k, '0');
//         for (int i = k - 1; i >= 0; i--) {
//             if (b & 1) {
//                 result[i] = '1';
//             }
//             b >>= 1;
//         }
        
//         return result;
//     }
// };

class Solution {
public:
    string encode(int num) {
        string result = "";
        num++;
        while (num) {
            if (num & 1) {
                result = '1' + result;
            } else {
                result = '0' + result;
            }
            
            num >>= 1;
        }
        
        return result.substr(1);
    }
};
```

## 2. [Smallest Common Region](https://leetcode.com/contest/biweekly-contest-13/problems/smallest-common-region/)

```C++
class Solution {
public:
    string findSmallestRegion(vector<vector<string>>& regions, string region1, string region2) {
        unordered_map<string, string> mp;
        for (auto r : regions) {
            for (int i = 1; i < r.size(); i++) {
                mp[r[i]] = r[0];
            }
        }
        
        unordered_set<string> flag;
        while (true) {
            flag.insert(region1);
            if (mp.find(region1) == mp.end()) break;
            region1 = mp[region1];
        } 
        
        while (true) {
            if (flag.find(region2) != flag.end()) break;
            region2 = mp[region2];
        }
        
        return region2;
    }
};
```

## 3. [Synonymous Sentences](https://leetcode.com/contest/biweekly-contest-13/problems/synonymous-sentences/)

```C++
Todo
```

## 4. [Handshakes That Don't Cross](https://leetcode.com/contest/biweekly-contest-13/problems/handshakes-that-dont-cross/)

```C++
class Solution {
public:
    const long long MOD = 1e9+7;
    
    int numberOfWays(int num_people) {
        int n = num_people / 2;
        vector<long long> dp(n + 1, 0);
        dp[0] = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= i - 1; j++) {
                dp[i] += dp[j] * dp[i - 1 - j] % MOD;
                dp[i] %= MOD;
            }
        }
        
        return dp[n];
    }
};
```

