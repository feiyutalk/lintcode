# Description

![](/images/search_range_in_binary_tree.png)

***
## Aanalysis

该题目是在一个二叉排序树中去查找一个区间，一个想法是根据二叉排序树的特点，对它进行中序遍历可以得到递增的序列，这是第一步，然后再在这个递增的序列中去判断，得到满足条件的解。还有一种想法就是递归的去得到每一个值，分类讨论如下：

root.val 小于 k1    此时左子树的所有节点将都不满足条件，只需要遍历右子树

root.val 大于 k1 && root.val 小于 k2  此时需要遍历左右子树

root.val 大于 k2    此时右子树的所有节点将都不满足条件，只需要遍历左子树 

## Solution
```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param k1 and k2: range k1 to k2.
     * @return: Return all keys that k1<=key<=k2 in ascending order.
     */
    public ArrayList<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        ArrayList<Integer> ret = new ArrayList<Integer>();
        ArrayList<Integer> ret2 = new ArrayList<Integer>();
        inorder(root, ret);
        for(int i=0; i<ret.size(); i++){
            int temp = ret.get(i);
            if(temp >= k1 && temp <= k2){
                ret2.add(temp);
            }
        }
        return ret2;
    }
    
    public void inorder(TreeNode root, ArrayList<Integer> ret){
        if(root == null){
            return ;
        }
        inorder(root.left, ret);
        ret.add(root.val);
        inorder(root.right, ret);
    }
}
```
***
enjoy life, coding now!:Deorder[i];
        }
        
        int[] inleft = new int[index];
        int[] inright = new int[preorder.length - index - 1];
        for(int i =0 ; i<index; i++){
            inleft[i] = inorder[i];
        }
        for(int i = index+1; i<inorder.length; i++){
            inright[i - index - 1] = inorder[i];
        }
        
        TreeNode root = new TreeNode(rootval);
        root.left = buildTree(preleft, inleft);
        root.right = buildTree(preright, inright);
        return root;
    }
}
```

***
enjoy life, coding now!:D