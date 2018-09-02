Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

#### Example:
```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

#### Solution
```
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> res;
        
        for(int i=0;i<numRows;i++){
            vector<int> row;
            for(int j=0;j<i+1;j++){
                if(j==0 || j==i){
                    row.push_back(1);
                }else{
                    row.push_back(res[i-1][j-1]+res[i-1][j]);
                }
            }
            res.push_back(row);
        }
        return res;
        
    }
};
```