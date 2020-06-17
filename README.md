# Queue Reconstruction by height
## https://leetcode.com/problems/queue-reconstruction-by-height



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

# References ;
1. https://leetcode.com/articles/queue-reconstruction-by-height
2. https://evelynn.gitbooks.io/google-interview/queue-reconstruction-by-height.html
