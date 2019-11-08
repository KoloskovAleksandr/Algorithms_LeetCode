# Topological sort

+ [Course Schedule](#course-schedule)
+ [Course Schedule II](#course-schedule-ii)
+ [Alien Dictionary](#alien-dictionary)

## Course Schedule

https://leetcode.com/problems/course-schedule/

```C++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses, vector<int>());
        vector<int> answer;
        vector<char> color(numCourses);

        for(auto edge : prerequisites)
            graph[edge[1]].push_back(edge[0]);         
        for(int i = 0; i < numCourses; i++)
            if(!TopologicalSort(graph, i, color, answer))
               return false;
        return true;        
    }
    bool TopologicalSort(vector<vector<int>>& graph, int i, vector<char>& color, vector<int>& answer){
        if(color[i] == 'B')
            return true;
        if(color[i] == 'G')
            return false;
        color[i] = 'G';
        for(auto depth : graph[i])
             if(!TopologicalSort(graph, depth, color, answer))
                return false;            
        
        color[i] = 'B';
        answer.push_back(i);
        return true;
    }        
};                          
```

## Course Schedule II

https://leetcode.com/problems/course-schedule-ii/submissions/

```C++
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses, vector<int>());
        vector<int> answer;
        vector<char> color(numCourses);
        
        for(auto edge : prerequisites)
            graph[edge[1]].push_back(edge[0]);         
        for(int i = 0; i < numCourses; i++)
            if(!TopologicalSort(graph, i, color, answer))
               return {};
        
        reverse(answer.begin(), answer.end());
        return answer;        
    }
    bool TopologicalSort(vector<vector<int>>& graph, int i, vector<char>& color, vector<int>& answer){
        if(color[i] == 'B')
            return true;
        if(color[i] == 'G')
            return false;
        color[i] = 'G';
        for(auto depth : graph[i])
             if(!TopologicalSort(graph, depth, color, answer))
                return false;            
        
        color[i] = 'B';
        answer.push_back(i);
        return true;
    }        
};
```

## Alien Dictionary

https://www.lintcode.com/problem/alien-dictionary/description

```C++
class Solution {
public:
    string alienOrder(vector<string> &words) {
        unordered_map<char, set<char>> outbound;
        unordered_map<char, set<char>> inbound;  
        set<char> no_pre;  
        string s = ""; 
        int wordsSize = words.size();
        for(int i = 0; i < wordsSize; i++) {
            string t = words[i]; 
            no_pre.insert(t.begin(), t.end()); 
            int length = min(s.size(), t.size());
            for(int j = 0; j < length; j++) {
                if(t[j] != s[j]) {
                    inbound[t[j]].insert(s[j]);
                    outbound[s[j]].insert(t[j]);  
                    break;  
                }  
            }
            s = t;
        }
        string result = "";
        for(auto i : no_pre)
            result += i;
        return result;
    }
};
```
