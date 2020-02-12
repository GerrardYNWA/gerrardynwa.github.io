title: LeetCode Weekly Contest 174
date: 2020-02-05 15:08:15
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第174场周赛

<!-- more -->

## 1. [The K Weakest Rows in a Matrix](https://leetcode.com/contest/weekly-contest-174/problems/the-k-weakest-rows-in-a-matrix/)

```C++
class Solution {
public:
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        int rows = mat.size();
        int cols = mat[0].size();
        vector<int> soliders(rows, 0);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                soliders[i] += mat[i][j];
            }
        }
        
        vector<pair<int, int>> p;
        for (int i = 0; i < rows; i++) {
            p.push_back(make_pair(soliders[i], i));
        }
        
        sort(p.begin(), p.end());
        
        vector<int> result;
        for (int i = 0; i < k; i++) {
            result.push_back(p[i].second);
        }
        
        return result;
    }
};
```

## 2. [Reduce Array Size to The Half](https://leetcode.com/contest/weekly-contest-174/problems/reduce-array-size-to-the-half/)

```C++
class Solution {
public:
    int minSetSize(vector<int>& arr) {
        unordered_map<int, int> mp;
        for (auto& a : arr) {
            mp[a]++;
        }
        
        vector<pair<int, int>> p;
        for (auto& it : mp) {
            p.push_back(make_pair(it.second, it.first));
        }
        
        sort(p.begin(), p.end());
        
        int n = arr.size();
        int cnt = 0;
        for (int i = p.size() - 1; i >= 0; i--) {
            cnt += p[i].first;
            if (cnt >= n / 2) {
                return p.size() - i;
            }
        }
        
        return 0;
    }
};
```

## 3. [Maximum Product of Splitted Binary Tree](https://leetcode.com/contest/weekly-contest-174/problems/maximum-product-of-splitted-binary-tree/)

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int MOD = 1e9 + 7;
    long result = 0, total = 0;
    
    int getSum(TreeNode* root, bool flag) {
        if (root == nullptr) return 0;
        
        int sum = root->val + getSum(root->left, flag) + getSum(root->right, flag);
        
        if (flag) result = max(result, sum * (total - sum));
        
        return sum;
    }
    
    int maxProduct(TreeNode* root) {
        total = getSum(root, false);
        getSum(root, true);
        
        return result % MOD;
    }
};
```

## 4. [Jump Game V](https://leetcode.com/contest/weekly-contest-174/problems/jump-game-v/)

```C++

```

