A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

#### Note:
m and n will be at most 100.

#### Example1:
```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

#### Solution
```
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if(obstacleGrid.empty() || obstacleGrid[0].empty() || obstacleGrid[0][0]==1){
            return 0;
        }
        int m=obstacleGrid.size(), n=obstacleGrid[0].size();
        vector<long> dp(n,1);
        for(int j=1; j<n; j++){
            if(obstacleGrid[0][j]==1){
                dp[j]=0;
            }else{
                dp[j]=dp[j-1];
            }
        }
        
        for(int i=1; i<m; i++){
            dp[0] = obstacleGrid[i][0]==1?0:dp[0];
            for(int j=1; j<n; j++){
                dp[j]= obstacleGrid[i][j]==1?0:dp[j-1]+dp[j];
            }
        }
        return dp[n-1];
    }
};
```
