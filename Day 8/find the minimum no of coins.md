## Return the minimum no of coins required to make change.

### Approach-Greedy

- traverse from the end of the array
- Now while(V >= coins[i]) we will reduce V by coins[i] and add it to the ans array.

Observations - 
- We can ignore the denomination that is greater than V
- find the greatest among them and use the greedy method to make as much as we can 

Simple keep on subtracting till it is possible for given denomination to get combination.
```c++
int findMinimumCoins(int amount) 
{
    // Write your code here
    int count = 0;
    int coins[] = {1, 2, 5, 10, 20, 50, 100, 500, 1000};
    int i = 0, n = 9;
    
    vector<int> combination;
     for (int i = n - 1; i >= 0; i--) {
        while(amount >= coins[i]){
            amount -= coins[i];
            combination.push_back(coins[i]);
        }
     }
    return combination.size();
}

```

Time - o(V) </br>
Space - o(1)
