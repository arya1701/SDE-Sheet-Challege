## Maximize the profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

### Approach 1: Brute force

1. Using two loops, 
2. 1st loop -> of ‘i’ from 0 to n.
3. 2nd loop -> of 'j' from ‘i+1’ to n.
4. If arr[j] > arr[i] , take the difference and compare  and store it in the maxPro variable.
5. Return maxPro.

```c++
for(int i = 0; i<n; i++){
  for(int j = i+1; j<n; j++){
    if(arr[j] > arr[i]){
      max_profit = max(max_profit, arr[j]- arr[i])
      }
  }
}
return mxa_profit;
    
```
Time - o(N^2)

Space - o(1)

### Approach 1: Optimal

Maximize the profit means - Buy at min price and try to sell at max so that we can get max profit.

Linearly iterating over the array and find the minimum_price and compare it with the max_profit and difference of CurrentPrice and minimum_price.
After completing the iteration return the max_profit.


```c++

int max_profit = 0;
int min_price = INT_MAX;
for(int i =0;i<prices.size();i++){
  min_price = min(min_price,prices[i]);
  max_profit = max(max_profit, prices[i] - min_price);
}
return max_profit;

```
Time - o(N)
space - O(1)
