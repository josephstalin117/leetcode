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
BST
Time complexity: O((n – k + 1) * logk)
Space complexity: O(k)
```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ans;
        if (nums.empty()){
            return ans;
        }
        multiset<int> window(nums.begin(), nums.begin() + k - 1);
        for (int i = k - 1; i < nums.size(); ++i) {
            window.insert(nums[i]);
            ans.push_back(*window.rbegin());
            if (i - k + 1 >= 0){
                window.erase(window.equal_range(nums[i - k + 1]).first);
            }
        }
        return ans;
    }
};
```

#### Solution3
双向队列，只保留最大的值，忽略无关的值
```
class Solution {
public:
    class MonotonicQueue {
        public:
        void push(int e) {
            //去除比较小的值
            while(!data_.empty() && e > data_.back()) data_.pop_back();
            data_.push_back(e);
        }
  
        void pop() {
            //去除不在窗口中的值
            data_.pop_front();
        }
  
        int max() const { 
            return data_.front(); 
        }
        private:
            deque<int> data_;
    };
    
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        MonotonicQueue q;
        vector<int> ans;
        
        for (int i = 0; i < nums.size(); ++i) {
            q.push(nums[i]);
            if (i - k + 1 >= 0) {
                ans.push_back(q.max());
                //去除不属于窗口的值
                if (nums[i - k + 1] == q.max()){
                    q.pop();
                }
            }      
        }
        return ans;
    }
};
```