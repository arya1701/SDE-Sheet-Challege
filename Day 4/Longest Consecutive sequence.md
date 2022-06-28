### Given an array of ‘N’ integers. Find the length of the longest sequence which contains the consecutive elements.

### Approach 1: Brute force

Sort the arrya and run a for loop to find the longest consecutive sequence.

Time - o(N*logN) </br>
Space - o(1)

### Approach 2: Optimal - using hash set

 ```c++
 #include <bits/stdc++.h> 
int lengthOfLongestConsecutiveSequence(vector<int> &arr, int n) {
    // Write your code here.
    
    unordered_set<int> hs;
    for(auto i:arr)
        hs.insert(i);
    int curr = 0;
    int ans = 0;
    for(int i = 0; i<n; i++){
        if(hs.find(arr[i]-1) != hs.end())
            continue;
        else{
            // if not contain in the hash set
            int curr = arr[i];
            int currentStreak = 1;
            while(hs.find(curr + 1) != hs.end()){
                curr += 1;
                currentStreak += 1;
            }
            ans = max(ans, currentStreak);
        }
    }
    return ans;
}
 ```
 
 Time - o(N) </br>
 Space - O(1)
