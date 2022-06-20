### Find the x power n.

### Approach 1: Brute force

Using loop from 1 to N, multiply the number every times.

```c++
for (int i = 0; i < n; i++) {
        ans = ans * x;
      }
```
Time - o(N)
space - o(1)

### Approach 2:

If n is negative i.e x<sup> -n</sup> = 1/n

1. Keep on iterating until n is greater than zero, now if n is an odd power then multiply x with ans ans reduce n by 1. 
2. Else multiply x with itself and divide n by two.

```c++
// find (x^n) % m
#include <bits/stdc++.h> 
int modularExponentiation(int x, int n, int m) {
	// Write your code here.
    
    long long temp = x; // because it's value going to destroyed so store make a duplicate
    long long res = 1;
    
    while(n > 0){
        
        // whenever the power is even
        if(n%2 == 0){
            temp = ((temp%m) * (temp%m))%m;
            n /= 2;
        }else{
            res = ((res%m) * (temp%m))%m;
            n -= 1;
        }   
    }
    return (int)res;
}
```

Time - o(logN)
space - o(1)
