Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

#### Example:
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

#### Follow up:
```
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```

#### Solution1
```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
    	//dp 来处理
        int sum = 0;
        //注意使用 INT_MIN
        int m = INT_MIN;

        for(int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            m = max(m, sum);
            if(sum < 0) {
                sum = 0;
            }
        }
        return m;   
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