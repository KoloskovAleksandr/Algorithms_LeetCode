# Dynamic programming

+ [Knapsack problem](#knapsack-problem)
+ [Climbing Stairs](#climbing-stairs)
+ [Longest Increasing Subsequence](#longest-increasing-subsequence)
+ [Coin Change](#coin-change)
+ [Coin Change 2](#coin-change-2)
+ [House Robber](#house-robber)
+ [House Robber II](#house-robber-ii)
+ [Jump Game](#jump-game)
+ [Jump Game II](#jump-game-ii)
+ [Decode Ways](#decode-ways)
+ [Unique Paths](#unique-paths)
+ [Unique Paths II](#unique-paths-ii)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Word Break](#word-break)
+ [N-Queens](#n-queens)
+ [N-Queens II](#n-queens-ii)

## Knapsack problem

https://stepik.org/lesson/13259/step/5?unit=3444

```C++
int main() {
  int capacity, n;
  cin >> capacity >> n;
  vector<vector<int>> maxValue(n + 1, vector<int>(capacity + 1));
  for (int i = 1; i <= n; i++) {
    int num;
    cin >> num;
    for (int j = 1; j <= capacity; j++) {
      if (num > j)
        maxValue[i][j] = maxValue[i - 1][j];
      else
        maxValue[i][j] = max(maxValue[i - 1][j], maxValue[i - 1][j - num] + num);
    }
  }
  cout << maxValue[n][capacity];
  return 0;
}
```

## Climbing Stairs

https://leetcode.com/problems/climbing-stairs/

```C++
class Solution {
public:
    int climbStairs(int n) {
        int first = 0, second = 1;
        while(n--){
            second = first + second;
            first = second - first;
        }
        return second;          
    }
};
```

## Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/

```C++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) 
            return 0;

        vector<int> steps(n);
        steps[0] = 1;
        int maxans = 1;
        for (int i = 1; i < n; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++) 
                if (nums[i] > nums[j]) 
                    maxval = max(maxval, steps[j]);
            steps[i] = maxval + 1;
            maxans = max(maxans, steps[i]);
        }
        return maxans;        
    }
};
```

## Coin Change

https://leetcode.com/problems/coin-change/

```C++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> mins(amount + 1, amount + 1);
        mins[0] = 0;
        for (int i = 1; i <= amount; i++)
            for (int j = 0, length = coins.size(); j < length; j++)
                if (coins[j] <= i) 
                    mins[i] = min(mins[i], mins[i - coins[j]] + 1);
        return mins.back() > amount ? -1 : mins.back();        
    }
};
```

## Coin Change 2

https://leetcode.com/problems/coin-change-2/

```C++
class Solution {
public:
    int change(int amount, vector<int>& coins){
        vector<int> num(amount + 1);
        num[0] = 1;
        for (int i = 0, length = coins.size(); i < length; i++)
            for (int j = coins[i]; j <= amount; j++)
                num[j] += num[j - coins[i]];
        return num.back();        
    }
};
```

## House Robber

https://leetcode.com/problems/house-robber/

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size(), pre = 0, cur = 0;
        for (int i = 0; i < n; i++) {
            int temp = max(pre + nums[i], cur);
            pre = cur;
            cur = temp;
        }
        return cur;        
    }
};
```

## House Robber II

https://leetcode.com/problems/house-robber-ii/

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1)  return nums[0];
        return max(DPRob(nums, 0, nums.size() - 1), DPRob(nums, 1, nums.size()));
    }
    int DPRob(vector<int>& nums, int begin, int end) {
        int cur = 0, prev = 0;
        for (int i = begin; i < end; i++) {
            int tmp = max(prev + nums[i], cur);
            prev = cur;
            cur = tmp;
        }
        return cur;
    }
};
```

## Jump Game

https://leetcode.com/problems/jump-game/

```C++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int lastPos = nums.size() - 1;
        for (int i = lastPos; i >= 0; i--) 
            if (i + nums[i] >= lastPos) 
                lastPos = i;
        return lastPos == 0;        
    }
};
```

## Jump Game II

https://leetcode.com/problems/jump-game-ii/

```C++
class Solution {
public:
    int jump(vector<int>& nums) {
        int res = 0, curpos = 0, jump = 0;
        for (int i = 0, n = nums.size() - 1; i < n; i++) {     
            jump = max(jump, i + nums[i]);
            if (i == curpos) {
                curpos = jump;
                res++;                
            }
        }
      return res;        
    }
};
```

## Decode Ways

https://leetcode.com/problems/decode-ways/

```C++
class Solution {
public:
    int numDecodings(string s) {
        int prev = 0, cur = 1;
        for (int i = 0, n = s.length(); i < n; i++) {  
            if (s[i] == '0')
                cur = 0;
            int tmp = cur + prev;        
            if (s[i] == '1' || s[i] == '2' && s[i + 1] <= '6')  
                prev = cur;         
            else
                prev = 0;
            cur = tmp;
        }
        return cur;        
    }
};
```

## Unique Paths

https://leetcode.com/problems/unique-paths/

```C++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> steps(n, 1);
        for (int i = 1; i < m; i++)
            for (int j = 1; j < n; j++) 
                steps[j] += steps[j - 1];
        return steps[n - 1];        
    }
};
```

## Unique Paths II

https://leetcode.com/problems/unique-paths-ii/

```C++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if (obstacleGrid[0][0] == 1)
            return 0;
        int m = obstacleGrid.size(), n = obstacleGrid[0].size();
        vector<long> steps(n);
        steps[0] = 1;
        for (int i = 0 ; i < m; i++)
            for (int j = 0 ; j < n; j++) {
            if (!obstacleGrid[i][j]) {
                if (j)
                steps[j] += steps[j - 1];
            } else
                steps[j] = 0;
        }
        return steps[n - 1];        
    }
};
```

## Longest Common Subsequence

https://leetcode.com/problems/longest-common-subsequence/

```C++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<vector<int>> sub(text1.length() + 1, vector<int>(text2.length() + 1));
        for (int i = 0, n = text1.length(); i < n; i++)
            for (int j = 0, m = text2.length(); j < m; j++) {
                if (text1[i] == text2[j])
                    sub[i + 1][j + 1] = 1 + sub[i][j];
                else
                    sub[i + 1][j + 1] = max(sub[i + 1][j], sub[i][j + 1]);
      }
    return sub.back().back();        
    }
};
```

## Word Break

https://leetcode.com/problems/word-break/

```C++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.size();        
        set<string> dict;
        for(auto w : wordDict)
            dict.insert(w);        
        vector<bool> dp(n + 1, false);
        dp[0] = true; 

        for(int i = 0; i < n; i++)
            for(int j = i; j >= 0; j--)
            {
                string curr = s.substr(j, i - j + 1);
                if(dict.find(curr) != dict.end())
                    dp[i + 1] = dp[i + 1] || dp[j];                
                if(dp[i + 1])
                    break;
            }        
        return dp[n];
    }      
};
```

## N-Queens

https://leetcode.com/problems/n-queens/

```C++
class Solution {
public:
    vector<vector<string>> solveNQueens(int n){
        vector<vector<string> > res;
	    vector<string> temp(n, string(n,'.'));
	    int dp[n];
	    helper(res, temp, dp, 0, n);
	    return res;    
    }    
    void helper(vector<vector<string>> &res, vector<string> &temp, int dp[], int row, int n){
	    if(row == n){
    		res.push_back(temp);
    		return;
    	}
    	for(int col = 0; col < n; ++col){
    		if(valid(dp, row, col, n)){
    			dp[row] = col;
    			temp[row][col] = 'Q';
    			helper(res, temp, dp, row + 1,n);
    			temp[row][col]='.';
    		}
    	}
    }
    bool valid(int dp[], int row, int col, int n){
    	for(int i = 0;i < row; ++i){
	    	if(dp[i] == col || abs(row - i) == abs(dp[i] - col))
    			return false;
    	}
    	return true;
    }
};

```

## N-Queens II

https://leetcode.com/problems/n-queens-ii/

```C++
class Solution {
public:
    int totalNQueens(int n) {
        int res = 0;
	    vector<string> temp(n, string(n,'.'));
	    int dp[n];
	    helper(res, temp, dp, 0, n);
	    return res;    
    }  
    void helper(int &res, vector<string> &temp, int dp[], int row, int n){
	    if(row == n){
    		res++;
    		return;
    	}
    	for(int col = 0; col < n; ++col){
    		if(valid(dp, row, col, n)){
    			dp[row] = col;
    			temp[row][col] = 'Q';
    			helper(res, temp, dp, row + 1,n);
    			temp[row][col]='.';
    		}
    	}
    }
    bool valid(int dp[], int row, int col, int n){
    	for(int i = 0;i < row; ++i){
	    	if(dp[i] == col || abs(row - i) == abs(dp[i] - col))
    			return false;
    	}
    	return true;
    }        
};
```
