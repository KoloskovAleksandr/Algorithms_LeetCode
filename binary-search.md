# Binary search

+ [Binary Search](#binary-search)
+ [Find Minimum in Rotated Sorted Array](#find-minimum-in-rotated-sorted-array)
+ [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)

## Binary Search

https://leetcode.com/problems/binary-search/

```C++
class Solution {
 public:
  int search(vector<int>& nums, int target) {
    int pivot, left = 0, right = nums.size() - 1;
    while (left <= right) {
      pivot = left + (right - left) / 2;
      if (nums[pivot] == target) return pivot;
      if (target < nums[pivot]) right = pivot - 1;
      else left = pivot + 1;
    }
    return -1;
  }
};
```

## Find Minimum in Rotated Sorted Array

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

```C++
class Solution {
 public:
  int findMin(vector<int>& nums) {
    int left = 0, right = nums.size() - 1; 
    if (!right || nums[right] > nums[0])  return nums[0]; 
    while (right >= left){
      int mid = left + (right - left) / 2;
      if (nums[mid] > nums[mid + 1]) return nums[mid + 1];    
      if (nums[mid - 1] > nums[mid]) return nums[mid];
      if (nums[mid] > nums[0]) 
        left = mid + 1;
      else
        right = mid - 1;       
    }
    return -1;
  }
};
```

## Search in Rotated Sorted Array

https://leetcode.com/problems/search-in-rotated-sorted-array/

```C++
class Solution {
 public:
  int search(vector<int>& nums, int target) {
    int low = 0, high = int(nums.size()) - 1;
    while (low < high) {
      int mid = (low + high) / 2;
      if ((nums[0] > target) ^ (nums[0] > nums[mid]) ^ (target > nums[mid]))
        low = mid + 1;
      else
        high = mid;
    }
    return low == high && nums[low] == target ? low : -1;
  }
};
```
