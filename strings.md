# Strings

+ [Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
+ [Generate Parentheses](#generate-parentheses)
+ [Is Subsequence](#is-subsequence)
+ [Valid Palindrome](#valid-palindrome)
+ [Longest Palindromic Substring](#longest-palindromic-substring)
+ [Palindromic Substrings](#palindromic-substrings)
+ [Valid Parentheses](#valid-parentheses)
+ [Group Anagrams](#group-anagrams)
+ [Longest Repeating Character Replacement](#longest-repeating-character-replacement)
+ [Minimum Window Substring](#minimum-window-substring)

## Longest Substring Without Repeating Characters

https://leetcode.com/problems/longest-substring-without-repeating-characters/

```C++
class Solution {
 public:
  int lengthOfLongestSubstring(string s) {
    vector<int> table(256, 0);
    int maxstr = 0, track = 0, n = s.length();
    for(int i = 0; i < n; i++) {
      while(table[s[i]])
        table[s[track++]] = 0;
      table[s[i]] = 1;
      maxstr = max(maxstr, i - track + 1);        
    }
    return maxstr;          
  }
};
```

## Generate Parentheses

https://leetcode.com/problems/generate-parentheses/

```C++
class Solution {
 public:
  vector<string> generateParenthesis(int n) {
    vector<string> res;
    addingpar(res, "", n, 0);
    return res;
  }
  void addingpar(vector<string> &v, string str, int n, int m){
    if(n==0 && m==0) {
      v.push_back(str);
      return;
    }
    if(m > 0)
      addingpar(v, str + ")", n, m-1); 
    if(n > 0)
      addingpar(v, str + "(", n-1, m+1); 
  }
};
```

## Is Subsequence

https://leetcode.com/problems/is-subsequence/

```C++
class Solution {
 public:
  bool isSubsequence(string s, string t) {
    int i = 0, j = 0, n = s.length(), m = t.length();
    if (m < n) return false;
    while (i < n && j < m)  {
      if (s[i] == t[j])
        ++i;
      ++j;
    }
    return i == n;
  }
};
```

## Valid Palindrome

https://leetcode.com/problems/valid-palindrome/

```C++
class Solution {
 public:
  bool isPalindrome(string s) {
    for (int i = 0, j = s.size() - 1; i < j; i++, j--) { 
      while (isalnum(s[i]) == false && i < j) i++; 
      while (isalnum(s[j]) == false && i < j) j--; 
      if (toupper(s[i]) != toupper(s[j])) return false;
    }    
    return true;
  }
};
```

## Longest Palindromic Substring

https://leetcode.com/problems/longest-palindromic-substring/

```C++
class Solution {
 public:
  string longestPalindrome(string s) {
    const int size_s = s.size();
    int max_s = 0, max_l = 0;
    for (int i = 0; i < size_s;) {
      int start = i, end = i;
      while (end + 1 < size_s && s[end] == s[end + 1]) end++;
      i = end + 1;
      while (start - 1 >= 0 && end + 1 < size_s && s[start - 1] == s[end + 1]) {
        start--;
        end++;
      }
      if (end - start + 1 > max_l) {
        max_l = end - start + 1;
       max_s = start;
      }
    }
    return s.substr(max_s, max_l);
  }
};
```

## Palindromic Substrings

https://leetcode.com/problems/palindromic-substrings/

```C++
class Solution {
 public:
  int countSubstrings(string s) {
    int n = s.length(), ans = 0;
    for (int center = 0; center <= 2 * n - 1; ++center) {
      int left = center / 2;
      int right = left + center % 2;
      while (left >= 0 && right < n && s[left] == s[right]) {
        ans++;
        left--;
        right++;
      }
    }
    return ans;
  }
};
```


## Valid Parentheses

https://leetcode.com/problems/valid-parentheses/

```C++
class Solution {
 public:
  bool isValid(string s) {
    stack<int> parent;
    for (int i = 0; i < s.size(); i++) {
      switch (s[i]) {
        case '(':
          parent.push(')');
          break;
        case '[':
          parent.push(']');
          break;
        case '{':
          parent.push('}');
          break;
        default:
          if (parent.empty() || parent.top() != s[i]) return false;
          parent.pop();
      }
    }
    return parent.empty();
  }
};
```

## Group Anagrams

https://leetcode.com/problems/group-anagrams/

```C++
class Solution {
 private:
  string strSort(string s) {
    int counter[26] = {0};
    for (char c : s)
      counter[c - 'a']++;
    string t;
    for (int c = 0; c < 26; c++)
      t += string(counter[c], c + 'a');
    return t;
  }
 public:
  vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> map;
    for (string s : strs)
      map[strSort(s)].push_back(s);
    vector<vector<string>> anagrams;
    for (auto p : map) 
      anagrams.push_back(p.second);
    return anagrams;
  }
};
  ```
  
## Longest Repeating Character Replacement

https://leetcode.com/problems/longest-repeating-character-replacement/

```C++
class Solution {
 public:
  int characterReplacement(string s, int k) {
    vector<int> counts(26, 0);
    int start = 0, maxCharCount = 0, n = s.length(), result = 0;
    for(int end = 0; end < n; end++){
      counts[s[end]-'A']++;
      if(maxCharCount < counts[s[end] - 'A'])
        maxCharCount = counts[s[end] - 'A'];
      while(end - start - maxCharCount + 1 > k){
        counts[s[start]-'A']--;
        start++;
        for(int i = 0; i < 26; i++)
          if(maxCharCount < counts[i])
        maxCharCount = counts[i];
      }
      result = max(result, end - start + 1);
    }
    return result;  
  }
};
```

## Minimum Window Substring

https://leetcode.com/problems/minimum-window-substring/

```C++
class Solution {
 public:
  string minWindow(string s, string t) {
    vector<int> map(128,0);
    for(auto c : t) map[c]++;
    int counter = t.size(), begin = 0, end = 0, d = INT_MAX, head = 0;
    while(end < s.size()){
      if(map[s[end++]]-- > 0) counter--; 
      while(counter == 0){ 
        if(end - begin < d)  d = end - (head = begin);
        if(map[s[begin++]]++ == 0) counter++;
      }  
    }
    return d == INT_MAX ? "" : s.substr(head, d);
  }
};
```
