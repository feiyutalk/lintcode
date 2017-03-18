# Description

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.


Clarification

Your algorithm should run in O(n) complexity.

Example

Given [100, 4, 200, 1, 3, 2],

The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

## Analysis
这道题目求最长连续序列，思路就是取出一个元素，记为temp,然后求temp+1是否在集合中，如果在集合中，把计数器+1，然后temp+2是否在集合中,遇到不在的就不继续往前推进，对称思想，temp-1也是类似的。注意，每遍历到一个元素，就应该把该元素从集合中删除。还有有点很重要，由于时间复杂度要求是O(n)的，这要求我们在循环内的操作时间复杂度都要求是O(1)。很明显，循环内我们肯定有collection.contains(temp+1)的操作，该操作必须是O(1)时间复杂度的，所以我们的集合必须用HashSet或者HashMap，我这里采用的是HashSet，代码如下：

## Solution
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return an integer
     */
    public int longestConsecutive(int[] num) {
        // write you code here
        Set<Integer> numbers = new HashSet<Integer>();
        for(int i=0; i<num.length; i++){
                numbers.add(num[i]);
        }
        int count = 0;
        int ret = 0;
        
        while(numbers.size()>0){
            int temp = numbers.iterator().next();
            numbers.remove(new Integer(temp));
            count = 1;
            int high = temp+1;
            while(numbers.size()>0){
                if(numbers.contains(high)){
                    count++;
                    numbers.remove(new Integer(temp));
                    high++;
                }else{
                    break;
                }
            }
            int low = temp - 1;
            while(numbers.size()>0){
                if(numbers.contains(low)){
                    count++;
                    numbers.remove(new Integer(temp));
                    low--;
                }else{
                    break;
                }
            }
            if(ret < count){
                ret = count;
            }
        }
        return ret;
    }
}
```

***
enjoy life, coding now!:D

