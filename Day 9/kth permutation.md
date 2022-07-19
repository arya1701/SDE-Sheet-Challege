## The set [1, 2, 3, ..., n] contains a total of n! unique permutations. Given n and k, return the kth permutation sequence.

### Approach 1: Brute force

Use recursion to generate all the permutation -> sort -> return the (k-1)th permutaion


Time - O(N! * N) +O(N! Log N!), recursion takes O(N!)  time because we generate every possible permutation, O(N) for putting into the ds. Also, O(N! Log N!)  time required to sort the data structure

Space - O(N) 

### Approach 2: Optimal using mathematics
```c++
string kthPermutation(int n, int k) {
    // Write your code here.
    int fact = 1;
    vector<int> numbers;
    string ans = "";
    for(int i = 1; i<n; i++){
        fact *= i;
        numbers.push_back(i);
    }
    numbers.push_back(n);
    k = k - 1;
    while(true){
        ans += to_string(numbers[k/fact]);
        numbers.erase(numbers.begin()+k/fact);
        if(numbers.size() == 0)
            break;
        k = k % fact;
        fact = fact / numbers.size();
    }
    
    
    return ans;
}
```
Time - O(N) * O(N) = O(N^2), o(N) for as we are looking for n number, o(n) for erase a number </br>
Space - O(N), to store the ans in ds


