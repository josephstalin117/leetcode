Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

#### Note:
You can only move either down or right at any point in time.

#### Example:
```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

#### Solution
采用动态规划。动态规划要求利用到上一次的结果，是一种特殊的迭代思想，动态规划的关键是要得到递推关系式。对于本题，从原点到达（i, j）的最小路径等于：原点到达（i-1, j）最小路径与到达（i, j-1）最小路径中的最小值。即 dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]。
```
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m=grid.size();
        if(m==0) return 0;
        int n=grid[0].size();
        
        for(int i=0;i<m;++i){
            for(int j=0;j<n;++j){
                if(i==0 && j==0){
                    continue;
                }
                if(i==0){
                    grid[i][j]+=grid[i][j-1];
                }else if(j==0){
                    grid[i][j]+=grid[i-1][j];
                }else{
                    grid[i][j]+=min(grid[i][j-1],grid[i-1][j]);
                }
            }
        }
        return grid[m-1][n-1];
    }
};
```
