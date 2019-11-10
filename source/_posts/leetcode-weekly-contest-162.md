title: LeetCode Weekly Contest 162
date: 2019-11-10 18:12:35
categories: Algorithm

tags: [leetcode]
---

　　LeetCode第162场周赛

<!-- more -->

## 1. [Cells with Odd Values in a Matrix](https://leetcode.com/contest/weekly-contest-162/problems/cells-with-odd-values-in-a-matrix/)

```C++
class Solution {
public:
    int oddCells(int n, int m, vector<vector<int>>& indices) {
        int ans = 0;
        vector<int> rows(n, 0);
        vector<int> cols(m, 0);
        for (auto indice : indices) {
            rows[indice[0]]++;
            cols[indice[1]]++;
        }
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if ((rows[i] + cols[j]) & 1) {
                    ans++;
                }
            }
        }
        
        return ans;
    }
};
```

## 2. [Reconstruct a 2-Row Binary Matrix](https://leetcode.com/contest/weekly-contest-162/problems/reconstruct-a-2-row-binary-matrix/)

```C++
class Solution {
public:
    vector<vector<int>> reconstructMatrix(int upper, int lower, vector<int>& colsum) {
        int n = colsum.size();
        vector<vector<int>> matrix(2, vector<int>(n, 0));
        
        int remainer = 0;
        for (int i = 0; i < colsum.size(); i++) {
            if (colsum[i] == 2) {
                matrix[0][i] = 1;
                matrix[1][i] = 1;
                upper--, lower--;
            } else if (colsum[i] == 1) {
                remainer++;
            }
        }
        
        if (upper < 0 || lower < 0 || (upper + lower) != remainer) return {};
        
        for (int i = 0; i < colsum.size(); i++) {
            if (colsum[i] == 1) {
                if (upper > 0) {
                    matrix[0][i] = 1;
                    upper--;
                } else if (lower > 0) {
                    matrix[1][i] = 1;
                    lower--;
                } else {
                    return {};
                }  
            }
        }
        
        return matrix;
    }
};
```

## 3. [Number of Closed Islands](https://leetcode.com/contest/weekly-contest-162/problems/number-of-closed-islands/)

```C++
class Solution {
public:
    int closedIsland(vector<vector<int>>& grid) {
        int res = 0;
        int rows = grid.size();
        int cols = grid[0].size();
        
        for (int i = 0; i < rows; i++) {
            dfs(grid, i, 0);
            dfs(grid, i, cols - 1);
        }

        for (int j = 0; j < rows; j++) {
            dfs(grid, 0, j);
            dfs(grid, rows - 1, j);
        }
        
        for (int i = 1; i < rows - 1; i++) {
            for (int j = 1; j < cols - 1; j++) {
                if (grid[i][j] == 0) {
                    dfs(grid, i, j);
                    res++;
                }
            }
        }
        
        return res;
    }
    
    void dfs(vector<vector<int>>& grid, int row, int col) {
        int rows = grid.size();
        int cols = grid[0].size();
        
        if (row < 0 || row >= rows || col < 0 || col >= cols || grid[row][col] == 1) {
            return;
        }
        
        grid[row][col] = 1;
        
        dfs(grid, row - 1, col);
        dfs(grid, row + 1, col);
        dfs(grid, row, col - 1);
        dfs(grid, row, col + 1);
    }
};
```

## 4. [Maximum Score Words Formed by Letters](https://leetcode.com/contest/weekly-contest-162/problems/maximum-score-words-formed-by-letters/)

```C++
class Solution {
public:
    int ans = 0;
    
    int maxScoreWords(vector<string>& words, vector<char>& letters, vector<int>& score) {
        vector<int> count(26, 0), used(26, 0);
        for (auto c : letters) count[c - 'a']++;
        
        backtrack(words, score, count, used, 0, 0);
        
        return ans;
    }
    
    void backtrack(const vector<string>& words, const vector<int>& score, const vector<int>& count, vector<int>& used, int pos, int reward) {
        for (int i = 0; i < 26; i++) {
            if (count[i] < used[i]) {
                return;
            }
        }
        
        ans = max(ans, reward);
        
        for (int i = pos; i < words.size(); i++) {
            for (auto c : words[i]) {
                used[c - 'a']++;
                reward += score[c - 'a'];
            }
            
            backtrack(words, score, count, used, i + 1, reward);
            
            for (auto c : words[i]) {
                used[c - 'a']--;
                reward -= score[c - 'a'];
            }
        }
    }
};
```

