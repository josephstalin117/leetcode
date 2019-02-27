Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

#### Example:
```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```

#### solution
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.empty() || matrix[0].empty()){
            return {};
        }
        int m = matrix.size();
        int n = matrix[0].size();
        vector<int> res;
        int up = 0, down = m - 1, left = 0, right = n - 1;
        while (true) {
            for (int j = left; j <= right; ++j){
                res.push_back(matrix[up][j]);
            }
            if (++up > down) break;
            for (int i = up; i <= down; ++i){
                res.push_back(matrix[i][right]);
            }
            if (--right < left) break;
            for (int j = right; j >= left; --j){
                res.push_back(matrix[down][j]);
            }  
            if (--down < up) break;
            for (int i = down; i >= up; --i){
                res.push_back(matrix[i][left]);
            }
            if (++left > right) break;
        }
        return res;
    }
};
```
