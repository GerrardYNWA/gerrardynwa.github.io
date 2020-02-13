title: LeetCode Weekly Contest 167 (Virtual)
date: 2019-12-18 15:06:17
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第167场周赛（Virtual）

<!-- more -->

## 1. [Convert Binary Number in a Linked List to Integer](https://leetcode.com/contest/weekly-contest-167/problems/convert-binary-number-in-a-linked-list-to-integer/)

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    int getDecimalValue(ListNode* head) {
        int ans = 0;
        
        while (head != nullptr) {
            ans <<= 1;
            ans += head->val;
            head = head->next;
        }
        
        return ans;
    }
};
```

## 2. [Sequential Digits](https://leetcode.com/contest/weekly-contest-167/problems/sequential-digits/)

```C++
class Solution {
public:
    vector<int> sequentialDigits(int low, int high) {
        vector<int> nums = {12, 23, 34, 45, 56, 67, 78, 89,
                            123, 234, 345, 456, 567, 678, 789,
                            1234, 2345, 3456, 4567, 5678, 6789,
                            12345, 23456, 34567, 45678, 56789,
                            123456, 234567, 345678, 456789,
                            1234567, 2345678, 3456789,
                            12345678, 23456789,
                            123456789};
        
        int l = lower_bound(nums.begin(), nums.end(), low) - nums.begin();
        int r = upper_bound(nums.begin(), nums.end(), high) - nums.begin();
        
        vector<int> result;
        for (int i = l; i < r; i++) {
            result.push_back(nums[i]);
        }
        
        return result;
    }
};
```

## 3. [Maximum Side Length of a Square with Sum Less than or Equal to Threshold](https://leetcode.com/contest/weekly-contest-167/problems/maximum-side-length-of-a-square-with-sum-less-than-or-equal-to-threshold/)

```C++

```

## 4. [Shortest Path in a Grid with Obstacles Elimination](https://leetcode.com/contest/weekly-contest-167/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

```C++

```

