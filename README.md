# Queue Reconstruction by height
## https://leetcode.com/problems/queue-reconstruction-by-height

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers `(h, k)`, where h is the height of the person and k is the number of people in front of this person who have a height greater than or equal to h. Write an algorithm to reconstruct the queue.

**Note: The number of people is less than 1,100.**

``` 
Example

Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

## Approach :
1. First sort the input array `people` in such a way that, persons are sorted in `descending order` of their height, and if multiple persons have same height, then they will be sorted in `ascending order` of index k. So input array `[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]` will become `[[7,0], [7,1], [6,1], [5,0], [5,2], [4,4]]`

2. Next iterate over the sorted array `people` and add the person `people[i]` at index `people[i][1]` of the list `result`, this solves the problem automagically.
```
Lets see an e.g.

Input array : `[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]`
After sorting : `[[7,0], [7,1], [6,1], [5,0], [5,2], [4,4]]`

Next lets iterate over sorted array and add people[i] at index people[i][1] of list `result`
result => [[7,0]]
result => [[7,0], [7,1]]
result => [[7,0], [6,1], [7,1]]
result => [[5,0], [7,0], [6,1], [7,1]]
result => [[5,0], [7,0], [5,2], [6,1], [7,1]]
result => [[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```
# Implementation :
```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        if(people == null || people.length <= 1)
            return people;
        
        // We sort the array based on descending order of height
        // If two persons have same height, we sort in increasing order of index k
        Arrays.sort(people, (person1, person2) -> {
           if(person1[0] != person2[0])
               return person2[0] - person1[0];
           else
               return person1[1] - person2[1];
        });
        
        List<int[]> result = new ArrayList<>();
        for(int[] person : people) {
            result.add(person[1], person);
        }
        
        return result.toArray(new int[people.length][]);
    }
}
```

### Complexity Analysis

**Time complexity : O(N^2)**
To sort people takes O(NlogN) time. Then one proceeds to n insert operations, and each takes up to O(k) time, where k is a current number of elements in the list. In total, one needs up to O(N^2) time for insertion.

**Space complexity : O(N) to keep the result.**

# References ;
1. https://leetcode.com/articles/queue-reconstruction-by-height
2. https://evelynn.gitbooks.io/google-interview/queue-reconstruction-by-height.html
