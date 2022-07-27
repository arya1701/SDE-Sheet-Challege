### return the nth root of the integer.

```c++

double multiply(double mid, int n){
    double ans = 1.0;
    for(int i =1;i<=n;i++)
        ans *= mid;
    return ans;
}
double findNthRootOfM(int n, int m) {
	// Write your code here.
    
    double low = 1;
    double high = m;
    double digitsPlace = 1e-8; // defines the no of digits places after decimal
    
    while((high - low) > digitsPlace){
        double mid = (low+high)/2.0;
        
        if(multiply(mid,n) < m)
            low = mid; // move left
        else
            high = mid; // move right
    }
    return low;
}
```
