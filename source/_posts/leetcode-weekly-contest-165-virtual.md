title: Leetcode Weekly Contest 165 (Virtual)
date: 2019-12-06 14:24:03
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第165场周赛（Virtual）

<!-- more -->

## 1. [Find Winner on a Tic Tac Toe Game](https://leetcode.com/contest/weekly-contest-165/problems/find-winner-on-a-tic-tac-toe-game/)

```C++
class Solution {
public:
    string tictactoe(vector<vector<int>>& moves) {
        vector<vector<int>> grid(3, vector<int>(3, 0));
        for (int i = 0; i < moves.size(); i++) {
            if (i & 1) {
                grid[moves[i][0]][moves[i][1]] = -1;
            } else {
                grid[moves[i][0]][moves[i][1]] = 1;
            }
        }
        
        vector<int> sum_row(3, 0), sum_col(3, 0);
        int sum_diag = 0, sum_anti = 0;
        for (int i = 0; i < 3; i++) {
            sum_diag += grid[i][i];
            sum_anti += grid[i][2 - i];
            
            for (int j = 0; j < 3; j++) {
                sum_row[i] += grid[i][j];
                sum_col[j] += grid[i][j];
            }
        }
        
        for (int i = 0; i < 3; i++) {
            if (sum_diag == 3 || sum_anti == 3 || sum_row[i] == 3 || sum_col[i] == 3) {
                return "A";
            }
            
            if (sum_diag == -3 || sum_anti == -3 || sum_row[i] == -3 || sum_col[i] == -3) {
                return "B";
            }
        }
        
        return moves.size() == 9 ? "Draw" : "Pending";
    }
};
```

## 2. [Number of Burgers with No Waste of Ingredients](https://leetcode.com/contest/weekly-contest-165/problems/number-of-burgers-with-no-waste-of-ingredients/)

```C++
class Solution {
public:
    vector<int> numOfBurgers(int tomatoSlices, int cheeseSlices) {
        if ((tomatoSlices & 1) || (tomatoSlices < 2 * cheeseSlices) || (tomatoSlices > 4 * cheeseSlices)) return {};
        
        return {tomatoSlices / 2 - cheeseSlices, 2 * cheeseSlices - tomatoSlices / 2};
    }
};
```

## 3. [Count Square Submatrices with All Ones](https://leetcode.com/contest/weekly-contest-165/problems/count-square-submatrices-with-all-ones/)

```C++
class Solution {
public:
    int countSquares(vector<vector<int>>& matrix) {
        int rows = matrix.size();
        int cols = matrix[0].size();
        
        int ans = 0;
        vector<vector<int>> dp(rows + 1, vector<int>(cols + 1, 0));
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j]) {
                    dp[i + 1][j + 1] = min(dp[i][j], min(dp[i + 1][j], dp[i][j + 1])) + 1;
                    ans += dp[i + 1][j + 1];
                }
            }
        }
        
        return ans;
    }
};
```

## 4. [Palindrome Partitioning III](https://leetcode.com/contest/weekly-contest-165/problems/palindrome-partitioning-iii/)

```C++
class Solution {
public:
    int palindromePartition(string s, int k) {
        int n = s.length();
        vector<vector<int>> sp(n, vector<int>(n, 0));
        vector<vector<int>> dp(n, vector<int>(k + 1, 0));
        
        for (int d = 1; d < n; d++) {
            for (int i = 0; i + d < n; i++) {
                if (s[i] == s[i + d]) {
                    sp[i][i + d] = sp[i + 1][i + d - 1];
                } else {
                    sp[i][i + d] = sp[i + 1][i + d - 1] + 1;
                }
            }
        }
        
        for (int i = 0; i < n; i++) {
            dp[i][1] = sp[0][i];
        }
        
        for (int c = 2; c <= k; c++) {
            for (int i = 1; i < n; i++) {
                dp[i][c] = i + 1;
                for (int j = 0; j < i; j++) {
                    dp[i][c] = min(dp[i][c], dp[j][c - 1] + sp[j + 1][i]);
                }
            }
        }
        
        return dp[n - 1][k];
    }
};
```

