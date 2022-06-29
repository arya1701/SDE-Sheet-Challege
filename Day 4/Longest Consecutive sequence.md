### Given an array of ‘N’ integers. Find the length of the longest sequence which contains the consecutive elements.

### Approach 1: Brute force

Sort the arrya and run a for loop to find the longest consecutive sequence.

Time - o(N*logN) + O(N) </br>
Space - o(1)

### Approach 2: Optimal - using hash set

- Insert all the elements into the hash set
- linearly iterate over the array and check, (currentNo - 1) exist in the hash set or not
- If exist - do nothing
- else check for (currentNo + 1) untill exist and count the length.

Reason for checking the (currentNo - 1) exists or not is that, we means to start with the minimal no, if we have a sequence and start with a minimal no
that we did not want (currentNo - 1) because we are starting with the minimal no.

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
 Space - O(N)
