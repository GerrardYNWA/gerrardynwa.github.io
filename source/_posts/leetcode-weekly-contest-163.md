title: LeetCode Weekly Contest 163
date: 2019-11-17 19:29:54
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第163场周赛

<!-- more -->

## 1. [Shift 2D Grid](https://leetcode.com/contest/weekly-contest-163/problems/shift-2d-grid/)

```C++
class Solution {
public:
    vector<vector<int>> shiftGrid(vector<vector<int>>& grid, int k) {
        int n = grid.size();
        int m = grid[0].size();
        
        k %= (n * m);
        
        vector<vector<int>> result(n, vector<int>(m));
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                int pos = (i * m + j + k) % (n * m);
                int row = pos / m;
                int col = pos % m;
                result[row][col] = grid[i][j];
            }
        }
        
        return result;
    }
};
```

## 2. [Find Elements in a Contaminated Binary Tree](https://leetcode.com/contest/weekly-contest-163/problems/find-elements-in-a-contaminated-binary-tree/)

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
class FindElements {
public:
    set<int> st;
public:
    FindElements(TreeNode* root) {
        init(root, 0);
    }
    
    bool find(int target) {
        if (st.find(target) != st.end()) {
            return true;
        } else {
            return false;
        }
    }
    
    void init(TreeNode* root, int val) {
        if (root == nullptr) return;
        
        root->val = val;
        st.insert(val);
        
        init(root->left, val * 2 + 1);
        init(root->right, val * 2 + 2);
    }
};

/**
 * Your FindElements object will be instantiated and called as such:
 * FindElements* obj = new FindElements(root);
 * bool param_1 = obj->find(target);
 */
```

## 3. [Greatest Sum Divisible by Three](https://leetcode.com/contest/weekly-contest-163/problems/greatest-sum-divisible-by-three/)

```C++
class Solution {
public:
    int maxSumDivThree(vector<int>& nums) {
        vector<int> dp(3, 0), next;
        for (int num : nums) {
            next = dp;
            for (int sum : next) {
                dp[(sum + num) % 3] = max(dp[(sum + num) % 3], sum + num);
            }
        }
        
        return dp[0];
    }
};

// class Solution {
// public:
//     int maxSumDivThree(vector<int>& nums) {
//         vector<int> dp(3, 0), result(3, 0);
//         dp[1] = dp[2] = INT_MIN;
//         for (int num : nums) {
//             int remainer = num % 3;
//             if (remainer == 0) {
//                 result[0] = dp[0] + num;
//                 result[1] = dp[1] + num;
//                 result[2] = dp[2] + num;
//             } else if (remainer == 1) {
//                 result[0] = max(dp[0], dp[2] + num);
//                 result[1] = max(dp[1], dp[0] + num);
//                 result[2] = max(dp[2], dp[1] + num);
//             } else if (remainer == 2) {
//                 result[0] = max(dp[0], dp[1] + num);
//                 result[1] = max(dp[1], dp[2] + num);
//                 result[2] = max(dp[2], dp[0] + num);
//             }
            
//             for (int i = 0; i < 3; i++) dp[i] = result[i];
//         }
        
//         return result[0];
//     }
// };

// class Solution {
// public:
//     int maxSumDivThree(vector<int>& nums) {
//         int n = nums.size();
//         vector<vector<int>> dp(n + 1, vector<int>(3, 0));
//         dp[0][1] = dp[0][2] = INT_MIN;
//         for (int i = 0; i < n; i++) {
//             int remainer = nums[i] % 3;
//             if (remainer == 0) {
//                 dp[i + 1][0] = dp[i][0] + nums[i];
//                 dp[i + 1][1] = dp[i][1] + nums[i];
//                 dp[i + 1][2] = dp[i][2] + nums[i];
//             } else if (remainer == 1) {
//                 dp[i + 1][0] = max(dp[i][0], dp[i][2] + nums[i]);
//                 dp[i + 1][1] = max(dp[i][1], dp[i][0] + nums[i]);
//                 dp[i + 1][2] = max(dp[i][2], dp[i][1] + nums[i]);
//             } else if (remainer == 2) {
//                 dp[i + 1][0] = max(dp[i][0], dp[i][1] + nums[i]);
//                 dp[i + 1][1] = max(dp[i][1], dp[i][2] + nums[i]);
//                 dp[i + 1][2] = max(dp[i][2], dp[i][0] + nums[i]);
//             }
//         }
        
//         return dp[n][0];
//     }
// };
// class Solution {
// public:
//     int maxSumDivThree(vector<int>& nums) {
//         int sum = 0;
//         vector<int> left;
//         for (auto num : nums) {
//             if (num % 3 == 0) {
//                 sum += num;
//             } else {
//                 left.push_back(num);
//             }
//         }
        
//         int n = left.size();
//         vector<vector<int>> dp(n + 1, vector<int>(3, 0));
//         for (int i = 0; i < n; i++) {
//             int remainer = left[i] % 3;
//             if (remainer == 1) {
//                 dp[i + 1][0] = (dp[i][2] == 0 ? dp[i][0] : max(dp[i][0], dp[i][2] + left[i]));
//                 dp[i + 1][1] = max(dp[i][1], dp[i][0] + left[i]);
//                 dp[i + 1][2] = (dp[i][1] == 0 ? dp[i][2] : max(dp[i][2], dp[i][1] + left[i]));
//             } else if (remainer == 2) {
//                 dp[i + 1][0] = (dp[i][1] == 0 ? dp[i][0] : max(dp[i][0], dp[i][1] + left[i]));
//                 dp[i + 1][1] = (dp[i][2] == 0 ? dp[i][1] : max(dp[i][1], dp[i][2] + left[i]));
//                 dp[i + 1][2] = max(dp[i][2], dp[i][0] + left[i]);
//             }
//         }
        
//         return sum + dp[n][0];
//     }
// };
```

## 4. [Minimum Moves to Move a Box to Their Target Location](https://leetcode.com/contest/weekly-contest-163/problems/minimum-moves-to-move-a-box-to-their-target-location/)

```C++
Todo
```

