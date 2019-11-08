# Arrays

+ [Two Sum](#two-sum)
+ [3Sum](#3sum)
+ [Subarray Sum Equals K](#subarray-sum-equals-k)

## Two Sum

https://leetcode.com/problems/two-sum/

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> data;
        vector<int> result;
        for (int i = 0; i < nums.size(); i++) {
            int complement = target - nums[i];
            if (data.find(complement) != data.end()) {
                result.push_back(data[complement]);
                result.push_back(i);            
                return result;
            }
            data[nums[i]] =  i;
        }
        return vector<int> (0);        
    }
};
```

## 3Sum

https://leetcode.com/problems/3sum/

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> answ;
        int length = nums.size() - 1;
        int a, b, c, target;
        sort(nums.begin(), nums.end());        
        for(a = 0; a <= length; a++){
            target = -nums[a];
            if(target < 0) break;
            b = a + 1;
            c = length;
            
            while(b < c){
                int twoSum = nums[b] + nums[c];
                if(twoSum < target)
                    while(b < c && nums[++b] == nums[b - 1]);
                else if(twoSum > target)
                    while(b < c && nums[--c] == nums[c + 1]);               
                else{
                    answ.push_back({-target, nums[b], nums[c]});
                    while(b < c && nums[++b] == nums[b - 1]);
                    while(b < c && nums[--c] == nums[c + 1]);                    
                    }
            }
            while (a < length && nums[a] == nums[a + 1]) a++;           
        } 
        return answ;
    }
};
```

## Subarray Sum Equals K

https://leetcode.com/problems/subarray-sum-equals-k/

```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int count = 0, sum = 0, length = nums.size();
        map<int, int> data;
        data[0]++;
        for (int i = 0; i < length; i++) {
            sum += nums[i];
            if (data.count(sum - k))
                count += data[sum - k];
            data[sum]++;            
        }
        return count;
    }
};
```
