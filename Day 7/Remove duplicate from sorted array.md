## Given sorted 'ARR' of size 'N'. Return the length of this new array.

### Approach 1: Brute force

- use a HashSet
- Traverse a array and put the element into the set
- Now put all elements of the set in the array from the starting of the array.
- return the length 
```c++
int removeDuplicates(int arr[]) {
  set < int > set;
  for (int i = 0; i < arr.size(); i++) {
    set.insert(arr[i]);
  }
  int k = set.size();
  int j = 0;
  for (int x: set) {
    arr[j++] = x;
  }
  return k;
}
```
Time - o(n*logn) + o(n) </br>
Space - o(n)


### Approach 2: Using two pointer

 ```c++
 int removeDuplicates(vector<int> &arr, int n) {
	// Write your code here.
    int i = 0;
    for(int j = 1; j<n; j++){
        if(arr[i] != arr[j])
            i++;
        arr[i] = arr[j];
    }
    return i+1;
}
```
Time - o(n) </br>
Space - o(1)
