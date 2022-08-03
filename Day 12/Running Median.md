### Leetcode 295
```c++
class MedianFinder {
public:
    
    // for storing the low number
    priority_queue<int> maxheap;
    
    // for storing the high number
    priority_queue<int, vector<int>, greater<int>> minheap;
    
    // we are consifering the maxheap will have 1 more elements the minheap
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        
        maxheap.push(num);
        minheap.push(maxheap.top());
        maxheap.pop();
        
        if(minheap.size() > maxheap.size()){
            maxheap.push(minheap.top());
            minheap.pop();
        }
    }
    
    double findMedian() {
        if(maxheap.size() > minheap.size())
            return maxheap.top();
        else
            return (maxheap.top() + minheap.top())/2.0;
    }
};

```
