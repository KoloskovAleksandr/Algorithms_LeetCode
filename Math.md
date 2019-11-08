# Fibonacci Number
+ [Recursive](#recursive)
+ [Recursive with Memo](#recursive-with-memo)
+ [Iterative](#iterative)

## Recursive
```C++
class Solution {
public:
    int fib(int N) {
        if (N <= 1)
            return N;
        else
            return fib(N - 1) + fib(N - 2);
    }
};
```
## Recursive with Memo
```C++
class Solution {
public:
    int fib(int N) {
        if (N <= 1)
            return N;
        int memo[N + 1] = {0, 1};
        return fib(N, memo);        
    }
    int fib(int N, int* memo){
        if (N <= 1)
            return N;
        if (!memo[N])
            memo[N]= fib(N - 1, memo) + fib(N - 2, memo);
        return memo[N];
    }
};
```
## Iterative
```C++
class Solution {
public:
    int fib(int N) {
        if (N <= 1)
            return N;
        int first = 0, second = 1, cur;
        while (N >= 2) {
            cur = first + second;
            first = second;
            second = cur;
            N--;
        }
        return cur;
    }
};
```
