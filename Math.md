# Fibonacci Number
+ [Recursive](#recursive)
+ [Recursive with Memo](#recursive-with-memo)
+ [Iterative](#iterative)

# Math
+ [Count Primes](#count-primes)

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

## Count Primes

https://leetcode.com/problems/count-primes/

```C++
class Solution {
 public:
  int countPrimes(int n) {
    if (n <= 2) return 0;
	vector<bool> passed(n, false);
	int sum = 1, upper = sqrt(n);
	for (int i = 3; i < n; i += 2) {
	  if (!passed[i]) {
	    sum++;
		if (i > upper) continue;
		for (int j = i * i; j < n; j += i) 
		  passed[j] = true;
	  }
	}
	return sum;
  }
};
```
