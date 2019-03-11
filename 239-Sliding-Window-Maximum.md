Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

#### Example:
```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

#### Note:
You may assume k is always valid, 1 ≤ k ≤ input array's size for non-empty array.

#### Follow up:
Could you solve it in linear time?

#### Solution1
Brute Force
Time complexity: O((n – k + 1) * k)
Space complexity: O(1)
```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ans;
        for (int i = k - 1; i < nums.size(); ++i) {
            ans.push_back(*max_element(nums.begin() + i - k + 1, nums.begin() + i + 1));
        }
        return ans;
    }
};
```

#### Solution2
