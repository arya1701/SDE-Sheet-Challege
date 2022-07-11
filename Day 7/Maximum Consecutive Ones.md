### Given a binary array 'ARR' of size 'N', your task is to find the longest sequence of continuous 1’s that can be formed by replacing at-most 'K' zeroes by ones.
Return the length of this longest sequence of continuous 1’s.

## Approach 1:

```C++
int longestSubSeg(vector<int> &arr , int n, int k){
    // Write your code here.
   
        
    int countZeros = 0;
    int j = -1;
    int ans = 0;
    for(int i = 0; i<n; i++){
        
        if(arr[i] == 0)
            countZeros++;
        
        while(countZeros > k){
            j++;
            
            if(arr[j] == 0)
                countZeros --;
        }
    int len = i - j;
    if(len > ans)
        ans = len;
    }
    return ans;
}
```

Time - o(n) </br>
Space - o(1)
