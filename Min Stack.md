# Description

Implement a stack with min() function, which will return the smallest number in the stack.

It should support push, pop and min operation all in O(1) cost.

>>>

Notice

min operation will never be called if there is no number in the stack.

>>>

***
## Analysis
本题需要一个数据结构，该数据结构基本的操作和栈类似，但是有一个特别的地方，就是该数据结构求最小值的时间复杂度竟然是O(1)，按照常规理解，我们求最小值需要遍历一遍栈里面的元素，然后求得最小，这样的时间复杂度必须为O(n),当我们在操作上找不到时间优化的办法的时候，我们要有意识，用时空互换的方法，能意识到该方法的前提是，我们必须有这样的认识，算法其实本质上的时空平衡的艺术。所以，我们将问题转化为构造辅助数据结构，来帮助我们解决在O(1)时间内求出最小值。这里的想法是另外构造一个栈，该栈是针对**当前元素**存储最小值，其栈内元素和原栈内的元素一样多。看代码可能就懂了，并不难。

## Solution
```java
public class MinStack {
     Stack<Integer> numbers;
     Stack<Integer> mins;
    public MinStack() {
        // do initialize if necessary
       numbers = new Stack<Integer>();
        mins = new Stack<Integer>();
    }

    public void push(int number) {
        // write your code here
        numbers.push(number);
        if(mins.size()==0){
            mins.push(number);
        }else{
            if(number<mins.peek()){
                mins.push(number);
            }else{
                mins.push(mins.peek());
            }
        }
    }

    public int pop() {
        // write your code here
        mins.pop();
        return numbers.pop();
    }

    public int min() {
        // write your code here
        return mins.peek();
    }
}

```

***
enjoy life, coding now!:D
