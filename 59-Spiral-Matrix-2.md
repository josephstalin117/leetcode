Given a positive integer n, generate a square matrix filled with elements from 1 to n^2 in spiral order.

#### Example:
```
Input: 3
Output:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

#### Solution
```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, 0));
        int left = 0;
        int right = n - 1;
        int up = 0;
        int down = n - 1;
        int count =1;
        while(left<=right && up<=down){
            for(int i=left;i<=right;i++){
                res[up][i]=count++;
            }
            up++;
            for(int i=up; i<=down; i++){
                res[i][right]=count++;
            }
            right--;
            for(int i=right; i>=left; i--){
                res[down][i]=count++;
            }
            down--;
            for(int i=down; i>=up; i--){
                res[i][left]=count++;
            }
            left++;
        }
        return res;
    }
};
```

#### Solution2
```
// 1. 最大值在A[left, mid - 1]里面
// 2. 最大值在A[mid + 1, right]里面
// 3. 最大值跨过了mid，也就是我们需要计算[left, mid - 1]区间的最大值，以及[mid + 1, right]的最大值，然后加上mid，三者之和就是总的最大值
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        return divide(nums, 0, nums.size()-1, INT_MIN);
    }
    
    int divide(vector<int>& nums, int left, int right, int tmax){
        if(left > right) {
            return INT_MIN;
        }
        if(left==right){
            return nums[left];
        }
        
        int mid = left + (right - left) / 2;
        //得到子区间[left, mid - 1]最大值
        int lmax = divide(nums, left, mid - 1, tmax);
        //得到子区间[mid + 1, right]最大值
        int rmax = divide(nums, mid + 1, right, tmax);

        tmax = max(tmax, lmax);
        tmax = max(tmax, rmax);

        int sum = 0;
        int mlmax = 0;
        //得到[left, mid - 1]最大值
        for(int i = mid - 1; i >= left; i--) {
            sum += nums[i];
            mlmax = max(mlmax, sum);
        }

        sum = 0;
        int mrmax = 0;
        //得到[mid + 1, right]最大值
        for(int i = mid + 1; i <= right; i++) {
            sum += nums[i];
            mrmax = max(mrmax, sum);
        }

        tmax = max(tmax, nums[mid] + mlmax + mrmax);
        return tmax;   
    }
};
```
