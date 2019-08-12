Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

1. Integers in each row are sorted from left to right.
2. The first integer of each row is greater than the last integer of the previous row.

#### Note:
Note: Given n will be a positive integer.

#### Example1:
```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
```

#### Example2:
```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```

#### Solution
```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()) return false;
        int l=0;
        int r=matrix.size() * matrix[0].size();
        const int cols=matrix[0].size();
        while(l<r){
            const int m=l+(r-l)/2;
            if(matrix[m / cols][m % cols]==target){
                return true;
            }else if(matrix[m / cols][m % cols]>target){
                r=m;
            }else{
                l=m+1;
            }
        }
        return false;
    }
};
```