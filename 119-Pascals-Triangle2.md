Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.

#### Example:
```
Input: 3
Output: [1,3,3,1]
```

#### Solution1
```
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> res;
        
        for(int i=0;i<=rowIndex;i++){
            if(i==0 || i==rowIndex){
                res.push_back(1);
            }else{
                if(i<=rowIndex/2){
                    res.push_back(getNum(rowIndex, i));
                }else{
                    res.push_back(res[rowIndex-i]);
                }
            }
        }
        return res;
    }
    
    int getNum(int rowIndex, int colIndex){
        int num = 0;
        if(colIndex == 0 || rowIndex == colIndex){
            num = 1;
        }else{
            num = getNum(rowIndex - 1, colIndex -1)+getNum(rowIndex - 1, colIndex);
        }
        return num;
        
    }
};
```

#### Solution2
```
class Solution {
public:
    //套用公式
    vector<int> getRow(int rowIndex) {
        vector<int> r;
        r.resize(rowIndex + 1);
        r[0] = r[rowIndex] = 1;
        for (auto i = 1; i < (r.size() + 1) / 2; ++i) {
            r[i] = r[rowIndex - i] = (unsigned long)r[i - 1] * (unsigned long)(rowIndex - i + 1) / i;
        }
        return r;
    }
};
```