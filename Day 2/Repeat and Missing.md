## Find the duplicate and missing number.

### Approach 1: Using couting sort -

1. Take the freq array and maintain the count of every number.
2. If count of any number is zero that means that number is missing
3. If count of any number is greater than 1, means it is duplicate.

```c++
vector<int> freq(n+1,0);
    pair<int,int> res;
    for(int i = 0; i<n; i++)
        freq[arr[i]] ++;
 
    for(int i = 1; i<freq.size(); i++){
        if(freq[i] == 0) // missing no
            res.first = i;
        if(freq[i] > 1)
            res.second = i;
    }
    return res;
```

Time - o(N) + o(N) - traversing the array twice || 
space - o(N)
