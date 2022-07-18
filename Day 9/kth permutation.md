## The set [1, 2, 3, ..., n] contains a total of n! unique permutations. Given n and k, return the kth permutation sequence.

### Approach 1: Brute force

Use recursion to generate all the permutation -> sort -> return the (k-1)th permutaion


Time - O(N! * N) +O(N! Log N!), recursion takes O(N!)  time because we generate every possible permutation, O(N) for putting into the ds. Also, O(N! Log N!)  time required to sort the data structure

Space - O(N) 

### Approach 2: Optimal

