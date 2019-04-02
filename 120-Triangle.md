Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

#### Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

#### Solution
简单的动态规划，找出状态转移方程就可以了。采用由下到上的思想（这样最后只需要取出dp[0][0]就是答案），本层每个结点的结果根据下面一行的路基累计和而计算，要么取左边的，要么取右边的，两者取最小的即可。
状态转移方程：triangle[i][j] += min(triangle[i + 1][j], triangle[i + 1][j + 1]) 
```
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        for(int i=triangle.size()-2; i>=0; --i){
            for(int j=0; j<=i; ++j){
                triangle[i][j]+=min(triangle[i+1][j+1], triangle[i+1][j]);
            }
        }
        return triangle[0][0];
    }
};
```