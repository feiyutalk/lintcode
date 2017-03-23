# Description

![](/images/merge_k_sorted_lists.png)

***
## Aanalysis

个人感觉这道题目还是相当有难度的，按顺序合并k个链表，如果k是2，那么相当简单，如果k>2，那么就变得复杂了，我们将k个链表的头结点构造成一个最小堆，利用最小堆的性质，依次选出最小的节点，然后向下继续调整。
关于堆的总结：

+ 把堆看成有规律的数组，这种规律在于：如果当前节点的编号为i，则左孩子编号为2*i+1,右孩子编号为2*i+2.
+ 核心是写好向下调整的函数，如此题的adjustDown(heap,i)
+ 分三个步骤完成： 1. 初始化堆   2. 构造堆   3. 不断取出元素，然后向下调整堆

## Solution
```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        // write your code here
        //1. 初始化堆
        ArrayList<ListNode> heap = new ArrayList<ListNode>();
        for(ListNode node : lists){
            if(node != null)
                heap.add(node);
        }
        //2. 构建最小堆
        for(int i = heap.size()-1; i>-1; i--){
            adjustDown(heap, i);
        }
        //3. 不停取出最小值，并调整堆
        ListNode head = null;
        ListNode tail = null;
        while(heap.size()>0){
            ListNode node = new ListNode(heap.get(0).val);
            if(head == null){
                head = node;
            }else{
                tail.next = node;
            }
            tail = node;
            heap.set(0, heap.get(0).next);
            if(heap.size()>0 && heap.get(0) == null){
                ListNode temp = heap.get(0);
                heap.set(0,heap.get(heap.size()-1));
                heap.set(heap.size()-1, temp);
                heap.remove(heap.size()-1);                
            }
            if(heap.size()>0 && heap.get(0) != null){
                adjustDown(heap, 0);
            }
        }
        return head;
    }
    
    public void adjustDown(List<ListNode> heap, int i){
        while(i < heap.size()){
            int index = i;
            int left = 2*i + 1;
            int right = 2*i + 2;
            if(left<heap.size() && heap.get(left).val < heap.get(index).val){
                index = left;
            }
            if(right < heap.size() && heap.get(right).val < heap.get(index).val){
                index = right;
            }
            if(index != i){
                ListNode temp = heap.get(index);
                heap.set(index, heap.get(i));
                heap.set(i, temp);
                i = index;
            }else{
                break;
            }
        }
    }
}
```

***
enjoy life, coding now!:D