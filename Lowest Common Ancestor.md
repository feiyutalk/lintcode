# Description
Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes.

The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

>>>

Notice

Assume two nodes are exist in tree.

**Example**

   4

  / \

3    7

     / \

    5    6

LCA(3, 5) = 4

LCA(5, 6) = 7

LCA(6, 7) = 7

>>>

## Analysis
这道题目需要用到主要矛盾的思想去发现问题的特点，然后缩小解空间。那么这道题的主要矛盾是什么呢？主要矛盾是，A，B两个节点一定位于最近公共祖先的左右两端，若不然，则能找到更近的公共祖先。
据此，我们可以分别递归的求出，左子树的最近公共祖先，右子树的最近公共祖先，然后分类讨论。

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
     * @param A and B: two nodes in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        // write your code here
        if(root == null || root == A || root == B){
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);
        if(left != null && right != null){
            return root;
        }else if (left != null){
            return left;
        }else{
            return right;
        }
        
    }
}

```

***
enjoy life, coding now!:D