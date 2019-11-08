# Intervals

+ [Non-overlapping Intervals](#non-overlapping-intervals)
+ [Merge Intervals](#merge-intervals)
+ [Insert Interval](#insert-interval)

## Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

```C++
bool BeginCompare(vector<int>& a, vector<int>& b){
       return (a[0] < b[0]);
}    
class Solution {   
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals){
        if (intervals.size() == 0)
          return intervals.size();
        int length = intervals.size(), count = 0; 
        sort(intervals.begin(), intervals.end(), BeginCompare);
        int rightEnd = intervals[0][1];
        for (int i = 1; i < length; i++){
            if (rightEnd > intervals[i][0]){
                count++;
                if (intervals[i][1] < rightEnd)
                    rightEnd = intervals[i][1];
            }
            else
                rightEnd = intervals[i][1];
        }
      return count;
    }
};
```

## Merge Intervals

https://leetcode.com/problems/merge-intervals/

```C++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.size() == 0 || intervals.size() == 1) return intervals;
        sort(intervals.begin(), intervals.end());         
		vector<vector<int>> res;		
        res.push_back(intervals[0]);
        for (auto i : intervals) {
            vector<int>& cur = res.back();
            if (cur[1] >= i[0]) {
                cur = {cur[0], max(i[1], cur[1])};
            } else {
                res.push_back(i); 
            }
        }
        return res;
    }
};
```

## Insert Interval

https://leetcode.com/problems/insert-interval/

```C++
class Solution {
public:
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> res;
        for(auto i : intervals){
            if(i[0] < newInterval[0]) res.push_back(i);
            else break;
        }
        if(!res.size() || res.back()[1] < newInterval[0]) res.push_back(newInterval);
        else if(res.back()[1] >= newInterval[0])
            res.back()[1] = res.back()[1] > newInterval[1] ? res.back()[1] : newInterval[1];
        for(auto i : intervals){
            if(res.back()[1] < i[0])  res.push_back(i);
            else res.back()[1] = res.back()[1] > i[1] ? res.back()[1] : i[1];
        }
        return res;
    }
};

};
```
