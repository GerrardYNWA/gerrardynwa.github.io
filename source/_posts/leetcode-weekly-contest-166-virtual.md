title: LeetCode Weekly Contest 166 (Virtual)
date: 2019-12-09 22:04:04
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第166场周赛（Virtual）

<!-- more -->

## 1. [Subtract the Product and Sum of Digits of an Integer](https://leetcode.com/contest/weekly-contest-166/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

```C++
class Solution {
public:
    int subtractProductAndSum(int n) {
        int product = 1, sum = 0;
        while (n) {
            int m = n % 10;
            product *= m;
            sum += m;
            n /= 10;
        }
        
        return product - sum;
    }
};
```

## 2. [Group the People Given the Group Size They Belong To](https://leetcode.com/contest/weekly-contest-166/problems/group-the-people-given-the-group-size-they-belong-to/)

```C++
class Solution {
public:
    vector<vector<int>> groupThePeople(vector<int>& groupSizes) {
        unordered_map<int, vector<int>> mp;
        for (int i = 0; i < groupSizes.size(); i++) {
            mp[groupSizes[i]].push_back(i);
        }
        
        vector<vector<int>> results;
        for (auto it : mp) {
            for (int i = 0; i < it.second.size() / it.first; i++) {
                vector<int> result;
                for (int j = 0; j < it.first; j++) {
                    result.push_back(it.second[i * it.first + j]);
                }
                results.push_back(result);
            }
        }
        
        return results;
    }
};
```

## 3. [Find the Smallest Divisor Given a Threshold](https://leetcode.com/contest/weekly-contest-166/problems/find-the-smallest-divisor-given-a-threshold/)

```C++
class Solution {
public:
    int sumOfDivision(vector<int>& nums, int divisor) {
        int sum = 0;
        for (int num : nums) {
            int division = num / divisor;
            
            if (num > divisor * division) division++;
            
            sum += division;
        }
        
        return sum;
    }
    
    int smallestDivisor(vector<int>& nums, int threshold) {
        int low = 1, high = *max_element(nums.begin(), nums.end());
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (sumOfDivision(nums, mid) > threshold) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        
        return low;
    }
};
```

## 4. [Minimum Number of Flips to Convert Binary Matrix to Zero Matrix](https://leetcode.com/contest/weekly-contest-166/problems/minimum-number-of-flips-to-convert-binary-matrix-to-zero-matrix/)

```C++
Todo
```

