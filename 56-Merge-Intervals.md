Given a collection of intervals, merge all overlapping intervals.

#### Example1:
```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

#### Example2:
```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
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
    vector<Interval> merge(vector<Interval>& intervals) {
        if(intervals.empty()){
            return {};
        }
        sort(intervals.begin(), intervals.end(), [](Interval &a, Interval &b) {return a.start < b.start;});
        //c++11
        vector<Interval> res{intervals[0]};
        for(int i=1;i<intervals.size();++i){
            if (res.back().end < intervals[i].start) {
                res.push_back(intervals[i]);
            } else {
                res.back().end = max(res.back().end, intervals[i].end);
            }
        }
        return res;
    }
};
```
