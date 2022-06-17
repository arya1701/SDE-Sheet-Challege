## Find the next permutation of the given number.

### Approach 1: Brute Force

Step 1: Find all possible permutations of elements

Step 2: Search input from all possible permutations and return the present right after it.

Time to generate all the combo - N!* N. Because there are N! orders, N size of every order.
Time - O(N!xN).

### Approach 2: Using the next_permutation() inbuilt function.
C++ provides the in-built function called next_permutation() which returns the lexicographically next greater permutation of the input.

```c++

next_permutation(arr.begin(),arr.end());

```

### Approach 3: Optimal 

```c++

#include <bits/stdc++.h> 
vector<int> nextPermutation(vector<int> &permutation, int n)
{
    // Approach
    // 1. Start traversing from the back, find the first index 
    // such that a[i] < a[i+1] ->index1
    // 2. again traversing from the back, find the index such that
    // a[i] > a[previous_find_index] -> index2
    // 3. swap(a[index1],a[index2])
    // 4 revrese(index1+1,last_pos)
    
    int index1 = -1,index2 = 0;
    
    // find the first increasing sequence breakpoint
    for(int i = n-2;i>=0;i--){
        if(permutation[i] < permutation[i+1]){    
            index1 = i;
            break;
        }
    }
    // if didn;t find any breakpoints simply reverse
    if(index1<0){
        reverse(permutation.begin(),permutation.end());
        return permutation;
    }
    else{
        // finding the point which is greater than the previously find index
        for(int i = n-1;i>=0;i--){
            index2 = i;        
            if(permutation[i] > permutation[index1]){
                break;
            }
        }
    }
    swap(permutation[index1],permutation[index2]);
    reverse(permutation.begin()+index1+1,permutation.end());
    return permutation;
}

Time - o(n)
space - o(1)
```
### Intuition
Intuition behind the algorithm lies in the dictionary order, that there will be an increasing sequence always in the permutation order.
e.g - 1 3 5 4 2 like 2 4 5
we need someone greater than {1 3} prefix , can't take {1 2}, that's why we need to replace with ele where the breakdows happen.i.e 1st step: a[i] < a[i+1]
so we can take {1 5} or {1 4} but it's better to take {1 4} i. e 2ns step: a[i] > a[index1] as we know it linearly increasing from the back so the first no which
is greater than a[index1]
so we make 1 4 .. 5 3 2 now need to take only right half . To make the next permutation what we can do (try to make as lesser as possible) so write them in the 
sorted order(means reverse them) ie. 4th Step
