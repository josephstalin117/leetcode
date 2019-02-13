Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.
#### Example1:
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

#### Example2:
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

#### solution
```
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {
        auto it=intervals.begin();
        while(it!=intervals.end() && newInterval.start >it->start){
            ++it;
        }
        intervals.insert(it, newInterval);
        
        //merge
        vector<Interval> res;
        for(const auto& interval:intervals){
            if(res.empty() || interval.start> res.back().end){
                res.push_back(interval);
            }else{
                res.back().end=max(res.back().end, interval.end);
            }
        }
        return res;
    }
};
```
