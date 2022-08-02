```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> kthSmallLarge(vector<int> &arr, int n, int k)
{
	// Write your code here.
    sort(arr.begin(),arr.end());
    vector<int> ans;
    
    ans.push_back(arr[k-1]);
    ans.push_back(arr[n-k]);
    return ans;
}
```
Time - o(nlogn)

## Using heap

```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> kthSmallLarge(vector<int> &arr, int n, int k)
{
	// Write your code here.
    vector<int>ans;
    priority_queue<int,vector<int>,greater<int>> minheap;
    priority_queue<int> maxheap;
    
    for(int i = 0;i<n; i++){
        maxheap.push(arr[i]);
        minheap.push(arr[i]);
    }
    // extracting root element k times
    k = k - 1;
    while(k){
        maxheap.pop();
        minheap.pop();
        k--;
    }
    int largest = maxheap.top();
    int smallest = minheap.top();
    ans.push_back(smallest);
    ans.push_back(largest);
    return ans;
    
}
```
Time - o(n + klogn), n for building the heap, and klogn for extracting the root ele k times(logn for heapify k times)

## Using Quick Select Algorithm

Quick Select algo - It is very similar to the quick sort algo. The only difference is that in quick select we will just search for single element only whereas the quick sort algo sorts 
the entire array. Partition algo is same in both the algo.

Since we are consider only single element so don't need to consider both the side like left part and right part

```c++

```
