## Merge two sorted array

### Approach 1: Brute force

1. Take a temp array of size n + m.
2. Iterated over array1, put all the elements into the temp array.
3. Similarly for array2.
4. Sort that temp array.
5. Put starting n elements to array1 and m elements to array2.

Time complexity: O(n*log(n))+O(n)+O(n)

Space Complexity: O(n) 

### Approach 2: Better - wothout using extra space

Intuition - Since our both array are sorted, we have to apply some logic that will use of that sorted order. 

Start iterating over the array1 and if we elements which is greater than the current elements so we can swap it. And our algo based on the fact that both the array
should be sorted so rearrarge the array2. And when iteration of array1 is complete, we'll have our answer.

Example: 
INPUT - array1 = 1 4 7 8 10 , array2 = 2 3 9

OUTPUT - array1 = 1 2 3 4 7 array2 = 8 9 10
```c++
for(int i = 0; i< arr1.size(); i++){
        
        if(arr1[i] > arr2[0])
            swap(arr1[i],arr2[0]);
        
        // now rearrange the array2, 
        // use insertion sort technique here
        
        int temp = arr2[0];
        for(int k = 1; k<n && arr2[k] < temp; k++)
            arr2[k-1] = arr2[k];
        arr2[k-1] = temp;
    }

```  

Time - o(N*M), assume array1 have larger elements than array2, so we have to swap everytime, linear traversal take n time and to reorder takes m times

space - o(1)

### Approach 3: Gap Method

1. Initially take the gap as (m+n)/2;
2. Take as a p1 = 0 and p2 = gap.
3. Run a loop from p1 &  p2 to  m+n and whenever arr[p2]<arr[p1], just swap those.
4. After completion of the loop reduce the gap as gap=gap/2.
Repeat the process until gap>0.

Time - o(logN)
space - o(1)

