### This problem is the extension of Majority element.

### Approach 1: Optimal - Boyers Moore Algorith, extension of Moore's algo.


```c++
#include <bits/stdc++.h> 
vector<int> majorityElementII(vector<int> &arr)
{
    // Write your code here.
    int ele1 = -1;
    int ele2 = -1;
    int c1 = 0;
    int c2 = 0;
    
    for(int i = 0; i<arr.size(); i++){
        
        if(arr[i] == ele1)
            c1++;
        else if(arr[i] == ele2)
            c2++;
        
        else if(c1 == 0){
            ele1 = arr[i];
            c1 = 1;
        }else if(c2== 0){
            ele2 = arr[i];
            c2 = 1;
        }
        else{
            c1--;
            c2--;
        }
    }
    c1 = 0;c2 = 0;
    for(int i = 0; i<arr.size(); i++){
        if(arr[i] == ele1)
            c1++;
        if(arr[i] == ele2)
            c2++;
    }
    vector<int> res;
    if(c1 > arr.size()/3)
        res.push_back(ele1);
    if(c2 > arr.size()/3)
        res.push_back(ele2);
    return res;

}
```
Intuition: At max there can be two majority elements, minimum can be 0. Basically we are just keep track of these two elements using four variable ele1, ele2, c1 
and c2. Whenever c1 becomes 0 that means we are changing ele1 and when c2 becomes 0, changing ele2. 
 For a more detailed explanation, please watch the video below.


Time - o(N) </br>
Space - o(1)

